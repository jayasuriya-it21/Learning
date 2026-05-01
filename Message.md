What you described is **NOT a logging system anymore** — it’s a **user-specific state management system**.

Let me restructure your idea clearly and show you **exactly how to implement it correctly** 👇

***

# ✅ 🧠 Your New Design Goal (Clear Interpretation)

You want:

### ✅ 1. Global candidate visibility

*   All users see **ACTIVE candidates**
*   Except:
    *   ❌ SELECTED → hidden for everyone
    *   ❌ REMOVED → hidden for everyone

***

### ✅ 2. Per-user status tracking

Each user can individually:

*   Shortlist
*   Reject
*   Assign
*   Revoke
*   Reassign

👉 These actions should NOT affect other users

***

### ✅ 3. Final blocking state

*   If a candidate becomes **SELECTED**
    👉 then NOT visible to any user anymore

***

### ✅ 4. Key idea

👉 `UserAction` is **NOT audit**
👉 It becomes **User-specific state table**

✅ This is a **completely valid enterprise design**

***

# ✅ 🔥 Final Architecture (IMPORTANT)

## ✅ Table Responsibilities

### ✅ CandidateProfile

```java
candidateStatus
```

👉 Global state:

*   ACTIVE
*   SELECTED ✅ (final)
*   REMOVED ✅ (final)

***

### ✅ UserAction

```java
user
candidate
updatedCandidateStatus
```

👉 User-specific state:

*   SHORTLISTED
*   REJECTED
*   ASSIGNED
*   etc

***

# ✅ ✅ RULES (VERY IMPORTANT)

## ✅ Rule 1 — CandidateProfile = GLOBAL STATUS

| Status   | Meaning           |
| -------- | ----------------- |
| ACTIVE   | Visible to all    |
| SELECTED | Hidden from all ✅ |
| REMOVED  | Hidden from all ✅ |

👉 Only **global final states go here**

***

## ✅ Rule 2 — UserAction = USER STATE

| Field                  | Used for           |
| ---------------------- | ------------------ |
| user\_id               | who                |
| candidate\_id          | which candidate    |
| updatedCandidateStatus | that user's status |

***

# ✅ ✅ HOW FLOW WORKS

***

## 🔵 Scenario 1 — User A shortlists

    UserAction:
    (UserA, Candidate1) → SHORTLISTED

    CandidateProfile:
    status → ACTIVE ✅ (no change)

***

## 🔵 Scenario 2 — User B rejects same candidate

    UserAction:
    (UserB, Candidate1) → REJECTED

    CandidateProfile:
    status → ACTIVE ✅

✅ Works independently per user

***

## 🔵 Scenario 3 — User A assigns

    UserAction:
    (UserA, Candidate1) → ASSIGNED

    CandidateProfile:
    status → ACTIVE ✅

***

## 🔵 Scenario 4 — User A SELECTS candidate ✅🔥

NOW:

    CandidateProfile:
    status → SELECTED ✅ (GLOBAL CHANGE)

    UserAction: (optional update)
    (UserA, Candidate1) → SELECTED

👉 Now:
❌ Candidate disappears for ALL users

***

# ✅ ✅ KEY CHANGE FROM PREVIOUS DESIGN

❌ You should NOT do this anymore:

```java
candidate.setCandidateStatus(ASSIGNED)
```

***

## ✅ Now only update candidate status for:

```java
SELECTED
REMOVED
```

***

| Table            | Purpose      |
| ---------------- | ------------ |
| CandidateProfile | GLOBAL state |
| UserAction       | USER state   |

***

# ✅ ✅ FINAL RULES YOU MUST FOLLOW

### ✅ CandidateProfile

Only update when:

*   SELECTED ✅
*   REMOVED ✅

***

### ✅ UserAction

Always update for:

*   SHORTLISTED
*   REJECTED
*   ASSIGNED
*   REVOKED
*   REASSIGN

***

# ✅ 🔥 RESULT

You now have:

✅ Multi-user independent workflows  
✅ Correct visibility rules  
✅ No conflicts between users  
✅ Enterprise-ready architecture

***

# CandidateStatusDto updateCandidateStatus() Method Changes
***

# ❌ CURRENT PROBLEM

Your method:

```java
candidate.setCandidateStatus(request.getStatus());
candidateProfileRepository.save(candidate);
```

***

## ❌ Why this is WRONG now

In your new architecture:

### ✅ CandidateProfile is ONLY for GLOBAL STATUS

Allowed:

*   ACTIVE
*   SELECTED ✅
*   REMOVED ✅

***

### ❌ But your method allows:

```java
SHORTLISTED ❌
REJECTED ❌
ASSIGNED ❌
```

👉 This **breaks your design**
👉 It will cause:

*   wrong visibility
*   users affecting each other ❌

***

# ✅ ✅ FIX (VERY IMPORTANT)

## ✅ Rule:

### ✅ ONLY update CandidateProfile for:

*   SELECTED ✅
*   REMOVED ✅

***

# ✅ ✅ EXACT FIX YOU MUST DO

***

## ✅ 🔹 1. REMOVE THIS LINE

```java
candidate.setCandidateStatus(request.getStatus());
```

***

## ✅ 🔹 2. ADD CONTROLLED UPDATE

Replace with:

```java
// ✅ Update global status ONLY for SELECTED or REMOVED
if (request.getStatus() == CandidateStatus.SELECTED
        || request.getStatus() == CandidateStatus.REMOVED) {

    candidate.setCandidateStatus(request.getStatus());
    candidate.setUpdatedBy(user.getUserId());
    candidateProfileRepository.save(candidate);
}
```

***

# ✅ ✅ RESULT

| Status      | Where stored |
| ----------- | ------------ |
| SHORTLISTED | UserAction ✅ |
| REJECTED    | UserAction ✅ |
| ASSIGNED    | UserAction ✅ |
| SELECTED    | BOTH ✅       |
| REMOVED     | BOTH ✅       |

***

# ✅ ✅ NEXT FIX (VERY IMPORTANT)

## ❌ Current logic

```java
UserAction statusRecord = userActionRepository
        .findByUserUserIdAndCandidateCandidateId(...)
        .orElseGet(UserAction::new);
```

👉 But you don’t initialize fields properly when new.

***

## ✅ ✅ FIX THIS BLOCK

Replace with:

```java
UserAction statusRecord = userActionRepository
        .findByUserUserIdAndCandidateCandidateId(userId, request.getCandidateId())
        .orElseGet(() -> {
            UserAction newAction = new UserAction();
            newAction.setUser(user);
            newAction.setCandidate(candidate);
            newAction.setCreatedBy(user.getUserId());
            return newAction;
        });
```

***

# ✅ ✅ KEEP THIS PART ✅

```java
statusRecord.setUpdatedCandidateStatus(request.getStatus());
statusRecord.setUpdateReason(request.getReason());
statusRecord.setUpdatedBy(user.getUserId());
```

***

# ✅ 🔥 OPTIONAL BUT STRONGLY RECOMMENDED

## ✅ Prevent illegal status change

Add validation:

```java
if (request.getStatus() == CandidateStatus.ASSIGNED) {
    throw new BadRequestException("Use Assign API instead");
}
```

***

# ✅ ✅ FINAL CORRECT FLOW

## When user clicks:

### ✅ SHORTLIST

*   Only UserAction updated ✅

***

### ✅ REJECT

*   Only UserAction updated ✅

***

### ✅ ASSIGN

*   Done via BE‑002 ✅

***

### ✅ SELECT ✅ (IMPORTANT)

*   CandidateProfile updated ✅
*   UserAction updated ✅

***

# ✅ ✅ FINAL VERSION (CLEAN)

Here is your corrected method:

```java
public CandidateStatusDto updateCandidateStatus(
        UpdateCandidateStatusRequestDto request,
        String userId) {

    User user = userRepository.findById(userId)
            .orElseThrow(() -> new RuntimeException(ProEvaConstants.noUser));

    CandidateProfile candidate = candidateProfileRepository
            .findById(request.getCandidateId())
            .orElseThrow(() -> new RuntimeException(ProEvaConstants.noCandidtae));

    // ❌ Prevent misuse
    if (request.getStatus() == CandidateStatus.ASSIGNED) {
        throw new BadRequestException("Use Assign API for assigning candidates");
    }

    // ✅ Update/Create UserAction
    UserAction statusRecord = userActionRepository
            .findByUserUserIdAndCandidateCandidateId(
                    userId, request.getCandidateId())
            .orElseGet(() -> {
                UserAction newAction = new UserAction();
                newAction.setUser(user);
                newAction.setCandidate(candidate);
                newAction.setCreatedBy(user.getUserId());
                return newAction;
            });

    statusRecord.setUpdatedCandidateStatus(request.getStatus());
    statusRecord.setUpdateReason(request.getReason());
    statusRecord.setUpdatedBy(user.getUserId());

    userActionRepository.save(statusRecord);

    // ✅ Update global status only when needed
    if (request.getStatus() == CandidateStatus.SELECTED
            || request.getStatus() == CandidateStatus.REMOVED) {

        candidate.setCandidateStatus(request.getStatus());
        candidate.setUpdatedBy(user.getUserId());
        candidateProfileRepository.save(candidate);
    }

    CandidateStatusDto responseDto = new CandidateStatusDto();
    responseDto.setCandidateData(
            CandidateMapperToDto.mapToCandidateProfileResponseDto(candidate));
    responseDto.setStatus(request.getStatus());
    responseDto.setReason(request.getReason());
    responseDto.setStatusUpdatedAt(user.getUpdatedAt());

    return responseDto;
}
```

***

# ✅ ✅ FINAL VERDICT

| Part         | Status                 |
| ------------ | ---------------------- |
| Your logic   | ✅ close                |
| Current code | ❌ breaks design        |
| After fix    | ✅ perfect architecture |

***

# 🚀 NEXT

Now your system is aligned:

👉 BE‑002 ✅  
👉 Status update ✅

***
