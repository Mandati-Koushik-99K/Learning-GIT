## Table of Contents

- [Level 3: Moving Work Around](#level-3-moving-work-around)
  - [3.1 Cherry-pick Intro](#31-cherry-pick-intro)
  - [3.2 Interactive Rebase Intro](#32-interactive-rebase-intro)

---

## Level 3: Moving Work Around

### 3.1 Cherry-pick Intro

#### 📋 Problem Statement
Use `git cherry-pick` to copy specific commits from different branches and place them below your current location (HEAD). Cherry-pick commits C3, C4, and C7 to the main branch.

**Challenge**: Git cherry-pick is followed by commit names! You need to select specific commits from different branches and apply them to main.

#### 💡 Solution Approach
Cherry-picking allows you to copy individual commits from anywhere in the repository and apply them to your current branch. Instead of merging entire branches, I selectively picked commits C3, C4, and C7 to bring their changes to the main branch.

The command used: `git cherry-pick c3 c4 c7`

This creates new commits (C3', C4', C7') on main with the same changes but different commit hashes.

#### ⚙️ Commands Used

| Command | Purpose |
|---------|---------|
| `git cherry-pick c3 c4 c7` | Copy commits C3, C4, and C7 to current branch (main) |

**Command Breakdown:**
- `git cherry-pick` - The cherry-pick command
- `c3 c4 c7` - Space-separated list of commits to copy
- Can also use: `git cherry-pick c3` then `git cherry-pick c4` then `git cherry-pick c7`

#### 📸 Screenshot

<img width="1915" height="948" alt="Lv3-1" src="https://github.com/user-attachments/assets/4a0b45b9-ca3a-457c-ba70-3ede73d59cd2" />


*Screenshot showing commits C3, C4, and C7 cherry-picked from different branches (bugFix, side, another) onto main branch, creating new commits C2, C4, C6, C3', C4', C7' in the goal state*

#### 📝 Explanation & Learning

- **What I learned**:
  - `git cherry-pick` copies specific commits to your current branch
  - It creates NEW commits with different hashes but same changes
  - You can pick commits from any branch, in any order
  - Multiple commits can be cherry-picked in a single command
  - The commits are applied in the order you specify
  - Original commits remain on their original branches

- **Key Concepts**:
  - **Cherry-picking**: Selectively copying commits from one branch to another
  - **New Commits Created**: Cherry-picked commits get new hashes (shown as C3', C4', C7')
  - **Non-destructive**: Original commits remain unchanged on source branches
  - **Order Matters**: Commits are applied in the order specified in the command

- **Syntax Variations**:
  ```bash
  # Single commit
  git cherry-pick c3
  
  # Multiple commits (space-separated)
  git cherry-pick c3 c4 c7
  
  # Range of commits
  git cherry-pick c3..c7
  
  # Using branch names
  git cherry-pick bugFix
  
  # Using relative refs
  git cherry-pick HEAD~2
  ```

- **Real-World Scenario**:
  ```bash
  # Bug fixed on develop branch, need it in production
  git checkout production
  git cherry-pick abc123f  # Cherry-pick the bug fix commit
  git push
  
  # Want specific features from feature branch
  git checkout main
  git cherry-pick feature~3 feature~1  # Pick specific commits
  ```

- **When to Use Cherry-pick**:
  ✅ **Do use when:**
  - You need specific commits, not entire branch
  - Applying hotfixes to multiple branches
  - Fixing commit order or organization
  - Backporting features to older versions
  
  ❌ **Don't use when:**
  - You want all changes from a branch (use merge/rebase instead)
  - Commits have dependencies on other commits you're not picking
  - Working with a large number of commits (merge is cleaner)

- **Cherry-pick vs Other Commands**:
  | Command | Purpose | Use Case |
  |---------|---------|----------|
  | `cherry-pick` | Copy specific commits | Select individual changes |
  | `merge` | Combine entire branches | Integrate all branch work |
  | `rebase` | Reapply commits on new base | Clean linear history |

- **Important Notes**:
  - Cherry-picked commits have NEW hashes (they're copies, not moves)
  - Original commits stay on their original branches
  - Can cause merge conflicts if changes overlap
  - Creates duplicate commits in repository history
  - Use sparingly in collaborative environments
    
---

### 3.2 Interactive Rebase Intro

#### 📋 Problem Statement
Use interactive rebase (`git rebase -i`) to reorder, omit, or modify commits interactively. Clean up the commit history by selecting which commits to keep and in what order.

**Challenge**: You can use either branches or relative refs (HEAD~) to specify the rebase target. Interactive rebase lets you choose which commits to include.

#### 💡 Solution Approach
Interactive rebase opens an editor where you can manipulate commits before replaying them. The command `git rebase -i HEAD~4` opens an interactive dialog showing the last 4 commits, allowing me to:
- Reorder commits by dragging
- Omit commits by clicking "Drop/Omit"
- Pick commits to include
- Edit commit messages

In this level, I needed to rebase the last 4 commits and selectively include/exclude certain commits to reach the goal state.

#### ⚙️ Commands Used

| Command | Purpose |
|---------|---------|
| `git rebase -i HEAD~4` | Start interactive rebase for last 4 commits |

**Interactive Rebase Options:**
- `pick` (or `p`) - Keep the commit
- `drop` (or `d`) - Remove the commit
- `reword` (or `r`) - Keep commit but edit message
- `edit` (or `e`) - Keep commit and pause to make changes
- `squash` (or `s`) - Combine with previous commit
- `fixup` (or `f`) - Like squash but discard commit message

#### 📸 Screenshots

<img width="1910" height="940" alt="Lv3-2" src="https://github.com/user-attachments/assets/7239e716-e8b2-4ec6-8346-5aa8349c216f" />


*Screenshot showing the interactive rebase dialog with 4 commits (C2, C3, C5, C4) where you can pick/omit commits and reorder them*

<img width="1919" height="948" alt="Lv3-2 1" src="https://github.com/user-attachments/assets/bc0feaab-5022-4f7f-bdbc-e1f29b086e07" />


*Screenshot showing the final result after interactive rebase with the cleaned-up commit history*

#### 📝 Explanation & Learning

- **What I learned**:
  - Interactive rebase (`-i` flag) gives fine-grained control over commit history
  - Can reorder commits by changing their order in the editor
  - Can omit commits completely (they disappear from history)
  - Can combine, split, or edit commits
  - Rewrites commit history with new hashes
  - Much more powerful than regular rebase

- **Key Concepts**:
  - **Interactive Mode**: Provides a menu to manipulate commits before applying
  - **HEAD~4**: Rebase starting from 4 commits before HEAD
  - **Commit Reordering**: Change the sequence of commits
  - **Commit Omission**: Remove commits from history entirely
  - **History Rewriting**: Creates new commits with new hashes

- **Visual Understanding from Screenshots**:
  
  **Screenshot 1 (Dialog)**:
  - Shows "Rebasing 4 Commits" dialog
  - Lists commits: C2, C3, C5, C4
  - Each has "Click to Drop/Omit" option (shown in pink/magenta)
  - Can drag and drop to reorder
  - "Cancel" to abort, "Confirm" to apply
  - Right side shows current state: overHere branch at C1
  
  **Screenshot 2 (Result)**:
  - Shows linear history after rebase
  - Main branch now at C5 with overHere at C1
  - Clean, linear commit history: C0 → C1 → C2 → C3 → C4 → C5
  - All commits in sequential order

- **How Interactive Rebase Works**:
  ```
  1. Git pauses before applying commits
  2. Opens editor with commit list
  3. You edit the list:
     - Change order (reorder lines)
     - Remove commits (delete lines or use 'drop')
     - Change action (pick, squash, edit, etc.)
  4. Save and close editor
  5. Git replays commits according to your instructions
  ```

- **Interactive Rebase Actions Explained**:

  | Action | Effect | When to Use |
  |--------|--------|-------------|
  | **pick** | Keep commit as-is | Default, keep commit |
  | **drop** | Remove commit completely | Remove unwanted commits |
  | **reword** | Keep commit, change message | Fix typos in messages |
  | **edit** | Pause to modify commit | Split commits or fix content |
  | **squash** | Combine with previous, keep both messages | Merge related commits |
  | **fixup** | Combine with previous, discard this message | Clean up WIP commits |

- **Step-by-Step Example**:
  ```bash
  # Start interactive rebase
  $ git rebase -i HEAD~3
  
  # Editor opens with:
  pick a1b2c3 Add login feature
  pick d4e5f6 Fix bug in login  
  pick g7h8i9 Update tests
  
  # Change to clean it up:
  pick a1b2c3 Add login feature
  fixup d4e5f6 Fix bug in login    # Merge fix into feature
  pick g7h8i9 Update tests
  
  # Save and exit
  # Git replays commits, combining the bug fix with feature
  ```

- **Safety and Best Practices**:

  ✅ **Do:**
  - Use on LOCAL commits only (not pushed)
  - Review changes carefully in the dialog
  - Test after rebasing
  - Keep backups of important branches
  - Use `--abort` if something goes wrong

  ❌ **Don't:**
  - Rebase commits that others have pulled
  - Rebase without understanding what you're changing
  - Use on public/shared branches
  - Forget to test after rewriting history

- **Handling Issues**:
  ```bash
  # Something went wrong during rebase
  git rebase --abort           # Cancel and return to original state
  
  # Need to pause and fix something
  git rebase --edit-todo       # Reopen the editor to change plan
  
  # Ready to continue after resolving conflicts
  git rebase --continue        # Proceed with rebase
  
  # Skip a problematic commit
  git rebase --skip            # Skip current commit
  ```

- **Interactive Rebase vs Regular Rebase**:

  | Feature | Regular Rebase | Interactive Rebase |
  |---------|---------------|-------------------|
  | **Command** | `git rebase main` | `git rebase -i main` |
  | **Control** | Automatic | Manual, step-by-step |
  | **Reorder** | No | Yes |
  | **Omit** | No | Yes |
  | **Squash** | No | Yes |
  | **Edit Messages** | No | Yes |
  | **Use Case** | Move branch base | Clean up history |

- **Real-World Scenario**:
  ```bash
  # You have messy feature branch with 10 commits
  git checkout feature-branch
  git log --oneline  # See all commits
  
  # Clean up before merging to main
  git rebase -i main
  
  # In editor:
  # - Squash all "WIP" commits
  # - Reorder so tests come after features
  # - Drop commits with console.log debugging
  # - Reword messages for clarity
  
  # Result: Clean 3-4 commits ready for merge
  git checkout main
  git merge feature-branch  # Clean history!
  ```
  
- **The Golden Rule of Interactive Rebase**:
  > **Never rebase commits that have been pushed to a shared repository!** 
  > Interactive rebase rewrites history. If others have based work on your commits, rewriting will cause major conflicts and confusion.

---

## Level 3 Summary

### Key Concepts Mastered

1. **Cherry-picking**
   - Copy specific commits from any branch
   - Creates new commits with same changes, different hashes
   - Non-destructive to original commits
   - Apply commits in any order

2. **Interactive Rebase**
   - Full control over commit history
   - Reorder, omit, combine, or edit commits
   - Clean up messy development history
   - Powerful but requires caution

### Commands Learned

| Command | Description | Use Case |
|---------|-------------|----------|
| `git cherry-pick <commits>` | Copy specific commits to current branch | Selective commit application |
| `git cherry-pick c3 c4 c7` | Cherry-pick multiple commits | Apply several specific commits |
| `git rebase -i HEAD~N` | Interactive rebase last N commits | Clean up commit history |
| `git rebase -i <branch>` | Interactive rebase onto branch | Reorganize before merging |

### Interactive Rebase Actions Reference

| Action | Shortcut | Effect |
|--------|----------|--------|
| pick | p | Use commit as-is |
| drop | d | Remove commit |
| reword | r | Change commit message |
| edit | e | Stop to amend commit |
| squash | s | Combine with previous, keep messages |
| fixup | f | Combine with previous, discard message |

### Best Practices Learned

✅ **Do:**
- Cherry-pick for specific commits across branches
- Use interactive rebase to clean LOCAL history
- Test thoroughly after rewriting history
- Create backup branches before complex rebases
- Read the interactive rebase instructions carefully

❌ **Don't:**
- Cherry-pick when you need entire branch (use merge)
- Interactive rebase pushed/shared commits
- Cherry-pick commits with unmet dependencies
- Forget to handle conflicts properly
- Rebase without understanding the impact

### Decision Tree: Cherry-pick vs Merge vs Rebase

```
Need changes from another branch?
│
├─ Need SPECIFIC commits only?
│  └─ Use git cherry-pick ✓
│
├─ Need ALL changes from branch?
│  │
│  ├─ Want to preserve branching history?
│  │  └─ Use git merge ✓
│  │
│  └─ Want linear history?
│     └─ Use git rebase ✓
│
└─ Need to clean up LOCAL commits?
   └─ Use git rebase -i ✓
```

### Common Workflows

**Workflow 1: Applying Hotfix to Multiple Branches**
```bash
# Fix found on develop, need on main and release
git checkout develop
# Make fix, commit it (gets hash abc123)

git checkout main
git cherry-pick abc123

git checkout release-1.0
git cherry-pick abc123
```

**Workflow 2: Cleaning Feature Branch Before Merge**
```bash
git checkout feature-branch
git rebase -i main

# In editor:
# - Squash WIP commits
# - Drop debug commits  
# - Reorder logically

git checkout main
git merge feature-branch  # Clean history
```

**Workflow 3: Backporting Features**
```bash
# Feature in version 2.0, need in 1.5
git checkout release-1.5
git cherry-pick feature-commit-1
git cherry-pick feature-commit-2
git push
```

### Safety Checklist

Before Cherry-picking:
- [ ] Understand what changes the commit includes
- [ ] Check for dependencies on other commits
- [ ] Prepared to handle potential conflicts
- [ ] Know the target branch is correct

Before Interactive Rebase:
- [ ] Commits are LOCAL only (not pushed)
- [ ] Created backup branch
- [ ] Understand what changes will happen
- [ ] Know how to abort if needed
- [ ] Tested branch after rebase

### Troubleshooting Guide

**Cherry-pick Conflicts:**
```bash
git cherry-pick abc123
# Conflict occurs
# Fix conflicts in files
git add <resolved-files>
git cherry-pick --continue
# Or abort: git cherry-pick --abort
```

**Interactive Rebase Issues:**
```bash
# Made a mistake
git rebase --abort  # Start over

# Conflicts during rebase
# Resolve conflicts
git add <files>
git rebase --continue

# Want to change the plan
git rebase --edit-todo
```

---
