# **Chapter 4 — Rewriting History**

## **4.1 Introduction**

Git allows developers to modify commit history before sharing it with others.

This process is called **History Rewriting**.

Common uses:

* Clean commit history
* Fix commit messages
* Combine commits
* Remove unnecessary commits
* Reorganize development history

### Important Warning

History rewriting changes commit hashes.

Avoid rewriting commits that have already been pushed to shared branches.

---

# **Git Rebase**

## **4.2 What Is Rebase?**

Rebase replays commits from one branch on top of another branch.

Command:

```bash
git rebase <branch>
```

Example:

```text
A --- B --- C  (main)
     \
      D --- E  (feature)
```

Run:

```bash
git switch feature
git rebase main
```

Result:

```text
A --- B --- C --- D' --- E'
```

`D'` and `E'` are new rewritten commits.

---

## **4.3 How Rebase Works**

Git performs four steps:

1. Find common ancestor
2. Temporarily remove branch commits
3. Move branch to target branch
4. Replay commits one by one

### Mental Model

```text
Replay My Commits Somewhere Else
```

---

## **4.4 Why Use Rebase?**

Benefits:

* Cleaner history
* Fewer merge commits
* Easier to read logs
* Better feature branch maintenance

---

## **4.5 Rebase vs Merge**

### Merge

```text
A --- B --- C ------- M
     \             /
      D --- E ----
```

Creates merge commit.

---

### Rebase

```text
A --- B --- C --- D' --- E'
```

Creates linear history.

---

## **4.6 Rebase Safety**

### Good Use Cases

* Personal branches
* Local feature branches

### Bad Use Cases

* Shared branches
* Public branches
* Already-pushed commits

### Why?

Because:

```text
Rebase rewrites commit hashes
```

---

# **Interactive Rebase**

## **4.7 What Is Interactive Rebase?**

Interactive Rebase allows manual editing of commit history.

Command:

```bash
git rebase -i <commit>
```

Example:

```bash
git rebase -i HEAD~3
```

Git opens an editor showing commits.

---

## **4.8 Common Interactive Actions**

| Action | Purpose                                    |
| ------ | ------------------------------------------ |
| pick   | Keep commit                                |
| reword | Change commit message                      |
| edit   | Modify commit                              |
| squash | Combine commits                            |
| fixup  | Combine commits and discard second message |
| drop   | Remove commit                              |

Example:

```text
pick abc123 Add login
reword def456 Fix typo
drop ghi789 Temporary test
```

---

## **4.9 Reordering Commits**

Commits can be rearranged by changing their order in the editor.

Example:

Before:

```text
A --- B --- C --- D
```

Editor:

```text
pick B
pick D
pick C
```

Result:

```text
A --- B --- D' --- C'
```

Git rebuilds history in the new order.

---

## **4.10 When to Use Interactive Rebase**

Useful for:

* Cleaning feature branches
* Removing mistakes
* Reordering work
* Preparing commits before merge

### Mental Model

```text
Manual History Editing
```

---

# **Squash and Fixup Commits**

## **4.11 What Is Squashing?**

Squashing combines multiple commits into one.

Example:

Before:

```text
A --- B --- C --- D
```

After:

```text
A --- E
```

Where:

```text
E = B + C + D
```

---

## **4.12 Why Squash Commits?**

Without squashing:

```text
Add login
Fix typo
Forgot file
Cleanup
```

History becomes noisy.

After squashing:

```text
Add login feature
```

History becomes cleaner.

---

## **4.13 Squashing During Interactive Rebase**

Example:

```text
pick abc123 Add login
squash def456 Fix typo
```

Meaning:

```text
Combine def456 into abc123
```

Result:

```text
Single combined commit
```

### Important Rule

Squash always combines:

```text
Current Commit
      ↓
Previous Commit
```

---

## **4.14 What Is Fixup?**

Fixup is similar to squash.

Example:

```text
pick abc123 Add login
fixup def456 Typo fix
```

Result:

* Commits combined
* Second commit message discarded

---

## **4.15 Creating Fixup Commits**

Command:

```bash
git commit --fixup=<commit-id>
```

Example:

```bash
git commit --fixup=abc123
```

Creates a special fixup commit.

---

## **4.16 Autosquash**

Command:

```bash
git rebase -i --autosquash <commit>
```

Git automatically:

* Finds fixup commits
* Moves them
* Marks them for fixup

Useful for cleaning history efficiently.

---

# **Amending Commits**

## **4.17 What Is Amend?**

Amend replaces the most recent commit with a new version.

Command:

```bash
git commit --amend
```

---

## **4.18 Fixing Commit Messages**

Example:

Wrong:

```bash
git commit -m "Addd login"
```

Correct:

```bash
git commit --amend -m "Add login"
```

Result:

```text
Old commit replaced
New commit created
```

---

## **4.19 Adding Forgotten Files**

Forgot:

```text
README.md
```

Stage file:

```bash
git add README.md
```

Amend:

```bash
git commit --amend
```

Now the latest commit contains both changes.

---

## **4.20 What Happens Internally?**

Before:

```text
A --- B
```

After:

```text
A --- C
```

Git creates:

```text
New Commit
New Hash
```

The old commit becomes unreferenced.

---

## **4.21 When to Use Amend**

Good for:

* Fixing latest commit message
* Adding forgotten files
* Minor corrections

Avoid for:

* Older commits
* Shared commits

---

## **4.22 Summary**

### Rebase

```text
Replay commits on another base
```

### Interactive Rebase

```text
Manually edit commit history
```

### Squash

```text
Combine multiple commits
```

### Fixup

```text
Combine commits and discard second message
```

### Amend

```text
Replace latest commit
```

Important Commands:

```bash
git rebase main
git rebase -i HEAD~3
git commit --fixup=<commit-id>
git rebase -i --autosquash HEAD~3
git commit --amend
git commit --amend -m "message"
```

---

## **Practice**

### Exercise 1 — Rebase

1. Create a feature branch.
2. Add two commits.
3. Add a commit to main.
4. Rebase feature onto main.

---

### Exercise 2 — Interactive Rebase

1. Create three commits.
2. Run:

```bash
git rebase -i HEAD~3
```

3. Reorder commits.
4. Observe new history.

---

### Exercise 3 — Squash

1. Create three related commits.
2. Squash them into one.
3. Compare commit history before and after.

---

### Exercise 4 — Amend

1. Create a commit with a typo in the message.
2. Fix it using:

```bash
git commit --amend -m "Correct message"
```

3. Observe that the commit hash changes.
