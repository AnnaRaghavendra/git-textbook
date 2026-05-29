# **Chapter 8 — Releases and Versioning**

## **8.1 Introduction**

As projects evolve, developers need a way to mark important points in history.

Examples:

* First stable release
* Major update
* Bug-fix release
* Production deployment

Git provides **Tags** for this purpose.

A tag acts as a permanent label attached to a specific commit.

---

# **Git Tags**

## **8.2 What Is a Tag?**

A tag is a named reference to a commit.

Example:

```text
A --- B --- C --- D
           ↑
          v1.0
```

Here:

```text
v1.0 → Commit C
```

The tag permanently points to commit `C`.

---

## **8.3 Why Use Tags?**

Without tags:

```text
Deploy commit a8c91f2
```

Hard to remember.

With tags:

```text
Deploy v1.0
```

Easy to understand.

### Common Uses

* Software releases
* Product versions
* Production deployments
* Milestones

---

## **8.4 Tags vs Branches**

Many beginners confuse tags and branches.

### Branch

```text
main
 ↓
A --- B --- C
```

As new commits are added:

```text
main
 ↓
A --- B --- C --- D --- E
```

The branch moves.

---

### Tag

```text
A --- B --- C --- D
           ↑
          v1.0
```

Even after new commits:

```text
A --- B --- C --- D --- E --- F
           ↑
          v1.0
```

The tag never moves.

### Mental Model

```text
Branch = Moving Pointer
Tag    = Permanent Bookmark
```

---

## **8.5 Lightweight Tags**

A lightweight tag is a simple pointer.

Create:

```bash
git tag v1.0
```

Result:

```text
v1.0 → Current Commit
```

### Characteristics

* Simple
* Fast
* No metadata

---

## **8.6 Viewing Tags**

List all tags:

```bash
git tag
```

Example:

```text
v1.0
v1.1
v2.0
```

---

## **8.7 Tagging Older Commits**

Tags can be attached to previous commits.

Find commit:

```bash
git log --oneline
```

Example:

```text
abc123 Add login
def456 Add dashboard
```

Tag specific commit:

```bash
git tag v1.0 abc123
```

Result:

```text
v1.0 → abc123
```

---

# **Annotated Tags**

## **8.8 What Is an Annotated Tag?**

Annotated tags store additional information.

Create:

```bash
git tag -a v1.0 -m "First stable release"
```

### Metadata Stored

* Tag name
* Tag message
* Tagger
* Date

---

## **8.9 Why Use Annotated Tags?**

Professional projects generally use annotated tags for releases.

Benefits:

* Release notes
* Metadata
* Better history tracking

### Mental Model

```text
Lightweight Tag
    ↓
Simple Pointer

Annotated Tag
    ↓
Full Release Record
```

---

## **8.10 Understanding -a and -m**

### `-a`

```text
Create Annotated Tag
```

---

### `-m`

```text
Provide Tag Message
```

Example:

```bash
git tag -a v2.0 -m "Major release"
```

---

## **8.11 Viewing Tag Details**

Show tag information:

```bash
git show v1.0
```

Example output:

```text
Tag: v1.0
Message: First stable release

commit abc123
Author: John Doe
```

Useful for reviewing release information.

---

# **Working with Tags**

## **8.12 Checking Out a Tag**

Move repository to tag state:

```bash
git checkout v1.0
```

Result:

```text
Repository appears exactly as it did at v1.0
```

### Common Uses

* Debug old releases
* Reproduce bugs
* Inspect previous versions

---

## **8.13 Creating Releases**

Typical workflow:

```bash
git add .
git commit -m "Release ready"

git tag -a v1.0 -m "First stable release"
```

Result:

```text
Release Commit
      ↓
Tagged as v1.0
```

---

# **Pushing Tags**

## **8.14 Why Tags Are Not Pushed Automatically**

Commits and tags are separate Git objects.

Running:

```bash
git push
```

does not automatically push tags.

---

## **8.15 Push a Single Tag**

```bash
git push origin v1.0
```

Pushes only:

```text
v1.0
```

to the remote repository.

---

## **8.16 Push All Tags**

```bash
git push --tags
```

Pushes every local tag.

---

## **8.17 Viewing Tags on GitHub**

After pushing:

```text
Repository
   ↓
Releases / Tags
```

GitHub displays tags and release information.

---

# **Deleting Tags**

## **8.18 Delete Local Tag**

Remove local tag:

```bash
git tag -d v1.0
```

Result:

```text
Tag removed locally
```

---

## **8.19 Delete Remote Tag**

Remove remote tag:

```bash
git push origin --delete v1.0
```

Result:

```text
Tag removed from remote repository
```

---

## **8.20 Local vs Remote Deletion**

Deleting locally:

```text
Does NOT remove remote tag
```

Deleting remotely:

```text
Does NOT remove local tag
```

Both actions are independent.

---

# **Versioning Strategies**

## **8.21 Common Version Format**

Most projects use:

```text
MAJOR.MINOR.PATCH
```

Example:

```text
1.0.0
1.1.0
1.1.1
2.0.0
```

---

## **8.22 Semantic Versioning Basics**

### Major

```text
Breaking Changes
```

Example:

```text
1.0.0 → 2.0.0
```

---

### Minor

```text
New Features
```

Example:

```text
1.1.0 → 1.2.0
```

---

### Patch

```text
Bug Fixes
```

Example:

```text
1.1.1 → 1.1.2
```

---

## **8.23 Real-World Release Example**

```text
v1.0.0
 ↓
Initial Release

v1.1.0
 ↓
New Dashboard

v1.1.1
 ↓
Bug Fixes

v2.0.0
 ↓
Major Redesign
```

---

## **8.24 Chapter Summary**

### Tag

```text
Named reference to a commit
```

---

### Lightweight Tag

```text
Simple pointer
```

Create:

```bash
git tag v1.0
```

---

### Annotated Tag

```text
Tag with metadata
```

Create:

```bash
git tag -a v1.0 -m "Release message"
```

---

### Important Commands

```bash
git tag

git tag v1.0

git tag -a v1.0 -m "message"

git show v1.0

git push origin v1.0

git push --tags

git tag -d v1.0

git push origin --delete v1.0
```

---

### Mental Model

```text
Branch = Moving Pointer

Tag = Permanent Bookmark
```

---

## **Practice**

### Exercise 1 — Lightweight Tag

1. Create a commit.
2. Run:

```bash
git tag v1.0
```

3. Verify:

```bash
git tag
```

---

### Exercise 2 — Annotated Tag

1. Create:

```bash
git tag -a v1.1 -m "Second release"
```

2. View details:

```bash
git show v1.1
```

---

### Exercise 3 — Tag an Older Commit

1. View history:

```bash
git log --oneline
```

2. Choose an older commit.

3. Create:

```bash
git tag v0.9 <commit-id>
```

---

### Exercise 4 — Push Tags

1. Create several tags.
2. Run:

```bash
git push --tags
```

3. Verify tags appear on GitHub.

---

### Exercise 5 — Delete Tags

1. Delete local tag:

```bash
git tag -d v1.0
```

2. Delete remote tag:

```bash
git push origin --delete v1.0
```

3. Verify removal.
