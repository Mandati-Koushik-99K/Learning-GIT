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

## Level 2: Ramping Up

### 2.1 Detach yo' HEAD

#### 📋 Problem Statement
Checkout a specific commit by its hash to detach HEAD from branches. Move HEAD to commit C4 to understand detached HEAD state.

**Challenge**: Use the commit hash/label to checkout directly to a commit instead of a branch.

#### 💡 Solution Approach
I needed to checkout a specific commit (C4) directly using its hash/label rather than a branch name. This detaches HEAD from any branch and points it directly to the commit. The command `git checkout c4` was used to accomplish this.

#### ⚙️ Commands Used

| Command | Purpose |
|---------|---------|
| `git checkout c4` | Checkout commit C4 directly, detaching HEAD from branches |
| `git checkout bugFix` | (Alternative shown) Checkout the bugFix branch |

**Note**: In the screenshots, the final command shown is `git checkout c4` to reach the goal state.

#### 📸 Screenshot

<img width="1914" height="948" alt="Lv2-1" src="https://github.com/user-attachments/assets/aaeb2299-47e8-4a63-aafd-1d35e09db001" />


*Screenshot showing HEAD detached and pointing directly to commit C4, independent of any branch*

#### 📝 Explanation & Learning

- **What I learned**:
  - HEAD normally points to a branch, which then points to a commit
  - When you checkout a specific commit hash, HEAD "detaches" and points directly to that commit
  - Detached HEAD state means you're not on any branch
  - New commits made in detached HEAD state won't belong to any branch unless you create one
  - Commit hashes/labels (like C4) can be used to reference specific commits

- **Key Concepts**:
  - **HEAD**: A special pointer that indicates your current position in the Git history
  - **Detached HEAD**: HEAD points directly to a commit instead of a branch
  - **Commit Hash**: Unique identifier for each commit (can be shortened to first few characters)
  - Branches are just pointers to commits; HEAD points to the current location

- **Visual Understanding**:
  - Left side (blue): Shows the initial state with HEAD on bugFix branch
  - Right side (pink/goal): Shows HEAD detached and pointing to C4
  - The bugFix branch remains at C4, but HEAD is independent

- **Practical Application**:
  - Useful for exploring old versions of code without affecting branches
  - Good for testing/debugging historical states
  - Can create a new branch from detached HEAD: `git branch new-branch-name`
  - Use `git checkout main` to reattach HEAD to a branch

- **Warning**: 
  - Commits made in detached HEAD state can be lost if you switch branches without saving them
  - Always create a branch if you want to keep work done in detached HEAD state

---

### 2.2 Relative Refs (^)

#### 📋 Problem Statement
Use relative references to move around the commit tree. Use the caret (^) operator to move HEAD to the parent of the current commit.

**Challenge**: Remember the caret (^) operator! Use relative references instead of commit hashes.

#### 💡 Solution Approach
Instead of using commit hashes, I used relative references with the `^` operator. The command `git checkout HEAD^` moves HEAD to the parent commit of wherever HEAD currently points. This is more flexible than using specific commit hashes.

#### ⚙️ Commands Used

| Command | Purpose |
|---------|---------|
| `git checkout c4` | First, checkout to commit C4 (as in previous level) |
| `git checkout HEAD^` | Move HEAD to the parent of current position (from C4 to C3) |

**Alternative commands that could work:**
- `git checkout main^` - Move to parent of main branch
- `git checkout bugFix^` - Move to parent of bugFix branch

#### 📸 Screenshot

<img width="1915" height="943" alt="Lv2-2" src="https://github.com/user-attachments/assets/a2047bf7-b140-481c-9e20-4f4a65e08941" />


*Screenshot showing HEAD moved to C3 (parent of C4) using the caret operator*

#### 📝 Explanation & Learning

- **What I learned**:
  - The `^` (caret) operator means "parent of"
  - `HEAD^` means "the parent of HEAD"
  - You can chain operators: `HEAD^^` means grandparent (two commits back)
  - `main^` means "the parent of the main branch's commit"
  - Relative refs are more flexible than absolute commit hashes

- **Key Concepts**:
  - **Relative References**: Navigate the commit tree relative to a known position
  - **Caret Operator (^)**: Moves to the parent commit
  - **HEAD^**: Parent of current commit
  - **branch^**: Parent of the commit that branch points to
  - Can be chained: `HEAD^^^` moves back 3 commits

- **Syntax Examples**:
  ```
  HEAD^     → Parent of HEAD
  HEAD^^    → Grandparent of HEAD  
  main^     → Parent of main branch
  bugFix^   → Parent of bugFix branch
  ```

- **Visual Understanding**:
  - Left side: HEAD at C4 (after detaching from bugFix)
  - Right side: HEAD moved to C3 using `HEAD^` operator
  - The ^ operator traveled UP the commit tree (to older commit)

- **Practical Application**:
  - Useful when you don't know exact commit hashes
  - Makes scripts more portable (don't need to hardcode hashes)
  - Quick navigation through commit history
  - Essential for complex Git operations

- **Comparison with Absolute References**:
  | Absolute | Relative |
  |----------|----------|
  | `git checkout c3` | `git checkout HEAD^` |
  | Requires knowing hash | Works from current position |
  | Less flexible | More flexible |

---

### 2.3 Relative Refs #2 (~)

#### 📋 Problem Statement
Use the tilde (~) operator to move multiple commits at once. Move HEAD up the commit tree and create a branch at that location.

**Challenge**: You'll need to use at least one direct reference (hash) to complete this level. Use `git checkout HEAD^` and `git branch -f bugFix c0`.

#### 💡 Solution Approach
This level introduces the `~` operator for moving multiple commits at once and the `git branch -f` command to forcefully move a branch pointer. I used:
1. `git checkout HEAD^` to move HEAD up one commit
2. `git branch -f bugFix c0` to force-move the bugFix branch to commit C0

#### ⚙️ Commands Used

| Command | Purpose |
|---------|---------|
| `git checkout HEAD^` | Move HEAD to parent commit (from C1 to C0) |
| `git branch -f bugFix c0` | Force move bugFix branch to point to commit C0 |
| `git branch -f main c6` | (Alternative) Force move main branch to commit C6 |

**Tilde operator examples:**
- `HEAD~1` = `HEAD^` (one commit back)
- `HEAD~2` = `HEAD^^` (two commits back)
- `HEAD~3` = `HEAD^^^` (three commits back)

#### 📸 Screenshot

<img width="1912" height="954" alt="Lv-2-3" src="https://github.com/user-attachments/assets/9f6fe60b-f32a-4e68-a0d7-ac84177433b8" />


*Screenshot showing bugFix branch force-moved to C0 and HEAD detached at commit above bugFix*

#### 📝 Explanation & Learning

- **What I learned**:
  - The `~` (tilde) operator is used to move multiple commits at once
  - `~` is followed by a number: `HEAD~3` moves back 3 commits
  - `git branch -f <branch> <location>` forcefully moves a branch to a specific commit
  - `-f` flag stands for "force" - use with caution!
  - Can combine relative and absolute references

- **Key Concepts**:
  - **Tilde Operator (~)**: Moves back multiple commits efficiently
  - **Branch Force Move**: `git branch -f` reassigns where a branch points
  - **Difference between ^ and ~**:
    - `^` is for single parent moves (can specify which parent in merges)
    - `~` is for moving back multiple generations (cleaner for linear history)

- **Operator Comparison**:
  | Operator | Usage | Example | Meaning |
  |----------|-------|---------|---------|
  | `^` | Single parent | `HEAD^` | Parent of HEAD |
  | `^^` | Chained | `HEAD^^` | Grandparent of HEAD |
  | `~1` | Number | `HEAD~1` | One commit back |
  | `~3` | Number | `HEAD~3` | Three commits back |

- **Examples**:
  ```bash
  git checkout HEAD~2    # Move 2 commits back
  git checkout main~3    # Go to 3 commits before main
  git branch -f main HEAD~3  # Move main branch back 3 commits
  ```

- **Visual Understanding**:
  - Complex commit tree shown with main at C6 (goal state)
  - bugFix needs to be at C0 (root commit)
  - HEAD needs to be positioned correctly
  - Force-moving branches allows repositioning without checking out

- **The Power of git branch -f**:
  - Moves branch pointers without checking them out
  - Syntax: `git branch -f <branch> <target-commit>`
  - Useful for reorganizing branches
  - **Warning**: Dangerous on shared/public branches!

- **Practical Application**:
  - Moving branches to specific commits for testing
  - Resetting feature branches to earlier states
  - Cleaning up branch structure
  - Useful in scripts and automation

- **Safety Note**:
  - `git branch -f` rewrites branch pointers
  - Only use on local, personal branches
  - Never force-move branches others are using
  - Alternative: Use `git reset` when on the branch

---

### 2.4 Reversing Changes in Git

#### 📋 Problem Statement
Learn how to reverse changes in Git using two methods: `git reset` and `git revert`. Undo changes on both local and remote branches.

**Challenge**: Use `git reset` for local changes and `git revert` for shared/remote changes.

#### 💡 Solution Approach
Git provides two ways to undo changes:
1. `git reset` - Moves branch backward to an older commit (good for local changes)
2. `git revert` - Creates a NEW commit that undoes changes (good for shared/remote branches)

For this level:
- Use `git checkout pushed` to switch to the pushed branch
- Use `git revert c2` to create a new commit that undoes C2
- Use `git branch -f local c1` to reset local branch to C1

#### ⚙️ Commands Used

| Command | Purpose |
|---------|---------|
| `git checkout pushed` | Switch to the pushed branch (represents remote branch) |
| `git revert c2` | Create new commit that reverses changes from C2 |
| `git branch -f local c1` | Reset local branch to point to commit C1 |

**Alternative approaches:**
```bash
# Could also do:
git checkout local
git reset HEAD^         # Reset local branch back one commit

git checkout pushed  
git revert HEAD         # Revert the latest commit
```

#### 📸 Screenshot

<img width="1911" height="947" alt="Lv2-4" src="https://github.com/user-attachments/assets/292a763d-403c-4276-a54f-f3b1305daf8b" />


*Screenshot showing local branch reset to C1 and pushed branch with new revert commit C2'*

#### 📝 Explanation & Learning

- **What I learned**:
  - Two fundamentally different ways to undo changes in Git
  - `git reset` rewrites history by moving branch pointer backward
  - `git revert` preserves history by creating a new "undo" commit
  - Choice depends on whether changes have been shared with others
  - Remote/shared branches should use `revert`, not `reset`

- **Key Concepts**:

  **Git Reset**:
  - Moves the branch pointer to an earlier commit
  - Erases commits from history (they still exist but become unreachable)
  - Used for LOCAL changes only
  - Syntax: `git reset <commit>`
  - **Danger**: Never reset shared branches!

  **Git Revert**:
  - Creates a NEW commit that undoes changes from a previous commit
  - Preserves history - shows both original change and the undo
  - Safe for PUBLIC/SHARED branches
  - Syntax: `git revert <commit>`
  - The new commit is often shown as C2' in diagrams

- **Comparison Table**:

  | Aspect | git reset | git revert |
  |--------|-----------|------------|
  | **History** | Erases commits | Adds new commit |
  | **Use case** | Local changes | Shared/remote changes |
  | **Safety** | Destructive | Non-destructive |
  | **Result** | Branch moves backward | New "undo" commit created |
  | **Collaboration** | Causes problems | Safe for teams |

- **Visual Understanding**:
  - **Local branch**: Shows reset from C2 back to C1 (C2 disappears)
  - **Pushed branch**: Shows C2' added that reverses C2 (C2 remains in history)
  - Orange color indicates "undone" or reset state
  - Both achieve same end result but different methods

- **When to Use Each**:

  **Use git reset when:**
  - Changes are only local (not pushed)
  - You want to "undo" commits completely
  - Working on a personal feature branch
  - Example: `git reset HEAD~1` (undo last commit locally)

  **Use git revert when:**
  - Changes have been pushed to remote
  - Others might have pulled your changes
  - Working on shared/public branches
  - You want to keep history of the mistake
  - Example: `git revert HEAD` (undo last commit safely)

- **Real-World Scenario**:
  ```bash
  # Oops, committed a bug to local branch
  git reset HEAD~1        # ✓ Safe - not pushed yet
  
  # Oops, committed a bug and already pushed
  git revert HEAD         # ✓ Safe - creates undo commit
  git push                # Share the fix
  
  # DON'T DO THIS:
  git reset HEAD~1        # ✗ Danger if already pushed!
  git push -f             # ✗ This breaks others' repos!
  ```

- **Reset Modes** (Advanced):
  - `git reset --soft`: Move HEAD, keep changes staged
  - `git reset --mixed`: Move HEAD, unstage changes (default)
  - `git reset --hard`: Move HEAD, discard all changes (destructive!)

- **Practical Application**:
  - Fixing mistakes in local work: use `reset`
  - Undoing published changes: use `revert`
  - Team collaboration: always `revert` on shared branches
  - Personal experimentation: `reset` is fine

- **Memory Aid**:
  - **Reset** = **Rewind** (go back in time, erase history)
  - **Revert** = **Reverse** (add a new opposite commit, keep history)

- **Important Safety Rule**:
  > **Golden Rule**: If commits have been pushed and others might have pulled them, ALWAYS use `git revert`, NEVER use `git reset`!

---

## Level 2 Summary

### Key Concepts Mastered

1. **Detached HEAD State**
   - HEAD can point directly to commits
   - Useful for exploring history without affecting branches

2. **Relative References**
   - `^` operator for parent commits
   - `~` operator for moving multiple commits
   - More flexible than absolute hashes

3. **Branch Manipulation**
   - `git branch -f` to force-move branches
   - Powerful but use carefully on local branches only

4. **Reversing Changes**
   - `git reset` for local changes (destructive)
   - `git revert` for shared changes (safe)
   - Choose based on whether changes are published

### Commands Learned

| Command | Description | Use Case |
|---------|-------------|----------|
| `git checkout <hash>` | Detach HEAD to specific commit | Explore history |
| `git checkout HEAD^` | Move to parent commit | Navigate relatively |
| `git checkout HEAD~3` | Move back 3 commits | Navigate efficiently |
| `git branch -f <branch> <commit>` | Force move branch | Reorganize branches |
| `git reset <commit>` | Move branch backward | Undo local changes |
| `git revert <commit>` | Create undo commit | Undo shared changes |

### Best Practices Learned

✅ **Do:**
- Use detached HEAD to explore old commits safely
- Use relative references for flexibility
- Use `git revert` on shared/public branches
- Use `git reset` on local, unpushed commits

❌ **Don't:**
- Make commits in detached HEAD without creating a branch
- Force-move branches that others are using
- Reset commits that have been pushed to shared repos
- Revert when a simple reset would suffice (on local work)

### Git Workflow Decision Tree

```
Need to undo changes?
│
├─ Changes only local (not pushed)?
│  └─ Use git reset ✓
│
└─ Changes pushed/shared with others?
   └─ Use git revert ✓
```

---

*Level 2 completed! Ready for Level 3: Moving Work Around*

## Level 3: Moving Work Around

### 3.1 [Level Name]

[Same format as above]

---

## Level 4: A Mixed Bag

### 4.1 [Level Name]

[Same format as above]

---

## Level 5: Advanced Topics

### 5.1 [Level Name]

[Same format as above]

---

## Summary & Key Takeaways

### Commands Master List

| Command | Description | When to Use |
|---------|-------------|-------------|
| `git commit` | Save changes to repository | After staging files |
| `git branch <name>` | Create new branch | Starting new feature |
| `git checkout <branch>` | Switch branches | Moving between features |
| `git checkout -b <name>` | Create and switch | Quick branch creation |
| `git merge <branch>` | Merge branches | Combining work |
| `git rebase <base>` | Reapply commits | Cleaning history |

### Best Practices Learned

1. ✅ **Use branches** for all new features and bug fixes
2. ✅ **Commit frequently** with clear, descriptive messages
3. ✅ **Merge** for combining shared work (preserves history)
4. ✅ **Rebase** for cleaning up local commits before sharing
5. ⚠️ **Never rebase** public/shared branches
6. ✅ **Pull before push** to avoid conflicts

### Git Workflow Summary

```
1. Create branch:     git checkout -b feature-name
2. Make changes:      [edit files]
3. Stage changes:     git add .
4. Commit:            git commit -m "Description"
5. Push to remote:    git push origin feature-name
6. Merge/PR:          [via GitHub or git merge]
```

---

## Resources & References

- [Learn Git Branching](https://learngitbranching.js.org/) - Interactive tutorial
- [Git Documentation](https://git-scm.com/doc) - Official docs
- [GitHub Guides](https://guides.github.com/) - GitHub tutorials
- [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials) - Comprehensive guides

---

## Progress Tracker

- [x] Level 1: Introduction Sequence (4/4 completed)
  - [x] 1.1 Introduction to Git Commits
  - [x] 1.2 Branching in Git
  - [x] 1.3 Merging in Git
  - [x] 1.4 Rebase Introduction
- [ ] Level 2: Ramping Up (0/X completed)
- [ ] Level 3: Moving Work Around (0/X completed)
- [ ] Level 4: A Mixed Bag (0/X completed)
- [ ] Level 5: Advanced Topics (0/X completed)

---

## Contact & Feedback

**Repository**: [https://github.com/Mandati-Koushik-99K/Learning-GIT](https://github.com/Mandati-Koushik-99K/Learning-GIT)

---

*Last Updated: December 22, 2025*
