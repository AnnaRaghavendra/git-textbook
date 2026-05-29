# **Chapter 7 — Remote Repositories and Collaboration**

## **7.1 Introduction**

So far, all Git operations have been performed locally.

However, modern software development is collaborative.

Developers need to:

* Share code
* Backup repositories
* Review changes
* Work in teams

This is achieved using **Remote Repositories**.

Common hosting platforms:

* GitHub
* GitLab
* Bitbucket

---

# **Remote Repositories**

## **7.2 What Is a Remote Repository?**

A remote repository is a Git repository hosted on another machine or server.

Example:

```text
Local Repository
       ↓
GitHub Repository
```

Local repository:

```text
C:\Projects\MyApp
```

Remote repository:

```text
https://github.com/user/myapp
```

---

## **7.3 Why Use Remote Repositories?**

Benefits:

* Backup code
* Collaborate with others
* Access code from multiple devices
* Share projects publicly

---

## **7.4 Viewing Remotes**

Show configured remotes:

```bash
git remote -v
```

Example:

```text
origin  https://github.com/user/project.git (fetch)
origin  https://github.com/user/project.git (push)
```

---

## **7.5 Adding a Remote**

Command:

```bash
git remote add origin <repository-url>
```

Example:

```bash
git remote add origin https://github.com/user/project.git
```

---

## **7.6 Understanding Origin**

`origin` is simply a name.

Example:

```text
origin
upstream
backup
```

are all valid remote names.

By convention:

```text
origin
```

is the primary remote repository.

### Mental Model

```text
origin = Main Remote Repository
```

---

# **Git Push**

## **7.7 What Is Git Push?**

Push uploads local commits to a remote repository.

Command:

```bash
git push
```

---

## **7.8 Why Push?**

Without push:

```text
Local Repository Only
```

With push:

```text
Local Repository
      ↓
Remote Repository
```

Others can now access your work.

---

## **7.9 First Push**

Common command:

```bash
git push -u origin main
```

Meaning:

```text
Push branch main to origin
Remember this relationship
```

---

## **7.10 What Does -u Mean?**

`-u` creates an upstream connection.

After:

```bash
git push -u origin main
```

future pushes become:

```bash
git push
```

without specifying branch names.

---

## **7.11 Push Workflow**

```text
Edit Files
      ↓
git add
      ↓
git commit
      ↓
git push
```

---

# **Git Fetch**

## **7.12 What Is Git Fetch?**

Fetch downloads changes from a remote repository.

Command:

```bash
git fetch
```

---

## **7.13 What Fetch Does**

Fetch:

* Downloads commits
* Updates remote-tracking branches

Fetch does NOT:

* Modify working files
* Modify current branch

### Mental Model

```text
Download Only
```

---

## **7.14 Example**

Before:

```text
origin/main
 ↓
A --- B
```

Remote gains:

```text
A --- B --- C
```

Run:

```bash
git fetch
```

Result:

```text
origin/main → C
main → B
```

Local branch remains unchanged.

---

## **7.15 Why Fetch Is Safe**

Because:

```text
No Local Changes Modified
```

You can inspect remote changes before integrating them.

---

# **Git Pull**

## **7.16 What Is Git Pull?**

Pull downloads and integrates remote changes.

Command:

```bash
git pull
```

---

## **7.17 How Pull Works**

Internally:

```text
git fetch
     +
git merge
```

Git performs both operations automatically.

---

## **7.18 Example**

Before:

```text
main → B
origin/main → C
```

Run:

```bash
git pull
```

Result:

```text
main → C
```

Local branch is updated.

---

## **7.19 Fetch vs Pull**

| Command | Downloads | Updates Current Branch |
| ------- | --------- | ---------------------- |
| fetch   | Yes       | No                     |
| pull    | Yes       | Yes                    |

### Mental Model

```text
fetch = Download
pull  = Download + Integrate
```

---

# **Repository Permissions**

## **7.20 Why Permissions Matter**

Not everyone should have full control of a repository.

Permissions protect projects from accidental changes.

---

## **7.21 Common Permission Levels**

### Read

Can:

* View code
* Clone repository

Cannot:

* Push changes

---

### Write

Can:

* Push commits
* Create branches
* Create pull requests

---

### Admin

Can:

* Manage repository
* Add collaborators
* Change settings
* Delete repository

---

## **7.22 Collaborators**

Repository owners can invite collaborators.

Example:

```text
Owner
 ↓
Adds Collaborator
 ↓
Collaborator Can Push
```

---

# **Pull Requests**

## **7.23 What Is a Pull Request?**

A Pull Request (PR) is a request to merge changes into another branch.

Commonly:

```text
feature
   ↓
main
```

---

## **7.24 Why Use Pull Requests?**

Benefits:

* Code review
* Team discussion
* Quality control
* Automated testing

---

## **7.25 Typical Pull Request Workflow**

```text
Create Branch
      ↓
Make Changes
      ↓
Push Branch
      ↓
Create Pull Request
      ↓
Review
      ↓
Merge
```

---

## **7.26 Example**

Feature branch:

```text
main
 ↓
A --- B

feature
 ↓
A --- B --- C --- D
```

Create PR:

```text
feature → main
```

After approval:

```text
A --- B --- C --- D
```

becomes part of main.

---

# **Team Collaboration Workflows**

## **7.27 Feature Branch Workflow**

Most common workflow.

Developers create separate branches.

Example:

```text
main
 ├── login-feature
 ├── dashboard-feature
 └── bugfix-auth
```

Each feature is developed independently.

---

## **7.28 Typical Team Workflow**

### Step 1

Get latest changes:

```bash
git pull
```

---

### Step 2

Create feature branch:

```bash
git switch -c login-feature
```

---

### Step 3

Develop feature:

```bash
git add .
git commit -m "Add login page"
```

---

### Step 4

Push branch:

```bash
git push -u origin login-feature
```

---

### Step 5

Create Pull Request.

---

### Step 6

Review and merge.

---

## **7.29 Common Collaboration Problems**

### Push Rejected

Cause:

```text
Remote has newer commits
```

Solution:

```bash
git pull
git push
```

---

### Merge Conflict

Cause:

```text
Two developers modified same code
```

Solution:

```text
Resolve Conflict
Commit
Push
```

---

### Working on Main Directly

Bad practice.

Prefer:

```text
Feature Branches
```

for development.

---

## **7.30 GitHub Repository Topics**

GitHub Topics help categorize repositories.

Example topics:

```text
git
version-control
git-tutorial
git-book
software-development
```

Benefits:

* Better discoverability
* Easier searching
* Improved project organization

---

## **7.31 Chapter Summary**

### Remote Repository

```text
Repository hosted on another machine
```

---

### Push

```text
Upload commits
```

---

### Fetch

```text
Download changes only
```

---

### Pull

```text
Download and integrate changes
```

---

### Pull Request

```text
Request to merge changes
```

---

### Team Workflow

```text
Pull
 ↓
Create Branch
 ↓
Develop
 ↓
Commit
 ↓
Push
 ↓
Pull Request
 ↓
Merge
```

---

### Important Commands

```bash
git remote -v

git remote add origin <url>

git push
git push -u origin main

git fetch

git pull

git switch -c <branch>

git push -u origin <branch>
```

---

## **Practice**

### Exercise 1 — Create a Remote

1. Create a GitHub repository.
2. Connect it:

```bash
git remote add origin <url>
```

3. Verify:

```bash
git remote -v
```

---

### Exercise 2 — First Push

1. Create a commit.
2. Run:

```bash
git push -u origin main
```

3. Verify commit appears on GitHub.

---

### Exercise 3 — Fetch and Pull

1. Add a commit from another device or GitHub.
2. Run:

```bash
git fetch
```

3. Observe differences.

4. Run:

```bash
git pull
```

5. Verify branch updates.

---

### Exercise 4 — Pull Request Workflow

1. Create a feature branch.
2. Add a commit.
3. Push the branch.
4. Create a Pull Request.
5. Merge it into main.
6. Study the resulting commit history.
