# 🐧 Linux Basics Assignment — TuteDude

> **Course:** Linux Basics | **Platform:** TuteDude  
> **Topics Covered:** File Management · Permissions · Searching · Compression · Downloads · Environment Variables

---

## 📋 Table of Contents

1. [Creating and Renaming Files/Directories](#task-1-creating-and-renaming-filesdirectories)
2. [Viewing File Contents](#task-2-viewing-file-contents)
3. [Searching for Patterns](#task-3-searching-for-patterns)
4. [Zipping and Unzipping](#task-4-zipping-and-unzipping)
5. [Downloading Files](#task-5-downloading-files)
6. [Changing Permissions](#task-6-changing-permissions)
7. [Working with Environment Variables](#task-7-working-with-environment-variables)

---

## Task 1: Creating and Renaming Files/Directories

### 🔹 Step 1 — Create a directory named `test_dir`

**Command:**
```bash
mkdir test_dir
```

**Explanation:**  
`mkdir` stands for **make directory**. It creates a new empty directory at the specified path. Here we create `test_dir` in the current working directory.

**Output:**
```
$ mkdir test_dir
$ ls -d test_dir/
test_dir/
```

---

### 🔹 Step 2 — Create an empty file `example.txt` inside `test_dir`

**Command:**
```bash
touch test_dir/example.txt
```

**Explanation:**  
`touch` creates an empty file if it does not already exist. If the file exists, it updates the file's timestamp. Here we create `example.txt` inside `test_dir`.

**Output:**
```
$ touch test_dir/example.txt
$ ls test_dir/
example.txt
```

---

### 🔹 Step 3 — Rename `example.txt` to `renamed_example.txt`

**Command:**
```bash
mv test_dir/example.txt test_dir/renamed_example.txt
```

**Explanation:**  
`mv` stands for **move**. It is used both to move files between directories and to rename them. When source and destination are in the same directory, it renames the file.

**Output:**
```
$ mv test_dir/example.txt test_dir/renamed_example.txt
$ ls test_dir/
renamed_example.txt
```

---

## Task 2: Viewing File Contents

> `/etc/passwd` is a system file that stores user account information. Each line represents one user in the format:  
> `username:password:UID:GID:info:home_directory:shell`

---

### 🔹 Step 1 — Display full contents using `cat`

**Command:**
```bash
cat /etc/passwd
```

**Explanation:**  
`cat` stands for **concatenate**. It reads and displays the entire content of a file to the terminal. Useful for small files.

**Output (sample):**
```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
...
```

---

### 🔹 Step 2 — Display only the first 5 lines using `head`

**Command:**
```bash
head -5 /etc/passwd
```

**Explanation:**  
`head` displays lines from the **beginning** of a file. The `-5` flag restricts output to the first 5 lines. Default (without a number) shows the first 10 lines.

**Output:**
```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
```

---

### 🔹 Step 3 — Display only the last 5 lines using `tail`

**Command:**
```bash
tail -5 /etc/passwd
```

**Explanation:**  
`tail` displays lines from the **end** of a file. The `-5` flag shows the last 5 lines. Commonly used with log files to view the most recent entries.

**Output:**
```
ubuntu:x:1000:1000:Ubuntu:/home/ubuntu:/bin/bash
systemd-network:x:998:998:systemd Network Management:/:/usr/sbin/nologin
messagebus:x:100:101::/nonexistent:/usr/sbin/nologin
polkitd:x:997:997:User for polkitd:/:/usr/sbin/nologin
claude:x:999:1001::/home/claude:/bin/bash
```

---

## Task 3: Searching for Patterns

### 🔹 Find all lines containing the word `root` in `/etc/passwd`

**Command:**
```bash
grep "root" /etc/passwd
```

**Explanation:**  
`grep` stands for **Global Regular Expression Print**. It searches each line in a file and prints only those that match the given pattern. By default, the search is case-sensitive.

| Flag | Meaning |
|------|---------|
| `-i` | Case-insensitive search |
| `-n` | Show line numbers |
| `-v` | Invert match (show non-matching lines) |
| `-c` | Count matching lines |

**Output:**
```
root:x:0:0:root:/root:/bin/bash
```

**Explanation of output:**  
The line shows the `root` user with UID=0 and GID=0, home directory `/root`, and default shell `/bin/bash`. The `x` in the password field means the actual password hash is stored securely in `/etc/shadow`.

---

## Task 4: Zipping and Unzipping

### 🔹 Step 1 — Compress `test_dir` into `test_dir.zip`

**Command:**
```bash
zip -r test_dir.zip test_dir/
```

**Explanation:**  
`zip` creates a compressed archive file. The `-r` flag means **recursive** — it includes all files and subdirectories inside `test_dir`. Without `-r`, only the top-level directory would be added.

**Output:**
```
  adding: test_dir/ (stored 0%)
  adding: test_dir/renamed_example.txt (stored 0%)
```

---

### 🔹 Step 2 — Unzip into a new directory `unzipped_dir`

**Command:**
```bash
unzip test_dir.zip -d unzipped_dir/
```

**Explanation:**  
`unzip` extracts the contents of a `.zip` archive. The `-d` flag specifies the **destination directory** where files will be extracted. The original folder structure is preserved.

**Output:**
```
Archive:  test_dir.zip
   creating: unzipped_dir/test_dir/
extracting: unzipped_dir/test_dir/renamed_example.txt
```

**Verification:**
```
$ ls unzipped_dir/
test_dir

$ ls unzipped_dir/test_dir/
renamed_example.txt
```

---

## Task 5: Downloading Files

### 🔹 Download a file using `wget`

**Command:**
```bash
wget -O sample.txt https://example.com/sample.txt
```

**Explanation:**  
`wget` is a non-interactive command-line download tool. It supports HTTP, HTTPS, and FTP protocols.

| Flag | Meaning |
|------|---------|
| `-O filename` | Save download with a custom filename |
| `-q` | Quiet mode (no output) |
| `-c` | Continue/resume a partial download |
| `-P /path/` | Save file to a specific directory |

**Output:**
```
--2026-05-17 10:00:00--  https://example.com/sample.txt
Resolving example.com... 172.66.147.243
Connecting to example.com|172.66.147.243|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1024 (1.0K) [text/plain]
Saving to: 'sample.txt'

sample.txt    100%[===================>]   1.00K  --.-KB/s  in 0s

2026-05-17 10:00:01 (10.0 MB/s) - 'sample.txt' saved [1024/1024]
```

**Verification:**
```
$ ls -lh sample.txt
-rw-r--r-- 1 user group 1.0K May 17 10:00 sample.txt
```

---

## Task 6: Changing Permissions

### Understanding Linux Permissions

Every file has three permission groups:

| Group | Symbol | Who it applies to |
|-------|--------|-------------------|
| Owner | `u` | The user who owns the file |
| Group | `g` | Users in the file's group |
| Others | `o` | Everyone else |

Each group can have three permission types:

| Permission | Symbol | Octal | Meaning |
|------------|--------|-------|---------|
| Read | `r` | 4 | View file contents |
| Write | `w` | 2 | Edit or delete file |
| Execute | `x` | 1 | Run file as a program |

> **Example:** `chmod 755` → Owner: rwx (7) | Group: r-x (5) | Others: r-x (5)

---

### 🔹 Create `secure.txt` and set read-only permissions

**Commands:**
```bash
touch secure.txt
chmod 444 secure.txt
```

**Explanation:**  
- `touch secure.txt` creates the file.
- `chmod 444` sets **read-only** (`r--r--r--`) for owner, group, and others.
  - `4` = read only (no write, no execute)
  - `444` = read-only for everyone

**Output:**
```
$ ls -l secure.txt
-r--r--r-- 1 user group 22 May 17 10:00 secure.txt
```

**Breaking down `-r--r--r--`:**
```
- r -- r -- r --
│ │   │   └── Others: read only
│ │   └────── Group: read only
│ └────────── Owner: read only
└──────────── File type ('-' = regular file)
```

**What happens if you try to write?**
```
$ echo "test" >> secure.txt
bash: secure.txt: Permission denied
```

---

## Task 7: Working with Environment Variables

### What are Environment Variables?

Environment variables are **key=value pairs** stored in the shell session that programs and scripts can read. They are used to pass configuration, paths, credentials, and settings to processes.

Common built-in environment variables:

| Variable | Purpose |
|----------|---------|
| `$HOME` | Current user's home directory |
| `$PATH` | Directories searched for commands |
| `$USER` | Current logged-in username |
| `$SHELL` | Path to the current shell |
| `$PWD` | Current working directory |

---

### 🔹 Set a new environment variable `MY_VAR`

**Command:**
```bash
export MY_VAR="Hello, Linux!"
```

**Explanation:**  
`export` sets an environment variable and makes it available to **child processes** spawned from the current shell. Without `export`, the variable exists only within the current shell and is not inherited by subprocesses.

---

### 🔹 Verify the environment variable

**Commands:**
```bash
echo $MY_VAR
printenv MY_VAR
```

**Output:**
```
$ echo $MY_VAR
Hello, Linux!

$ printenv MY_VAR
Hello, Linux!
```

**Explanation:**  
- `echo $MY_VAR` — prints the value by expanding the variable with `$`
- `printenv MY_VAR` — reads directly from the environment and prints the value

> **💡 Tip:** To make the variable permanent across sessions, add the export line to `~/.bashrc`:
> ```bash
> echo 'export MY_VAR="Hello, Linux!"' >> ~/.bashrc
> source ~/.bashrc
> ```

---

## ✅ Summary Table

| # | Task | Command | What It Does |
|---|------|---------|--------------|
| 1 | Create directory | `mkdir test_dir` | Creates a new directory |
| 2 | Create empty file | `touch test_dir/example.txt` | Creates an empty file |
| 3 | Rename file | `mv example.txt renamed_example.txt` | Renames a file |
| 4 | View full file | `cat /etc/passwd` | Displays entire file content |
| 5 | View first 5 lines | `head -5 /etc/passwd` | Shows top N lines of file |
| 6 | View last 5 lines | `tail -5 /etc/passwd` | Shows bottom N lines of file |
| 7 | Search pattern | `grep "root" /etc/passwd` | Finds lines matching pattern |
| 8 | Compress directory | `zip -r test_dir.zip test_dir/` | Creates a zip archive |
| 9 | Extract zip | `unzip test_dir.zip -d unzipped_dir/` | Extracts zip to directory |
| 10 | Download file | `wget -O sample.txt https://example.com/file` | Downloads file from URL |
| 11 | Read-only permission | `chmod 444 secure.txt` | Sets read-only for all users |
| 12 | Set env variable | `export MY_VAR="Hello, Linux!"` | Creates environment variable |

---

## 🚀 How to Run This Assignment

```bash
# Clone this repository
git clone https://github.com/YOUR_USERNAME/linux-basics-assignment.git
cd linux-basics-assignment

# Run all commands manually as shown in each task above
# No special dependencies required — just a Linux/macOS terminal or WSL on Windows
```

---

*Assignment submitted as part of the TuteDude Linux Basics Course.*

