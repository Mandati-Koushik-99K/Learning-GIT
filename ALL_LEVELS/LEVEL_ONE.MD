# Learning Git - Complete Documentation

## Student Details

- **Name**: [Your Name]
- **Faculty**: [Faculty Name]
- **Course**: [Course Name]
- **Academic Year**: [Year]

---

## Project Overview

This repository contains comprehensive documentation of my Git learning journey through the "Learn Git Branching" interactive tutorial. Each level demonstrates understanding of Git concepts through problem-solving, command execution, and visual explanations.

---

## Table of Contents

- [Level 1: Introduction Sequence](#level-1-introduction-sequence)
  - [1.1 Introduction to Git Commits](#11-introduction-to-git-commits)
  - [1.2 Branching in Git](#12-branching-in-git)
  - [1.3 Merging in Git](#13-merging-in-git)
  - [1.4 Rebase Introduction](#14-rebase-introduction)
- [Level 2: Ramping Up](#level-2-ramping-up)
- [Level 3: Moving Work Around](#level-3-moving-work-around)
- [Level 4: A Mixed Bag](#level-4-a-mixed-bag)
- [Level 5: Advanced Topics](#level-5-advanced-topics)

---

## Level 1: Introduction Sequence

### 1.1 Introduction to Git Commits

#### 📋 Problem Statement
Make two commits on the current branch to reach the goal.

#### 📸 Screenshot

<img width="1890" height="934" alt="Lv1-1" src="https://github.com/user-attachments/assets/a98ddd5d-6e3a-49eb-bbb1-5fceb4ecf769" />

*Screenshot showing two successful git commits*

**Challenge**: Just type `git commit` twice to finish!

#### 💡 Solution Approach
Use `git commit` twice. Each commit saves the current staged changes and advances the branch pointer.

#### ⚙️ Commands Used

| Command | Purpose |
|---------|---------|
| `git commit` | Create first commit (saves current state) |
| `git commit` | Create second commit (advances branch further) |


#### 📝 Explanation & Learning

- **What I learned**:
  - `git commit` writes staged changes to the repository as a new snapshot
  - Each commit has a parent (the previous commit)
  - Creating two commits advances the branch two steps ahead
  - Commits create a history chain that can be traversed

- **Key Concepts**:
  - Commits are snapshots of your project at specific points in time
  - Each commit gets a unique SHA hash identifier
  - The commit history forms a directed acyclic graph (DAG)

---

### 1.2 Branching in Git

#### 📋 Problem Statement
Create a new branch and switch (check out) to it.

#### 📸 Screenshot

<img width="1911" height="929" alt="Lv1-2" src="https://github.com/user-attachments/assets/ec93c039-abf0-4251-bd76-1c85091aa10c" />

*Screenshot showing branch creation and checkout*

**Challenge**: Make a new branch with `git branch <name>` and check it out with `git checkout <name>`

#### 💡 Solution Approach
First create the branch `bugFix`, then switch to it so HEAD points to the new branch.

#### ⚙️ Commands Used

| Command | Purpose |
|---------|---------|
| `git branch bugFix` | Create a new branch named `bugFix` (pointer to current commit) |
| `git checkout bugFix` | Switch to branch `bugFix` (move HEAD to that branch) |

**Alternative**: `git checkout -b bugFix` (creates and switches in one command)

#### 📝 Explanation & Learning

- **What I learned**:
  - `git branch <name>` creates a new branch reference pointing at the current commit
  - It does NOT automatically switch to the new branch
  - `git checkout <branch>` moves HEAD to the named branch
  - After checkout, new commits will be recorded on the current branch

- **Key Concepts**:
  - Branches are lightweight pointers to commits
  - HEAD is a pointer to the current branch/commit
  - Branching allows parallel development without affecting main code

---

### 1.3 Merging in Git

#### 📋 Problem Statement
Create a `bugFix` branch, commit on it, return to main, commit there, then merge the `bugFix` branch into main.

#### 📸 Screenshot

<img width="1913" height="943" alt="Lv1-3" src="https://github.com/user-attachments/assets/bdadafdd-8347-4eb7-be08-e4f27e1cdaf5" />

*Screenshot showing the merge operation and resulting commit graph*

**Challenge**: Complete commits in the specified order (bugFix before main)

#### 💡 Solution Approach
1. Create and switch to `bugFix`
2. Make a commit on `bugFix` (creates c2)
3. Switch back to `main`
4. Make a commit on `main` (creates c3)
5. Merge `bugFix` into `main`

#### ⚙️ Commands Used

| Command | Purpose |
|---------|---------|
| `git branch bugFix` | Create branch bugFix |
| `git checkout bugFix` | Switch to bugFix |
| `git commit` | Commit changes on bugFix (creates commit c2) |
| `git checkout main` | Switch back to main |
| `git commit` | Commit changes on main (creates commit c3) |
| `git merge bugFix` | Merge the bugFix branch into main |


#### 📝 Explanation & Learning

- **What I learned**:
  - `git merge <branch>` combines changes from the specified branch into current branch
  - When branches diverge, Git creates a **merge commit** with two parents
  - The merge commit joins the two branches in the history
  - Order matters: doing bugFix commit first, then main, ensures proper merge

- **Key Concepts**:
  - Merge commits have two parent commits
  - Merging preserves the complete history of both branches
  - The resulting graph shows how branches converged
  - Use `git merge c2` to merge by commit hash (less common)

---

### 1.4 Rebase Introduction

#### 📋 Problem Statement
After creating a `bugFix` branch and committing to both branches, rebase the `bugFix` branch onto main so bugFix commits appear as if they were made after the latest main commits.

#### 📸 Screenshot

<img width="1906" height="939" alt="Lv1-4" src="https://github.com/user-attachments/assets/4450c9b6-c90e-440b-b0ce-b7232bd15608" />

*Screenshot showing rebase operation creating new commit c2'*

**Challenge**: Create a linear history by rebasing

#### 💡 Solution Approach
1. Create `bugFix` and commit on it
2. Commit on `main`
3. Switch to `bugFix`
4. Run `git rebase main` to replay bugFix commits on top of main

This creates new commits (c2') with different hashes but same changes.

#### ⚙️ Commands Used

| Command | Purpose |
|---------|---------|
| `git branch bugFix` | Create the bugFix branch |
| `git checkout bugFix` | Switch to bugFix |
| `git commit` | Commit on bugFix (original commit c2) |
| `git checkout main` | Switch to main |
| `git commit` | Commit on main (creates c3) |
| `git checkout bugFix` | Go back to bugFix |
| `git rebase main` | Rebase bugFix onto tip of main (creates c2') |


#### 📝 Explanation & Learning

- **What I learned**:
  - `git rebase <base>` takes commits from current branch not in `<base>`
  - It temporarily removes them, moves branch to `<base>`, then replays commits
  - Rebase creates NEW commits with new hashes (shown as c2' in diagrams)
  - Results in a linear, cleaner history without merge commits

- **Key Concepts**:
  - Rebasing rewrites commit history
  - Original commits are replaced with new ones (different SHA hashes)
  - Use rebase for clean, linear history before merging features
  - **⚠️ Warning**: Never rebase public/shared branches - it rewrites history

- **Rebase vs Merge**:
  | Rebase | Merge |
  |--------|-------|
  | Linear history | Branching history |
  | Rewrites commits | Preserves original commits |
  | Cleaner graph | Shows actual workflow |
  | Use for local cleanup | Use for shared branches |

---
