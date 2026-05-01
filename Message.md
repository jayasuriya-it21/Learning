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

# ✅ ✅ BE‑002 CHANGE (IMPORTANT UPDATE)

## ❌ OLD BEHAVIOR

```java
candidate.setCandidateStatus(ASSIGNED);  ❌ REMOVE THIS
```

***

## ✅ NEW BEHAVIOR

### Only:

```java
UserAction → ASSIGNED ✅
```

👉 DO NOT change CandidateProfile status

***

# ✅ ✅ Updated BE‑002 Logic

Change your service like this:

***

## ✅ ✅ UPDATE THIS PART

### ❌ REMOVE

```java
candidate.setCandidateStatus(CandidateStatus.ASSIGNED);
candidateProfileRepository.save(candidate);
```

***

### ✅ KEEP ONLY THIS

```java
userAction.setUpdatedCandidateStatus(CandidateStatus.ASSIGNED);
```

***

# ✅ ✅ Query Logic (CRITICAL PART)

Now your APIs must behave like this:

***

## ✅ View All Candidates Page

```sql
WHERE candidateStatus != SELECTED
AND candidateStatus != REMOVED
```

✅ returns global candidates

***

## ✅ Shortlisted Page

```sql
FROM user_action
WHERE user_id = currentUser
AND updatedCandidateStatus = SHORTLISTED
```

***

## ✅ Assigned To Me

```sql
FROM candidate_assignment
WHERE assigned_to_user_id = currentUser
AND is_active = true
```

***

## ✅ Assigned By Me

```sql
WHERE assigned_by_user_id = currentUser
```

***

# ✅ ✅ Important Change Required in UserAction

Your current constraint:

```java
@UniqueConstraint(columnNames = { "user_id", "candidate_id" })
```

✅ KEEP THIS ✅

Why?

👉 Because each user has **only ONE state per candidate**

✔ Clean  
✔ Simple  
✔ No duplicates

***

# ✅ ✅ Updated Service Logic (Core Rule)

Replace:

```java
userAction = find or create
```

✅ ALWAYS DO:

```java
Optional<UserAction> existing =
    userActionRepository.findByUser_UserIdAndCandidate_CandidateId(userId, candidateId);

if (existing.isPresent()) {
    userAction = existing.get();
} else {
    userAction = new UserAction();
    userAction.setUser(user);
    userAction.setCandidate(candidate);
    userAction.setCreatedBy(userId);
}

userAction.setUpdatedCandidateStatus(CandidateStatus.ASSIGNED);
userAction.setUpdateReason(request.getInstruction());
userAction.setUpdatedBy(userId);

userActionRepository.save(userAction);
```

***

# ✅ ✅ FINAL ANSWER TO YOUR QUESTION

> ❓ “how to connect both tables?”

### ✅ Answer:

👉 **DON’T connect by logic — connect by purpose**

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

# ✅ 🚀 NEXT STEP (VERY IMPORTANT)

Now your BE‑002 is correct ✅
