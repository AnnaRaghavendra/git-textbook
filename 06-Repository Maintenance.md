# **Chapter 6 — Repository Maintenance**

## **6.1 Introduction**

During development, repositories often accumulate:

* Temporary files
* Build artifacts
* Generated files
* Experimental changes

Git provides tools to manage these situations:

```text
git clean
git stash
```

These commands help maintain a clean working environment without affecting commit history.

---

# **Git Clean**

## **6.2 What Is Git Clean?**

`git clean` removes untracked files and directories from the working directory.

Command:

```bash
git clean
```

### Important

Git clean affects:

```text
Untracked Files
Untracked Directories
```

It does not affect:

```text
Committed Files
Tracked Files
```

---

## **6.3 Why Use Git Clean?**

Common scenarios:

* Remove build files
* Remove temporary files
* Start with a clean repository
* Remove generated artifacts

Example:

Before:

```text
project/
├── app.py
├── temp.log
├── cache.txt
└── build/
```

After cleaning:

```text
project/
└── app.py
```

---

## **6.4 Preview Before Deleting**

Always perform a dry run first.

Command:

```bash
git clean -n
```

Example output:

```text
Would remove temp.log
Would remove cache.txt
```

### Why Use It?

Prevents accidental deletion.

### Mental Model

```text
-n = Preview Only
```

---

## **6.5 Force Deletion**

Git requires confirmation before deleting.

Command:

```bash
git clean -f
```

Meaning:

```text
Delete untracked files
```

### Mental Model

```text
-f = Force
```

---

## **6.6 Cleaning Directories**

By default:

```text
Directories are ignored
```

Example:

```text
build/
obj/
```

will not be removed.

Include directories:

```bash
git clean -d
```

Most commonly:

```bash
git clean -f -d
```

Meaning:

```text
Delete untracked files and directories
```

---

## **6.7 Why Staged Files Survive**

Example:

```bash
git add mylib.c
```

Now:

```text
mylib.c
```

becomes tracked.

Even if not committed.

Running:

```bash
git clean -f
```

will not delete it.

### Mental Model

```text
Tracked = Protected
Untracked = Removable
```

---

## **6.8 Common Git Clean Commands**

Preview:

```bash
git clean -n
```

Preview including directories:

```bash
git clean -n -d
```

Delete files:

```bash
git clean -f
```

Delete files and directories:

```bash
git clean -f -d
```

---

## **6.9 Git Clean Summary**

### Purpose

```text
Remove untracked files
```

### Important Commands

```bash
git clean -n
git clean -f
git clean -n -d
git clean -f -d
```

### Warning

Untracked files removed by Git Clean:

```text
Cannot be recovered from Git history
```

because Git never tracked them.

---

# **Git Stash**

## **6.10 What Is Git Stash?**

Git Stash temporarily stores uncommitted changes.

Command:

```bash
git stash
```

Git saves your work and restores a clean working directory.

---

## **6.11 Why Use Stash?**

Common scenario:

You are working on a feature.

Suddenly:

```text
Critical Bug Appears
```

You need to switch branches immediately.

Instead of committing unfinished work:

```bash
git stash
```

Then:

```bash
git switch main
```

Fix the bug.

Return later and restore your work.

---

## **6.12 How Stash Works**

Before:

```text
Working Directory
 ├── Modified File A
 └── Modified File B
```

Run:

```bash
git stash
```

After:

```text
Working Directory
 └── Clean
```

Changes are stored safely in the stash.

---

## **6.13 Viewing Stashes**

Command:

```bash
git stash list
```

Example:

```text
stash@{0}
stash@{1}
stash@{2}
```

Each stash entry stores saved work.

---

## **6.14 Restoring Stashed Changes**

Restore latest stash:

```bash
git stash apply
```

Result:

```text
Changes return
Stash remains
```

### Important

Apply does not remove the stash entry.

---

## **6.15 Restoring Staging State**

Normally:

```bash
git stash apply
```

restores files only.

Staging information may be lost.

Restore both:

```bash
git stash apply --index
```

Result:

```text
Files Restored
Staging Restored
```

### Mental Model

```text
--index = Restore Exactly
```

---

## **6.16 Removing Stashes**

Delete latest stash:

```bash
git stash drop
```

Delete specific stash:

```bash
git stash drop stash@{1}
```

---

## **6.17 Stash Workflow Example**

### Save Work

```bash
git stash
```

---

### View Saved Work

```bash
git stash list
```

---

### Restore Work

```bash
git stash apply
```

---

### Delete Saved Work

```bash
git stash drop
```

---

## **6.18 Common Uses of Stash**

### Temporary Context Switch

```text
Feature Work
      ↓
Urgent Bug Fix
      ↓
Return to Feature Work
```

---

### Pulling Changes Safely

Stash changes before:

```bash
git pull
```

Then restore afterward.

---

### Experimenting

Save current work.

Try something risky.

Restore original work if necessary.

---

## **6.19 Git Stash Summary**

### Purpose

```text
Temporarily save uncommitted work
```

### Important Commands

```bash
git stash
git stash list
git stash apply
git stash apply --index
git stash drop
```

### Mental Model

```text
Stash = Temporary Shelf for Work
```

---

## **6.20 Chapter Summary**

### Git Clean

```text
Remove untracked files and directories
```

Useful for:

* Build artifacts
* Temporary files
* Generated files

---

### Git Stash

```text
Temporarily save unfinished work
```

Useful for:

* Branch switching
* Emergency fixes
* Context switching

---

### Important Commands

```bash
git clean -n
git clean -f
git clean -f -d

git stash
git stash list
git stash apply
git stash apply --index
git stash drop
```

---

## **Practice**

### Exercise 1 — Git Clean

1. Create several untracked files.
2. Run:

```bash
git clean -n
```

3. Observe files that would be deleted.

4. Run:

```bash
git clean -f
```

5. Verify files are removed.

---

### Exercise 2 — Git Clean with Directories

1. Create:

```text
build/
obj/
```

2. Run:

```bash
git clean -n -d
```

3. Then:

```bash
git clean -f -d
```

4. Verify directories are removed.

---

### Exercise 3 — Git Stash

1. Modify several files.
2. Run:

```bash
git stash
```

3. Verify working directory is clean.

4. Run:

```bash
git stash apply
```

5. Verify changes return.

---

### Exercise 4 — Staging Recovery

1. Stage a file.
2. Run:

```bash
git stash
```

3. Restore using:

```bash
git stash apply --index
```

4. Verify staged state returns.
