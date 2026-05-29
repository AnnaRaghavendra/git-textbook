# **Chapter 2 — The Internal Architecture of Git**

## **2.1 Introduction**

Most beginners think Git stores files and folders like a normal backup system.

This is not true.

Git is fundamentally an **object database**.

Everything inside Git is stored as objects identified by unique SHA hashes.

Understanding Git's internal architecture makes advanced topics such as branching, merging, rebasing, and recovery much easier to understand.

---

## **2.2 Git as an Object Database**

Git stores data as objects.

Each object:

* Has a SHA hash (unique identifier)
* Contains data
* Can reference other objects

Example:

```text
e69de29...
a1b2c3d...
fc1da67...
```

These hashes uniquely identify Git objects.

### Important Concept

Git is not a file-based history system.

Git is an:

```text
Object Database
      ↓
Objects connected by hashes
```

---

## **2.3 The Four Core Git Objects**

Git mainly uses four object types:

| Object | Purpose                            |
| ------ | ---------------------------------- |
| Blob   | Stores file contents               |
| Tree   | Stores directory structure         |
| Commit | Stores project snapshot metadata   |
| Tag    | Stores named references to commits |

---

## **2.4 Blob Objects**

A Blob stores:

```text
File Content Only
```

A Blob does **not** store:

* File name
* Folder name
* File path

Example file:

```python
print("Hello World")
```

Git stores:

```text
Blob
 └── print("Hello World")
```

The blob knows the content but not the file name.

### Mental Model

```text
Blob = Raw File Data
```

---

## **2.5 Tree Objects**

A Tree represents a directory structure.

It connects:

* File names
* Folder names
* Blob objects
* Other tree objects

Example project:

```text
project/
├── README.md
└── src/
    └── app.py
```

Tree structure:

```text
Root Tree
├── README.md → Blob
└── src → Tree
```

### Mental Model

```text
Tree = Folder Snapshot
```

---

## **2.6 Commit Objects**

A Commit stores:

* Author
* Committer
* Date
* Commit message
* Parent commit
* Root tree

Example:

```bash
git commit -m "Add login feature"
```

Git creates a commit object that points to a tree.

### Important Concept

A commit does not directly store files.

Instead:

```text
Commit
   ↓
Tree
   ↓
Blobs
```

### Mental Model

```text
Commit = Snapshot Metadata
```

---

## **2.7 Tag Objects**

A Tag is a named reference to a commit.

Example:

```bash
git tag v1.0
```

Result:

```text
v1.0 → Commit abc123
```

Tags are commonly used for:

* Releases
* Versions
* Milestones

### Mental Model

```text
Tag = Permanent Bookmark
```

---

## **2.8 Exploring Git Objects**

Git provides commands for inspecting objects.

### Show Object Contents

```bash
git cat-file -p <sha>
```

Example:

```bash
git cat-file -p fc1da67
```

Displays the contents of an object.

---

### Show Object Type

```bash
git cat-file -t <sha>
```

Possible output:

```text
blob
tree
commit
tag
```

---

### Show Object Size

```bash
git cat-file -s <sha>
```

Displays object size in bytes.

---

## **2.9 Listing Tree Contents**

### Root Tree

```bash
git ls-tree master
```

Example:

```text
100644 blob e69de29 README.md
040000 tree a1b2c3d src
```

---

### Entire Repository

```bash
git ls-tree -r master
```

Lists all files recursively.

---

## **2.10 Understanding Git's Object Graph**

Git objects form a graph.

Example:

```text
master
  ↓
commit fc1da67
  ↓
tree a1b2c3

tree a1b2c3
  ├── blob e69de29 (README.md)
  └── tree 8f3c1ab (src)

tree 8f3c1ab
  └── blob abcd123 (app.py)
```

This structure represents the entire repository.

---

## **2.11 Branches and the Object Graph**

A branch is simply a pointer.

Example:

```text
main
  ↓
commit abc123
```

The branch points to a commit.

The commit points to a tree.

The tree points to blobs and other trees.

---

## **2.12 Why This Matters**

Many advanced Git features become easier to understand:

* Branches
* Tags
* Merges
* Rebases
* Resets
* Recovery

Because all of them operate on Git objects and references.

---

## **2.13 Summary**

Git stores data as objects.

The four core objects are:

```text
Blob
Tree
Commit
Tag
```

Relationship:

```text
Branch
  ↓
Commit
  ↓
Tree
  ↓
Blob
```

Key commands:

```bash
git cat-file -p <sha>
git cat-file -t <sha>
git cat-file -s <sha>
git ls-tree master
git ls-tree -r master
```

Git is fundamentally:

```text
A Content-Addressable Object Database
```

Everything else in Git is built on top of these objects.

---

## **Practice**

1. Create a repository and make a commit.
2. Run `git log --oneline` and copy the commit SHA.
3. Use `git cat-file -p <sha>` to inspect the commit.
4. Find the tree SHA inside the commit.
5. Inspect the tree using `git cat-file -p`.
6. Use `git cat-file -t` to identify object types.
7. Draw the object graph for your repository.
