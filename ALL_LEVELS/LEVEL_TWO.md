
## Table of Contents

- [Level 2: Ramping Up](#level-2-ramping-up)
  - [2.1 Detach yo' HEAD](#21-detach-yo-head)
  - [2.2 Relative Refs (^)](#22-relative-refs-)
  - [2.3 Relative Refs #2 (~)](#23-relative-refs-2-)
  - [2.4 Reversing Changes in Git](#24-reversing-changes-in-git)

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
  - 

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

