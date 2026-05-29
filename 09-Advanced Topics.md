# **Chapter 9 — Advanced Topics**

## **9.1 Introduction**

This chapter focuses on how Git is used in real projects.

Rather than introducing new basic commands, we will:

* Learn professional workflows
* Understand advanced Git concepts
* Solve common Git problems
* Practice real-world Git scenarios

---

# **Professional Git Workflows**

## **9.2 What Is a Git Workflow?**

A workflow is a set of rules that teams follow when using Git.

A good workflow helps teams:

* Avoid conflicts
* Maintain clean history
* Collaborate effectively
* Release software safely

---

## **9.3 Feature Branch Workflow**

The most common workflow.

Example:

```text id="d4u9z8"
main
 ├── login-feature
 ├── payment-feature
 └── bugfix-auth
```

Each feature is developed in its own branch.

### Workflow

```text id="c8s9v2"
Create Branch
      ↓
Develop Feature
      ↓
Commit Changes
      ↓
Push Branch
      ↓
Pull Request
      ↓
Merge
```

### Benefits

* Isolated development
* Easier reviews
* Safer collaboration

---

## **9.4 GitHub Flow**

A lightweight workflow commonly used on GitHub.

Steps:

1. Create branch
2. Make changes
3. Push branch
4. Create Pull Request
5. Review
6. Merge

Example:

```text id="v7h1q4"
main
 ↓
feature
 ↓
Pull Request
 ↓
Merge
```

---

## **9.5 Common Team Rules**

### Rule 1

Do not work directly on:

```text id="b1k6n0"
main
```

---

### Rule 2

Use meaningful commit messages.

Good:

```text id="l8p2s7"
Add login validation
```

Bad:

```text id="j5r4d9"
fix
```

---

### Rule 3

Keep commits focused.

One commit should represent one logical change.

---

### Rule 4

Review code before merging.

---

## **9.6 Professional Commit Strategy**

Good history:

```text id="h7x3p1"
Add login page
Add password validation
Add authentication tests
```

Poor history:

```text id="f3v8m6"
fix
oops
another fix
test
```

Clean history saves time later.

---

# **Advanced Git Internals**

## **9.7 Revisiting Git Objects**

Git stores:

```text id="y2n4c8"
Blob
Tree
Commit
Tag
```

Everything in Git is built on these objects.

---

## **9.8 Commit Graph**

Example:

```text id="m5r1w9"
A --- B --- C --- D
```

Each commit stores:

```text id="g9q3t2"
Parent Commit
Tree Snapshot
Metadata
```

Git history is actually a graph.

---

## **9.9 Branches Revisited**

A branch is only:

```text id="s4j6x7"
A Pointer
```

Example:

```text id="t1z8p5"
main
 ↓
A --- B --- C
```

The branch itself contains no files.

It simply points to a commit.

---

## **9.10 Detached HEAD**

Normally:

```text id="r8m2y6"
HEAD → main
```

Sometimes:

```text id="4w7k9d"
HEAD → Commit
```

Example:

```bash id="d9q1c4"
git checkout abc123
```

Result:

```text id="n3v5b8"
Detached HEAD
```

You are no longer on a branch.

### Why It Matters

Commits created here may become difficult to find later.

---

## **9.11 Garbage Collection**

Git periodically removes:

```text id="k6x2r1"
Unused Objects
```

Command:

```bash id="p7m4v9"
git gc
```

Purpose:

* Reduce repository size
* Remove unreachable objects
* Optimize storage

---

# **Troubleshooting and Recovery Scenarios**

## **9.12 Scenario: Wrong Commit Message**

Problem:

```text id="q5n8w2"
Addd login
```

Solution:

```bash id="a4t6y7"
git commit --amend -m "Add login"
```

---

## **9.13 Scenario: Forgot a File**

Problem:

```text id="u9r3m1"
README.md missing
```

Solution:

```bash id="h2v7c5"
git add README.md
git commit --amend
```

---

## **9.14 Scenario: Accidentally Deleted Commit**

Problem:

```bash id="c1x8n6"
git reset --hard HEAD~1
```

Solution:

```bash id="r5p9j2"
git reflog
git reset --hard <commit>
```

---

## **9.15 Scenario: Wrong Branch**

Problem:

```text id="g7m3v1"
Feature committed to main
```

Possible solution:

```bash id="b4n8q6"
git branch feature
git reset --hard HEAD~1
```

Move work to proper branch.

---

## **9.16 Scenario: Merge Conflict**

Problem:

Two developers modify same code.

Solution:

1. Open conflicted file.
2. Remove markers.
3. Keep correct code.
4. Stage file.
5. Commit merge.

---

## **9.17 Scenario: Unfinished Work but Need Branch Switch**

Solution:

```bash id="x9j5t3"
git stash
git switch main
```

Return later:

```bash id="k2r8v4"
git stash apply
```

---

## **9.18 Scenario: Accidentally Squashed Commits**

Solution:

```bash id="t7m1x5"
git reflog
git reset --hard <commit>
```

Restore pre-rebase state.

---

## **9.19 Scenario: Push Rejected**

Cause:

```text id="w6c2n8"
Remote has newer commits
```

Solution:

```bash id="p3v7r9"
git pull
git push
```

---

## **9.20 Scenario: Repository Contains Build Files**

Solution:

```bash id="j8n4m2"
git clean -n
git clean -f -d
```

Removes untracked generated files.

---

# **Practical Git Katas and Exercises**

## **9.21 Kata 1 — Branching**

### Goal

Practice branch creation and merging.

Steps:

```bash id="n5x1p8"
git switch -c feature
```

Add commits.

Merge into main.

Observe history.

---

## **9.22 Kata 2 — Merge Conflict**

### Goal

Practice conflict resolution.

Steps:

1. Create two branches.
2. Modify same line differently.
3. Merge branches.
4. Resolve conflict.

---

## **9.23 Kata 3 — Rebase**

### Goal

Practice history rewriting.

Steps:

1. Create feature branch.
2. Add commits.
3. Update main.
4. Rebase feature onto main.

---

## **9.24 Kata 4 — Squash**

### Goal

Combine multiple commits.

Steps:

```bash id="u7m3v6"
git rebase -i HEAD~3
```

Replace:

```text id="r2n8w4"
pick
```

with:

```text id="g5t1x9"
squash
```

Combine commits.

---

## **9.25 Kata 5 — Recovery**

### Goal

Recover lost work.

Steps:

```bash id="y4k7m2"
git reset --hard HEAD~1
```

Recover using:

```bash id="f9r3v8"
git reflog
git reset --hard <commit>
```

---

## **9.26 Kata 6 — Stash Workflow**

### Goal

Practice temporary work storage.

Steps:

```bash id="q6n2x7"
git stash
git stash list
git stash apply
git stash drop
```

---

## **9.27 Kata 7 — Tags**

### Goal

Practice release management.

Steps:

```bash id="m8v4r1"
git tag v1.0
git tag -a v1.1 -m "Release"
git push --tags
```

---

# **9.28 Final Summary**

Professional developers:

```text id="w1p8m3"
Use Branches
Create Small Commits
Review Code
Use Pull Requests
Tag Releases
Keep History Clean
```

Git Internals:

```text id="t6n4x8"
Blob
Tree
Commit
Tag
```

Recovery Tools:

```text id="a3r7v2"
git reset
git reflog
git stash
git clean
```

Most Git mistakes are recoverable if:

```text id="k9m2w5"
You Stay Calm
Check Reflog
Avoid Panic Commands
```

---

## **Mastery Checklist**

You should now be able to:

* Create repositories
* Commit changes
* Work with branches
* Merge code
* Resolve conflicts
* Rebase safely
* Squash commits
* Recover lost work
* Use tags
* Collaborate using GitHub
* Understand Git internals
* Follow professional workflows

Completing these skills means you possess a solid practical foundation in Git and GitHub.
