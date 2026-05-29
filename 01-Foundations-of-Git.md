# **Chapter 1 — Introduction to Version Control**

## **1.1 What Is Version Control?**

Version Control is a system that records changes made to files over time.

It allows you to:

* Track changes
* Restore previous versions
* Collaborate with others
* Maintain a history of a project

Without Version Control:

```text
report.doc
report_final.doc
report_final_v2.doc
report_final_v3_REAL.doc
```

With Version Control:

```text
Project
 ├── Version 1
 ├── Version 2
 ├── Version 3
 └── Complete History
```

---

## **1.2 Why Git Was Created**

Before Git, many Version Control Systems were:

* Slower
* Centralized
* Less flexible

Git was created by **Linus Torvalds** in 2005 to manage the development of the Linux Kernel.

Git focuses on:

* Speed
* Reliability
* Distributed development
* Efficient storage

---

## **1.3 Benefits of Git**

Git helps developers:

* Track project history
* Work safely on new features
* Collaborate with teams
* Recover lost work
* Experiment without risk

Example:

```text
Main Project
     │
     ├── Feature A
     ├── Feature B
     └── Bug Fix
```

Each feature can be developed independently and merged later.

---

## **1.4 Local vs Remote Repository**

### Local Repository

Stored on your computer.

Example:

```text
C:\Projects\MyApp
```

You can commit, branch, and view history without internet access.

### Remote Repository

Stored on a server such as GitHub.

Example:

```text
https://github.com/user/project
```

Used for:

* Backup
* Collaboration
* Sharing code

---

## **1.5 Basic Git Workflow**

A typical Git workflow follows four steps:

```text
Modify Files
      ↓
Stage Changes
      ↓
Create Commit
      ↓
Push to Remote
```

Example:

```bash
git add .
git commit -m "Add login page"
git push
```

---

## **1.6 Key Terms**

### Repository (Repo)

A project managed by Git.

### Commit

A snapshot of the project at a specific point in time.

### Branch

An independent line of development.

### Merge

Combining changes from different branches.

### Remote

A shared repository hosted elsewhere.

---

## **1.7 Summary**

* Version Control tracks file changes over time.
* Git is a distributed Version Control System.
* Git stores project history as commits.
* Repositories can be local or remote.
* A typical workflow is:

```text
Edit → Stage → Commit → Push
```

The next chapter introduces Git's three fundamental areas:

```text
Working Directory
Staging Area
Repository
```
