# **Chapter 10 — Essential Git Concepts**

## **10.1 Working Directory, Staging Area, and Repository**

### What Are the Three Git Areas?

Every Git project consists of three important areas:

```text
Working Directory
       ↓
Staging Area
       ↓
Repository
```

---

### Working Directory

The Working Directory contains your actual project files.

Example:

```text
project/
├── app.py
├── README.md
└── notes.txt
```

Changes made here are not yet tracked by Git.

---

### Staging Area

The Staging Area (Index) stores changes that are ready to be committed.

Example:

```bash
git add app.py
```

Now:

```text
app.py
     ↓
Staging Area
```

---

### Repository

The Repository contains commit history.

Example:

```bash
git commit -m "Add login feature"
```

Git stores a snapshot inside the repository.

---

### Complete Flow

```text
Modify File
      ↓
Working Directory
      ↓
git add
      ↓
Staging Area
      ↓
git commit
      ↓
Repository
```

### Mental Model

```text
Working Directory = Workspace
Staging Area      = Draft
Repository        = Permanent History
```

---

# **10.2 Git Status**

## What Is Git Status?

Displays the current state of the repository.

Command:

```bash
git status
```

---

## Why Use It?

Shows:

* Modified files
* Staged files
* Untracked files
* Current branch

---

## Common File States

### Untracked

```text
New file not known to Git
```

Example:

```text
notes.txt
```

---

### Modified

```text
Tracked file changed
```

---

### Staged

```text
Ready for commit
```

---

### Committed

```text
Stored in repository
```

---

### Typical Workflow

```text
Untracked
    ↓
Modified
    ↓
Staged
    ↓
Committed
```

### Mental Model

```text
git status = Repository Dashboard
```

---

# **10.3 Git Revert**

## What Is Revert?

Creates a new commit that undoes a previous commit.

Command:

```bash
git revert <commit>
```

---

## Why Use Revert?

Unlike reset:

```text
reset
 ↓
Rewrites History
```

```text
revert
 ↓
Preserves History
```

---

## Example

History:

```text
A --- B --- C
```

Revert C:

```bash
git revert C
```

Result:

```text
A --- B --- C --- D
```

Where:

```text
D = Undo of C
```

---

## When To Use Revert

Best for:

```text
Shared Branches
Public Repositories
Team Projects
```

### Mental Model

```text
Revert = Safe Undo
```

---

# **10.4 Git Show**

## What Is Git Show?

Displays detailed information about commits, tags, and objects.

Command:

```bash
git show
```

Shows:

* Commit information
* Author
* Date
* Changes

---

## Show Latest Commit

```bash
git show
```

---

## Show Specific Commit

```bash
git show abc123
```

---

## Example Output

```text
Commit Message
Author
Date

Modified Lines
```

### Mental Model

```text
git show = Inspect Commit
```

---

# **10.5 Detached HEAD**

## What Is Detached HEAD?

Normally:

```text
HEAD → main
```

Git expects HEAD to point to a branch.

---

## How Detached HEAD Happens

Example:

```bash
git checkout abc123
```

Result:

```text
HEAD → Commit
```

instead of:

```text
HEAD → Branch
```

---

## Why Is It Dangerous?

New commits may become difficult to find later.

Example:

```text
main
 ↓
A --- B --- C

HEAD
 ↓
B
```

Create commit:

```text
A --- B --- X
```

Commit `X` is not attached to a branch.

---

## Recovery

Create a branch:

```bash
git switch -c rescue-branch
```

### Mental Model

```text
Detached HEAD = Not On A Branch
```

---

# **10.6 Git Clone**

## What Is Clone?

Creates a local copy of a remote repository.

Command:

```bash
git clone <url>
```

Example:

```bash
git clone https://github.com/user/project.git
```

---

## What Happens?

Git automatically:

```text
Downloads Repository
Creates Local Copy
Configures Origin
```

---

## Result

```text
Remote Repository
       ↓
Local Repository
```

---

## Verify Remote

```bash
git remote -v
```

### Mental Model

```text
Clone = Download Repository
```

---

# **10.7 .gitignore**

## What Is .gitignore?

A file that tells Git which files to ignore.

Example:

```text
.gitignore
```

---

## Why Use It?

Do not commit:

* Build files
* Cache files
* Logs
* Secrets

---

## Example

```text
*.log
__pycache__/
node_modules/
.env
```

Git ignores matching files.

---

## Common Python Example

```text
__pycache__/
*.pyc
.env
```

---

## Common JavaScript Example

```text
node_modules/
dist/
.env
```

### Mental Model

```text
.gitignore = Ignore List
```

---

# **10.8 Forks and Upstream Repositories**

## What Is a Fork?

A fork is your personal copy of someone else's repository.

Example:

```text
Original Repository
         ↓
        Fork
         ↓
Your Account
```

---

## Why Fork?

Common in open-source projects.

Allows:

* Safe experimentation
* Independent development
* Pull Request contributions

---

## Typical Fork Workflow

```text
Fork Repository
       ↓
Clone Fork
       ↓
Create Branch
       ↓
Make Changes
       ↓
Push Changes
       ↓
Create Pull Request
```

---

## What Is Upstream?

The original repository.

Example:

```text
origin   → Your Fork
upstream → Original Repository
```

---

## Add Upstream

```bash
git remote add upstream <url>
```

Verify:

```bash
git remote -v
```

---

## Why Use Upstream?

To receive updates from the original project.

Example:

```bash
git fetch upstream
```

### Mental Model

```text
origin   = My Copy
upstream = Original Source
```

---

# **10.9 Git Cherry-Pick**

## What Is Cherry-Pick?

Copies a commit from one branch to another.

Command:

```bash
git cherry-pick <commit>
```

---

## Example

Branch:

```text
main
 ↓
A --- B

feature
 ↓
A --- B --- C
```

Copy commit C:

```bash
git cherry-pick C
```

Result:

```text
main
 ↓
A --- B --- C'
```

---

## Why Use Cherry-Pick?

Useful when:

* Only one commit is needed
* Avoid full merge
* Apply bug fixes elsewhere

---

## Cherry-Pick vs Merge

### Merge

```text
Bring Entire Branch
```

---

### Cherry-Pick

```text
Bring Specific Commit
```

### Mental Model

```text
Cherry-Pick = Copy One Commit
```

---

# **10.10 Chapter Summary**

### Working Directory

```text
Where files are edited
```

---

### Staging Area

```text
Where changes are prepared
```

---

### Repository

```text
Where commits are stored
```

---

### Important Commands

```bash
git status

git revert <commit>

git show
git show <commit>

git clone <url>

git remote add upstream <url>

git cherry-pick <commit>
```

---

### Key Concepts

```text
Working Directory → Workspace

Staging Area → Draft

Repository → History

Revert → Safe Undo

Clone → Download Repository

Fork → Personal Copy

Upstream → Original Repository

Cherry-Pick → Copy Commit
```

---

## **Practice**

### Exercise 1 — Git Status

1. Create a new file.
2. Run:

```bash
git status
```

3. Observe the file state.

---

### Exercise 2 — Revert

1. Create a commit.
2. Run:

```bash
git revert <commit>
```

3. Observe the new undo commit.

---

### Exercise 3 — Detached HEAD

1. Checkout an old commit:

```bash
git checkout <commit>
```

2. Observe Detached HEAD.

3. Recover:

```bash
git switch -c rescue-branch
```

---

### Exercise 4 — .gitignore

1. Create `.gitignore`.
2. Add:

```text
*.log
temp/
```

3. Verify ignored files.

---

### Exercise 5 — Cherry-Pick

1. Create a feature branch.
2. Add a commit.
3. Switch to main.
4. Run:

```bash
git cherry-pick <commit>
```

5. Verify the commit appears on main.
