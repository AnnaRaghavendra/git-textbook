# **Chapter 3 — Branching and Merging**

## **3.1 Introduction**

One of Git's most powerful features is the ability to create branches.

Branches allow developers to:

* Work on new features
* Fix bugs
* Experiment safely
* Develop independently

Without affecting the main project.

---

## **3.2 Understanding Branches**

A branch is simply a pointer to a commit.

Example:

```text
main
 ↓
A --- B --- C
```

Here:

```text
main → C
```

The branch points to the latest commit.

### Why Branches Exist

Without branches:

* Every change affects the main project.

With branches:

* Work can be isolated safely.

Example:

```text
main
 ↓
A --- B --- C

feature
 ↓
A --- B --- C --- D --- E
```

The feature branch can evolve independently.

### Mental Model

```text
Branch = Movable Pointer to a Commit
```

---

## **3.3 Creating Branches**

Create a new branch:

```bash
git branch feature
```

Result:

```text
main
 ↓
A --- B --- C
            ↑
         feature
```

Both branches initially point to the same commit.

---

## **3.4 Switching Branches**

Switch to an existing branch:

```bash
git switch feature
```

Create and switch immediately:

```bash
git switch -c feature
```

### View Branches

```bash
git branch
```

Example:

```text
* main
  feature
```

The `*` indicates the current branch.

---

## **3.5 Viewing Branch Information**

Show branch names and latest commits:

```bash
git branch -v
```

Example:

```text
main    a1b2c3 Add login
feature d4e5f6 Add dashboard
```

---

## **3.6 Comparing Branches**

Git can compare two branches.

Command:

```bash
git diff main feature
```

Shows:

* Added lines
* Removed lines
* Modified lines

### Use Case

Before merging:

```bash
git diff main feature
```

Review what will change.

---

## **3.7 Visualizing Branch History**

Display branch graph:

```bash
git log --oneline --graph --all
```

Example:

```text
* d4e5f6 Add dashboard
| * a1b2c3 Add login
|/
* f7g8h9 Initial commit
```

Useful for understanding branch structure.

---

# **Fast-Forward Merges**

## **3.8 What Is a Fast-Forward Merge?**

A Fast-Forward Merge occurs when the target branch has not changed since the branch was created.

Example:

```text
A --- B (main)
      \
       C --- D (feature)
```

Only the feature branch moved forward.

---

## **3.9 Performing a Fast-Forward Merge**

Switch to main:

```bash
git switch main
```

Merge:

```bash
git merge feature
```

Result:

```text
A --- B --- C --- D
                  ↑
                main
```

Git simply moves the branch pointer.

---

## **3.10 Characteristics of Fast-Forward Merges**

* No merge commit created
* Linear history
* Clean commit graph
* Usually conflict-free

### Mental Model

```text
Move Branch Pointer Forward
```

---

# **Three-Way Merges**

## **3.11 What Is a Three-Way Merge?**

A Three-Way Merge occurs when both branches have new commits.

Example:

```text
A --- B --- D (main)
      \
       C --- E (feature)
```

Both branches evolved independently.

---

## **3.12 Why It Is Called Three-Way**

Git compares three commits:

```text
Common Ancestor
Current Branch
Incoming Branch
```

Example:

```text
Ancestor = B
Current  = D
Incoming = E
```

---

## **3.13 Performing a Three-Way Merge**

```bash
git switch main
git merge feature
```

Result:

```text
      D -------- M
     /          /
A --- B        /
     \        /
      C --- E
```

`M` = Merge Commit

---

## **3.14 Characteristics of Three-Way Merges**

* Creates merge commit
* Preserves branch history
* Shows branch structure
* May produce conflicts

### Mental Model

```text
Combine Two Histories
```

---

# **Merge Conflicts**

## **3.15 What Is a Merge Conflict?**

A merge conflict occurs when Git cannot determine which change should be kept.

Example:

Original:

```python
print("hello")
```

Main branch:

```python
print("hello world")
```

Feature branch:

```python
print("hello john")
```

Git cannot decide automatically.

---

## **3.16 Conflict Markers**

Git inserts markers:

```text
<<<<<<< HEAD
print("hello world")
=======
print("hello john")
>>>>>>> feature
```

Meaning:

* Above separator → current branch
* Below separator → incoming branch

---

## **3.17 Resolving Conflicts Manually**

### Step 1

Attempt merge:

```bash
git merge feature
```

---

### Step 2

Check status:

```bash
git status
```

---

### Step 3

Open conflicted file.

Remove conflict markers.

Choose final code.

Example:

```python
print("hello world")
```

---

### Step 4

Mark resolved:

```bash
git add file.py
```

---

### Step 5

Finish merge:

```bash
git commit
```

Git creates the merge commit.

---

## **3.18 Common Causes of Conflicts**

* Same line edited differently
* Simultaneous bug fixes
* Large refactoring
* Long-lived branches

---

# **Merge Tools**

## **3.19 Why Merge Tools Exist**

Manual conflict resolution becomes difficult for large projects.

Merge tools provide visual interfaces.

Benefits:

* Easier comparison
* Faster resolution
* Fewer mistakes

---

## **3.20 Vimdiff**

Launch:

```bash
git mergetool --tool=vimdiff
```

Vimdiff displays:

* Current branch
* Incoming branch
* Merged result

Useful for experienced Vim users.

### Drawbacks

* Steep learning curve
* Requires Vim knowledge

---

## **3.21 Emerge**

Launch:

```bash
git mergetool --tool=emerge
```

Emerge is the Emacs merge tool.

Useful for developers already familiar with Emacs.

### Drawbacks

* Requires Emacs knowledge
* Less common today

---

## **3.22 Modern Alternatives**

Many developers prefer graphical tools:

* VS Code
* IntelliJ IDEA
* GitKraken
* SourceTree

These tools simplify conflict resolution significantly.

---

## **3.23 Summary**

A branch is:

```text
A pointer to a commit
```

Important commands:

```bash
git branch
git branch <name>
git switch <name>
git switch -c <name>
git branch -v
git diff <branchA> <branchB>
git merge <branch>
git log --oneline --graph --all
```

Merge Types:

```text
Fast-Forward Merge
→ Moves branch pointer

Three-Way Merge
→ Creates merge commit
```

Conflicts occur when Git cannot automatically combine changes.

Merge tools help resolve conflicts more efficiently.

---

## **Practice**

1. Create a repository and make three commits.
2. Create a branch named `feature`.
3. Add a commit on `feature`.
4. Perform a Fast-Forward Merge.
5. Create two branches with different changes.
6. Perform a Three-Way Merge.
7. Intentionally create a merge conflict.
8. Resolve the conflict manually.
9. Run:

```bash
git log --oneline --graph --all
```

and study the resulting graph.
