# **Chapter 5 — Undoing and Recovery**

## **5.1 Introduction**

Mistakes are inevitable during development.

Common mistakes include:

* Incorrect commits
* Wrong commit messages
* Accidental resets
* Failed rebases
* Lost commits

Git provides several tools to recover from these situations.

The most important are:

```text
HEAD
git reset
git reflog
```

---

# **Understanding HEAD**

## **5.2 What Is HEAD?**

`HEAD` is a special pointer that represents your current position in the repository.

Example:

```text
A --- B --- C (HEAD)
```

Currently:

```text
HEAD → C
```

Git commands often operate relative to HEAD.

---

## **5.3 HEAD References**

Git allows navigation relative to HEAD.

| Expression | Meaning            |
| ---------- | ------------------ |
| HEAD       | Current commit     |
| HEAD~1     | Previous commit    |
| HEAD~2     | Two commits back   |
| HEAD~3     | Three commits back |

Example:

```text
A --- B --- C --- D (HEAD)
```

Then:

```text
HEAD    → D
HEAD~1  → C
HEAD~2  → B
HEAD~3  → A
```

---

## **5.4 Why HEAD Matters**

Many commands use HEAD:

```bash
git reset HEAD~1
git rebase HEAD~3
git checkout HEAD~2
```

Understanding HEAD makes these commands easier to understand.

### Mental Model

```text
HEAD = Current Position in History
```

---

# **Git Reset**

## **5.5 What Is Reset?**

`git reset` moves HEAD to another commit.

Command:

```bash
git reset HEAD~1
```

Meaning:

```text
Move HEAD back one commit
```

---

## **5.6 The Three Git Areas**

To understand reset, remember Git's three areas:

```text
Working Directory
      ↓
Staging Area
      ↓
Repository (HEAD)
```

Different reset modes affect different areas.

---

## **5.7 Soft Reset**

Command:

```bash
git reset --soft HEAD~1
```

Effects:

| Area         | Result     |
| ------------ | ---------- |
| History      | Moves back |
| Staging Area | Preserved  |
| Files        | Preserved  |

### Use Case

Undo a commit while keeping everything staged.

Example:

```text
Commit removed
Changes still ready to commit
```

### Mental Model

```text
Undo Commit Only
```

---

## **5.8 Mixed Reset**

Command:

```bash
git reset --mixed HEAD~1
```

or simply:

```bash
git reset HEAD~1
```

Effects:

| Area         | Result     |
| ------------ | ---------- |
| History      | Moves back |
| Staging Area | Reset      |
| Files        | Preserved  |

### Use Case

Undo commit and unstage changes.

### Mental Model

```text
Undo Commit + Unstage
```

---

## **5.9 Hard Reset**

Command:

```bash
git reset --hard HEAD~1
```

Effects:

| Area         | Result     |
| ------------ | ---------- |
| History      | Moves back |
| Staging Area | Reset      |
| Files        | Reset      |

### Example

Before:

```text
A --- B --- C (HEAD)
```

After:

```text
A --- B (HEAD)
```

Changes from `C` disappear.

### Mental Model

```text
Undo Everything
```

---

## **5.10 Reset Comparison**

| Reset Type | History | Staging | Files |
| ---------- | ------- | ------- | ----- |
| soft       | Move    | Keep    | Keep  |
| mixed      | Move    | Reset   | Keep  |
| hard       | Move    | Reset   | Reset |

---

## **5.11 Common Uses of Reset**

### Undo Last Commit

```bash
git reset --soft HEAD~1
```

---

### Unstage Files

```bash
git reset HEAD~1
```

---

### Return to Earlier Commit

```bash
git reset --hard <commit>
```

---

## **5.12 Reset vs Revert**

### Reset

```text
Rewrites history
```

Used mostly on local branches.

---

### Revert

```text
Creates a new commit that undoes another commit
```

Safer for shared branches.

---

# **Git Reflog**

## **5.13 What Is Reflog?**

Reflog records where HEAD has pointed.

Git tracks:

* Commits
* Resets
* Rebases
* Checkouts
* Merges

Command:

```bash
git reflog
```

---

## **5.14 Why Reflog Is Important**

Reflog acts as a safety net.

Even after:

```bash
git reset --hard
```

the old commits often still exist.

Reflog helps find them.

---

## **5.15 Reading Reflog Output**

Example:

```text
abc123 HEAD@{0}: reset: moving to HEAD~1
def456 HEAD@{1}: commit: Add login
```

Meaning:

```text
Current HEAD → abc123
Previous HEAD → def456
```

---

## **5.16 Recovering Lost Commits**

Suppose:

```bash
git reset --hard HEAD~1
```

removed a commit.

Find it:

```bash
git reflog
```

Example:

```text
def456 HEAD@{1}: commit: Add login
```

Recover:

```bash
git reset --hard def456
```

Commit restored.

---

## **5.17 Why Recovery Works**

Reset usually does not immediately destroy commits.

Instead:

```text
Commit becomes unreferenced
```

Git keeps these commits temporarily.

Reflog allows recovery before garbage collection removes them.

---

## **5.18 Common Recovery Scenarios**

### Recover After Hard Reset

```bash
git reflog
git reset --hard <commit>
```

---

### Recover After Bad Rebase

```bash
git reflog
git reset --hard <commit>
```

---

### Recover Deleted Branch Work

Find old commit in reflog and reset to it.

---

## **5.19 Important Warnings**

### Hard Reset Is Dangerous

```bash
git reset --hard
```

can remove:

* Uncommitted work
* File changes
* Staged changes

Always verify before using it.

---

### Reflog Is Local

Reflog exists only on your machine.

Other developers cannot access your reflog history.

---

## **5.20 Summary**

### HEAD

```text
Current position in history
```

---

### Reset

```text
Move HEAD to another commit
```

---

### Reflog

```text
History of HEAD movements
```

---

### Reset Types

| Command             | Meaning                 |
| ------------------- | ----------------------- |
| `git reset --soft`  | Undo commit only        |
| `git reset --mixed` | Undo commit and unstage |
| `git reset --hard`  | Undo everything         |

---

### Important Commands

```bash
git reset --soft HEAD~1
git reset HEAD~1
git reset --hard HEAD~1

git reflog

git reset --hard <commit>
```

---

## **Practice**

### Exercise 1 — HEAD

1. Create four commits.
2. Identify:

   * HEAD
   * HEAD~1
   * HEAD~2

---

### Exercise 2 — Reset

1. Create three commits.
2. Try:

   * soft reset
   * mixed reset
   * hard reset
3. Observe differences using:

```bash
git status
git log --oneline
```

---

### Exercise 3 — Recovery

1. Create a commit.
2. Run:

```bash
git reset --hard HEAD~1
```

3. Recover using:

```bash
git reflog
git reset --hard <commit>
```

4. Verify the commit is restored.
