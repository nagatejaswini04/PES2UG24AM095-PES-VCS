# PES-VCS Lab Report

## 👤 Author

**Name:** NAGA TEJASWINI
**SRN:** PES2UG24AM095

---

# 📌 Project Overview

This project implements a simplified version control system inspired by Git. It uses content-addressable storage, tree structures, and commit history to track file changes efficiently.

The system supports:

* `pes init`
* `pes add`
* `pes status`
* `pes commit`
* `pes log`

---

# ⚙️ Platform

* Ubuntu 22.04
* GCC Compiler

---

# 🧱 Phase 1: Object Storage

### ✅ Objective

Implement blob storage using SHA-256 hashing and content-addressable storage.

### ✅ Key Features

* Object write (hash + store)
* Object read (retrieve + verify)
* Deduplication

### 📸 Screenshot 1A

*Add screenshot of `./test_objects` output*

### 📸 Screenshot 1B

*Add screenshot of `.pes/objects` directory structure*

---

# 🌳 Phase 2: Tree Objects

### ✅ Objective

Build directory structure using tree objects.

### ✅ Key Features

* Tree serialization
* Nested directory handling
* Deterministic structure

### 📸 Screenshot 2A

*Add screenshot of `./test_tree` output*

### 📸 Screenshot 2B

*Add screenshot of `xxd` tree object*

---

# 📂 Phase 3: Index (Staging Area)

### ✅ Objective

Implement staging area for tracking files before commit.

### ✅ Key Features

* index_load
* index_save
* index_add

### 📸 Screenshot 3A

*Add screenshot of `pes init`, `pes add`, `pes status`*

### 📸 Screenshot 3B

*Add screenshot of `.pes/index`*

---

# 🧾 Phase 4: Commits and History

### ✅ Objective

Implement commit creation and history tracking.

### ✅ Key Features

* commit_create
* parent linking
* log traversal

### 📸 Screenshot 4A

*Add screenshot of `pes log`*

### 📸 Screenshot 4B

*Add screenshot of `.pes` structure*

### 📸 Screenshot 4C

*Add screenshot of HEAD and branch file*

---

# ✍️ Analysis Questions

## 🔹 Q5.1: Branch Checkout

A branch is a file containing a commit hash. To implement checkout:

* Update `.pes/HEAD` to point to new branch
* Read target commit and its tree
* Update working directory:

  * Remove old files
  * Add new files from tree

**Complexity:**

* Must handle file updates, deletions, and conflicts
* Requires syncing working directory, index, and repository

---

## 🔹 Q5.2: Dirty Working Directory Detection

Steps:

1. Compare working file hash with index hash
2. If different → file modified
3. Compare with target branch hash

**Conflict condition:**

* File modified locally AND differs in target branch → abort checkout

---

## 🔹 Q5.3: Detached HEAD

* HEAD points directly to a commit instead of branch
* New commits are created but not linked to any branch

**Recovery:**

* Create a new branch pointing to that commit

---

## 🔹 Q6.1: Garbage Collection

### Algorithm:

1. Start from all branch heads
2. Traverse commits, trees, and blobs
3. Mark reachable objects
4. Delete unmarked objects

### Data Structure:

* Hash set for tracking reachable objects

### Estimate:

* ~100,000 commits + associated trees/blobs
* Total objects may reach millions

---

## 🔹 Q6.2: GC Race Condition

### Problem:

* GC may delete objects while commit is in progress

### Example:

* Commit creates object
* GC runs before reference update
* Object deleted → corruption

### Solution:

* Use locks
* Delay deletion
* Ensure safe reference updates

---

# ✅ Conclusion

This project demonstrates how Git internally manages:

* File storage using hashing
* Directory structures using trees
* Version history using commits

It provides a strong understanding of filesystem concepts and version control design.

---

# 🔗 Repository Link

*Add your GitHub repo link here*

---
