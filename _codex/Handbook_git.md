---
---

<img width="960" height="401" alt="Git-logo-white svg" src="https://github.com/user-attachments/assets/2cea87ae-b7af-4b07-9918-81384fe8070e" />

# ABOUT GIT

Git is a distributed version control software system[10] that is capable of managing versions of source code or data. It is often used to control source code by programmers who are developing software collaboratively.

# Specify a specific account when using git clone

For HTTPS cloning, you can force Git to use a specific account by prepending the username to the URL. This is useful if you have multiple accounts and want to ensure Git prompts you for the credentials of the correct one. 
```
git clone git@github.com:username/repository.git
```
# Setting Commit Identity for the Repo

Navigate into the repository and run:
```
git config user.name "Your Name"
git config user.email "your-account-email@example.com"
```

# List all changes
Shows line-by-line changes in all modified files (unstaged changes).
```
git diff
```

# File specific changess
```
git diff fileName.txt
```

# Short summary of all changes
Shows line-by-line changes in all modified files (unstaged changes).
```
git diff --stat
```
Example output:
```
...SessionRoleAuthorizeAttribute.cs | 12 +++---
...Mastermind.csproj                |  3 ++-
```

# list everything in a repo except files ignored by .gitignore
```
git ls-files --cached --others --exclude-standard
```
What it does:
--cached → includes tracked files
--others → includes untracked files
--exclude-standard → applies .gitignore, .git/info/exclude, and global gitignore

# If you want it for a specific folder
```
git ls-files --cached --others --exclude-standard -- .\your-folder\
```

# Staged everything except

**Exclude a specific folder:**
```bash
git add -A -- . ':(exclude)folder_to_ignore'
```

**Exclude a specific file:**
```bash
git add -A -- . ':(exclude)secret.txt'
```

**Exclude all files with a certain extension (e.g. `.log`):**
```bash
git add -A -- . ':(exclude)*.log'
```

**Exclude multiple specific files:**
```bash
git add -A -- . ':!file1.txt' ':!folder/file2.cs' ':!Sem04-Sommatif_1/StudentClient/StudentClient/ConfigHelper.cs'
```
