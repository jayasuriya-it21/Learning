# Linux Luminarium
---

### 📁 `ls` – List directory contents  
**Usage:** `ls [OPTIONS] [PATH]`  
**Common Options:**
- `-l`: long listing format (permissions, size, date, etc.)
- `-a`: show all files, including hidden (starting with `.`)
- `-h`: human-readable sizes (with `-l`)
- `-R`: recursively list subdirectories

---

### 📄 `cat` – Concatenate and display file content  
**Usage:** `cat [FILE...]`  
**Common Use Cases:**
- `cat file.txt`: display content of `file.txt`
- `cat file1 file2`: concatenate multiple files

---

### 📂 `cd` – Change current directory  
**Usage:** `cd [DIRECTORY]`  
**Useful Tips:**
- `cd`: go to your home directory
- `cd ~`: also goes to your home directory
- `cd ..`: move up one directory
- `cd -`: switch to previous directory

---

### 🔍 `find` – Search for files in a directory hierarchy  
**Usage:** `find [PATH] [OPTIONS]`  
**Common Options:**
- `-name "pattern"`: search by file name
- `-type f`: search for files
- `-type d`: search for directories
- `-exec command {} \;`: run a command on each result

Example:
```bash
find . -name "*.txt"        # Find all .txt files in current dir
```

---

### 🔎 `grep` – Search for patterns within files  
**Usage:** `grep [OPTIONS] PATTERN [FILE...]`  
**Common Options:**
- `-i`: ignore case
- `-r`: recursive search in directories
- `-n`: show line numbers
- `--color=auto`: highlight matches

Example:
```bash
grep "flag" notes.txt
grep -rn "main" src/
```

---

### 🔗 `ln` – Create links between files  
**Usage:** `ln [OPTIONS] TARGET LINK_NAME`  
**Types of Links:**
- **Hard link**: `ln original.txt link.txt`
- **Symbolic (soft) link**: `ln -s original.txt link.txt`

**Common Options:**
- `-s`: create a symbolic link
- `-f`: force overwrite existing links

---

These commands are **foundational** for Linux navigation and scripting. Practicing them in challenges at [pwn.college](https://pwn.college/linux-luminarium/commands/) will give you solid hands-on experience. 