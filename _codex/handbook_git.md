<img width="960" height="401" alt="Git-logo-white svg" src="https://github.com/user-attachments/assets/2cea87ae-b7af-4b07-9918-81384fe8070e" />

# ABOUT GIT

Git is a distributed version control software system that is capable of managing versions of source code or data. It is often used to control source code by programmers who are developing software collaboratively.

# Preface

This content is intended for console use. While the appeal of a GUI like SourceTree is understandable, using a CLI makes it easier to spot problems and use AI when necessary.

The goal of this article is to provide the basic steps, common problems, and their solutions in a simplified way.

# 3 basic steps to push

The basic Git workflow is:

### 1. Add

Stage your changes:

```bash
git add .
```

### 2. Commit

Create a commit with a message:

```bash
git commit -m "Your commit message"
```

### 3. Push

Push your commit to the remote repository:

```
git push
```

So, the usual workflow is:

```
git add .
git commit -m "Your commit message"
git push
```

# Branch

## Committing to a Branch 

Checkout (switch to) the branch where you want the commit: 
```
git checkout branch_name 
```
 

If the branch doesn’t exist yet, create and switch with: 
```
git checkout -b branch_name 
```
 

Stage your changes: 
```
git add <files> 
```
 

Commit your staged changes: 
```
git commit -m "Your commit message" 
```
 

Push to remote: 
```
git push origin branch_name
```

---

## merge a branch to main 

Switch to main: 
```
git checkout main 
```
 

Pull the latest changes on main from the remote: 
```
git pull origin main 
```
 

Merge the other branch (e.g., feature-branch) into main: 
```
git merge feature-branch 
```
 

If there are merge conflicts, resolve them manually: 

Check Conflict Status 
```
Git status 
```

Open Each Conflicted File using any text editor. 

```
Look for conflict markers within each file: 
<<<<<<< HEAD 
// your local changes 
======= 
// remote changes 
>>>>>>> origin/main 
Remove all the <<<<<<<, =======, and >>>>>>> markers after resolving the code. 
```

Stage the Resolved Files 
```
Git add <filename> 
```
Commit the merge 
```
git commit -m "Resolved merge conflicts" 
```
push back to the remote 
```
git push 
```
 

Push the updated main branch to the remote: 
```
git push origin main
```



# Analyze

## List all branch
```
git branch -a
```

## List all changes
Shows line-by-line changes in all modified files (unstaged changes).
```
git diff
```

## File specific changes
```
git diff fileName.txt
```

## Short summary of all changes
Shows line-by-line changes in all modified files (unstaged changes).
```
git diff --stat
```
Example output:
```
...SessionRoleAuthorizeAttribute.cs | 12 +++---
...Mastermind.csproj                |  3 ++-
```

## list everything in a repo except files ignored by .gitignore
```
git ls-files --cached --others --exclude-standard
```
What it does:
--cached → includes tracked files
--others → includes untracked files
--exclude-standard → applies .gitignore, .git/info/exclude, and global gitignore

## If you want it for a specific folder
```
git ls-files --cached --others --exclude-standard -- .\your-folder\
```

# Add

## Stage everything except

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

# Commit

## use a file as a commit message
```
git commit -F <path_to_file>
```

## Setting Commit Identity for the Repo

Navigate into the repository and run:
```
git config user.name "Your Name"
git config user.email "your-account-email@example.com"
```

# TroubleShoot

## Specify a specific account when using git clone

For HTTPS cloning, you can force Git to use a specific account by prepending the username to the URL. This is useful if you have multiple accounts and want to ensure Git prompts you for the credentials of the correct one. 
```
git clone git@github.com:username/repository.git
```

## Reset 
Cancel last commit while keeping the modification intact
```
git reset --soft HEAD~1
```

