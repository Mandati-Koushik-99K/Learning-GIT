## Table of Contents

- [Level 4: A Mixed Bag](#level-4-a-mixed-bag)
  - [4.1 Grabbing Just 1 Commit](#41-grabbing-just-1-commit)
  - [4.2 Juggling Commits](#42-juggling-commits)
  - [4.3 Juggling Commits #2](#43-juggling-commits-2)
  - [4.4 Git Tags](#44-git-tags)
  - [4.5 Git Describe](#45-git-describe)

---

## Level 4: A Mixed Bag

### 4.1 Grabbing Just 1 Commit

#### 📋 Problem Statement
Use your skills to grab just one commit and place it on the main branch. Cherry-pick commit C4 specifically to the main branch, even though there are multiple branches with different commits.

**Challenge**: Navigate a complex branching structure and selectively grab exactly one commit (C4) to apply to main.

#### 💡 Solution Approach
Looking at the complex tree with multiple branches (bugFix, side, another, print, debug), I needed to identify commit C4 and cherry-pick it to main. The solution involved:
1. Making sure I'm on the main branch with `git checkout main`
2. Using `git cherry-pick c4` to copy commit C4 onto main

This demonstrates cherry-picking's power to grab a single specific commit from anywhere in the repository.

#### ⚙️ Commands Used

| Command | Purpose |
|---------|---------|
| `git checkout main` | Switch to main branch (ensure we're on the target branch) |
| `git cherry-pick c4` | Copy commit C4 to the current branch (main) |

**Alternative approach:**
```bash
# Could also specify the full commit hash
git cherry-pick <full-hash-of-c4>
```

#### 📸 Screenshot

<img width="1919" height="945" alt="Lv4-1" src="https://github.com/user-attachments/assets/97f5c44a-ce3e-4e95-8a65-3d9e00f221f1" />



*Screenshot showing complex branching structure with multiple branches (bugFix at C3, side at C5, debug at C2, print at C3, another at C7) and the goal of cherry-picking C4 to main*

#### 📝 Explanation & Learning

- **What I learned**:
  - Cherry-pick is perfect for grabbing a single commit from complex branch structures
  - Can cherry-pick from any branch without needing to merge the entire branch
  - The commit maintains its changes but gets a new hash when cherry-picked
  - Don't need to know which branch the commit is on, just need the commit identifier
  - Useful in real projects when you need a specific fix but not all branch changes

- **Key Concepts**:
  - **Selective Commit Application**: Choose exactly which commits to apply
  - **Branch Independence**: Can grab commits without merging branches
  - **Commit Identification**: Using commit hashes/labels to specify exact commits
  - **Non-destructive**: Original commit remains on its branch

- **Visual Understanding**:
  - **Left side (initial state)**:
    - Main branch at C1
    - Multiple branches diverging from various points
    - C4 is on the "side" branch
    - Need to get C4's changes onto main
  
  - **Right side (goal state)**:
    - Main at C1 with a new commit C4'
    - This is a COPY of C4 (shown with turquoise/green color)
    - All other branches remain unchanged
    - Clean application of just the one needed commit

- **Complex Branch Navigation**:
  In this scenario with multiple branches:
  - bugFix branch: C2 → C3
  - side branch: C4 → C5  
  - print branch: at C3
  - debug branch: at C2
  - another branch: C6 → C7
  
  We successfully isolated and applied only C4!

- **When This Pattern Is Useful**:
  - Emergency fixes needed in production
  - Selecting specific features from a feature branch
  - Backporting fixes to older versions
  - Avoiding merge of incomplete work
  - Working with multiple release branches

- **Cherry-pick vs Full Merge**:
  | Scenario | Solution |
  |----------|----------|
  | Need 1 commit from branch | Cherry-pick |
  | Need all commits from branch | Merge |
  | Need specific commits only | Cherry-pick multiple |
  | Branch has dependencies | Consider merge instead |

---

### 4.2 Juggling Commits

#### 📋 Problem Statement
Reorder and manipulate commits using both interactive rebase and cherry-pick. The challenge involves working with commits that need to be reordered and selectively applied to create a clean history.

**Challenge**: Use a combination of `git rebase -i` and `git branch -f` to achieve the desired commit order and structure.

#### 💡 Solution Approach
This level requires juggling commits using multiple techniques:
1. Use `git rebase -i main` to enter interactive rebase mode
2. Reorder/modify commits in the interactive dialog
3. Use `git branch -f` to move branch pointers to specific locations
4. The goal is to get main pointing to a clean, reordered set of commits

The command sequence shown:
```bash
git rebase -i main         # Open interactive rebase
git branch -f main c3'     # Force move main to c3'
git rebase -i main         # Another interactive rebase
git branch -f main c1      # Move main back to c1
git rebase -i main         # Yet another rebase
git branch -f main c3''    # Final position for main
```

#### ⚙️ Commands Used

| Command | Purpose |
|---------|---------|
| `git rebase -i main` | Interactive rebase onto main (open commit editor) |
| `git branch -f main c3'` | Force move main branch pointer to commit c3' |
| `git rebase -i main` | Another interactive rebase to continue juggling |
| `git branch -f main c1` | Move main to c1 |
| `git rebase -i main` | Final interactive rebase |
| `git branch -f main c3''` | Position main at final location c3'' |

#### 📸 Screenshots

<img width="1912" height="949" alt="Lv4-2" src="https://github.com/user-attachments/assets/8a0bf9f6-8bd9-4f3a-8640-e9505b4a55e3" />


*Initial state showing branches that need to be reorganized*

<img width="1918" height="945" alt="Lv4-2 1" src="https://github.com/user-attachments/assets/3705417d-f196-49cc-83bc-ef11e7d417ba" />


*Interactive rebase dialog showing "Rebasing 2 Commits" with options to pick/drop C2'' and C3'*

<img width="1341" height="588" alt="Lv4-2 2" src="https://github.com/user-attachments/assets/b7d8004a-ce79-4781-9bff-860bf9665dc5" />


*Mid-process showing the commits being reorganized with various rebase operations*

<img width="1844" height="780" alt="Lv4-2 3" src="https://github.com/user-attachments/assets/97f0bf19-8d6b-44a2-a1ba-b8f1e1bf57b3" />


*Final clean state with main and caption branches properly positioned*

#### 📝 Explanation & Learning

- **What I learned**:
  - Interactive rebase is powerful for reordering commits
  - Can combine `git rebase -i` with `git branch -f` for complex manipulations
  - Multiple rebase operations can be chained to achieve desired structure
  - Commits can be reordered, omitted, or duplicated through this process
  - Branch pointers can be moved independently of HEAD
  - The prime notation (C3', C3'', C3''') indicates new commits created through rebasing

- **Key Concepts**:
  - **Interactive Rebase**: Fine-grained control over commit history
  - **Branch Force-Moving**: `git branch -f` moves branch pointers without checking out
  - **Commit Juggling**: Combining techniques to reorganize complex histories
  - **Multiple Iterations**: Sometimes need several passes to achieve goal
  - **Commit Recreation**: Each rebase creates new commits (new hashes)

- **Visual Understanding from Screenshots**:

  **Screenshot 1 (Initial State)**:
  - Main at C1
  - newImage branch at C2
  - caption branch with multiple commits
  - Complex branching that needs cleanup

  **Screenshot 2 (Interactive Dialog)**:
  - "Rebasing 2 Commits" dialog shown
  - Lists C2'' and C3' for manipulation
  - Can pick or drop each commit
  - This is where the reordering happens

  **Screenshot 3 (Process)**:
  - Shows intermediate state during juggling
  - newImage branch positioned
  - Multiple commit versions (C2, C2', C2'', etc.)
  - Demonstrates the step-by-step transformation

  **Screenshot 4 (Final)**:
  - Clean final structure achieved
  - Main and caption branches at correct positions
  - Excess commits cleaned up
  - Goal state matches requirements

- **The Juggling Pattern**:
  ```
  Step 1: Rebase to reorder commits
  Step 2: Force-move branch pointer  
  Step 3: Rebase again if needed
  Step 4: Force-move to final position
  Step 5: Clean up with final rebase
  ```

- **Why This Is Called "Juggling"**:
  - Multiple commits being manipulated simultaneously
  - Like juggling balls, keeping track of multiple elements
  - Commits move through different states
  - Requires coordination of multiple commands
  - End result is cleaner than start, but process is complex


- **When to Use This Pattern**:
  ✅ **Do use when:**
  - Preparing clean history for PR
  - Fixing commit order mistakes
  - Splitting or combining work
  - Creating logical commit progression
  
  ❌ **Don't use when:**
  - Commits already pushed to shared branch
  - Other developers based work on these commits
  - You're not comfortable with rebase
  - Simple merge would suffice

- **Safety Considerations**:
  - Always work on local branches
  - Create backup branch before starting
  - Understand what each command does
  - Test the result
  - Never force-push to shared branches

---

### 4.3 Juggling Commits #2

#### 📋 Problem Statement
Another commit juggling challenge using a simpler approach. Use `git rebase -i HEAD~2` to interactively rebase the last 2 commits and reorganize the commit structure.

**Challenge**: The hint says "The first command is git rebase -i HEAD~2". This suggests using relative references with interactive rebase.

#### 💡 Solution Approach
This challenge can be solved more elegantly with a single interactive rebase command. By using `git rebase -i HEAD~2`, we can open an editor showing the last 2 commits and reorder them as needed. The level tests understanding of:
- Relative references (HEAD~2)
- Interactive rebase for simple reordering
- Less complex than the previous juggling exercise

Commands used:
```bash
git rebase -i HEAD~2    # Interactive rebase last 2 commits
# In the editor, reorder the commits as needed
```

#### ⚙️ Commands Used

| Command | Purpose |
|---------|---------|
| `git rebase -i HEAD~2` | Interactive rebase of last 2 commits from current position |

**What happens:**
- Opens editor with last 2 commits
- Can reorder lines to change commit order
- Can pick/drop/squash as needed
- Simpler than multiple rebase operations

#### 📸 Screenshot

<img width="1911" height="937" alt="Lv4-3" src="https://github.com/user-attachments/assets/17213297-9e09-43f4-93d0-ea853f6506ef" />



<img width="1918" height="602" alt="Lv4-3 1" src="https://github.com/user-attachments/assets/1f63e3bc-c152-41f5-8647-a3e12fe1096d" />

*Screenshot showing simpler commit structure where HEAD~2 relative reference is used for clean reordering*

#### 📝 Explanation & Learning

- **What I learned**:
  - `HEAD~N` is powerful for referencing recent commits
  - Sometimes simpler solutions exist (one rebase vs multiple)
  - Interactive rebase with relative refs is very practical
  - The "~2" means "2 commits before HEAD"
  - This approach is much cleaner than juggling with force-moves

- **Key Concepts**:
  - **Relative References with Rebase**: Using HEAD~N for clean rebasing
  - **Simpler Approach**: One command vs complex juggling
  - **HEAD~2 Meaning**: Start from 2 commits before current HEAD
  - **Interactive Editor**: Visual way to reorganize commits

- **Visual Understanding**:
  - **Left side**: Shows initial state with newImage and caption branches
  - **Right side**: Clean final state with properly ordered commits
  - The intermediate complexity is hidden in the interactive editor
  - Much cleaner than previous juggling approach

- **HEAD~N Notation Review**:
  ```
  HEAD~1  = Parent of HEAD (1 commit back)
  HEAD~2  = Grandparent (2 commits back)
  HEAD~3  = Great-grandparent (3 commits back)
  ```

- **Why This Approach Is Better**:
  | Complex Juggling | Simple Rebase -i |
  |-----------------|------------------|
  | Multiple commands | Single command |
  | Force branch moves | Natural flow |
  | Easy to make mistakes | Clear and simple |
  | Hard to understand | Intuitive |


- **Interactive Rebase Power**:
  With one command, you can:
  - Reorder commits (change line order)
  - Squash commits (combine them)
  - Drop commits (remove from history)
  - Edit commits (modify content)
  - Reword messages (fix typos)

- **When to Use This Pattern**:
  - Quick fixes to recent commit order
  - Cleaning up last few commits before pushing
  - Squashing WIP commits
  - Much more common than complex juggling
  - Daily workflow for most developers

- **Comparison of Both Juggling Levels**:
  
  **Level 4.2 (Complex Juggling)**:
  - Multiple rebase operations
  - Branch force-moves
  - Complex scenarios
  - Teaching advanced manipulation

  **Level 4.3 (Simple Juggling)**:
  - Single rebase operation
  - Relative reference
  - Practical daily use
  - Teaching efficient workflow

---

### 4.4 Git Tags

#### 📋 Problem Statement
Learn about Git tags as permanent markers for commits. Create tags at specific commits to mark important milestones like releases or significant points in history.

**Challenge**: Create tags v0 and v1 at commits C1 and C2 respectively, then navigate using tags and checkout specific positions.

#### 💡 Solution Approach
Tags are like permanent bookmarks on specific commits. Unlike branches that move forward with new commits, tags stay forever at the commit they're created on. This level teaches:
1. Creating tags with `git tag v0 c1` and `git tag v1 c2`
2. Using tags to mark release points
3. Checking out tags or using them as references

Commands used:
```bash
git tag v0 c1         # Create tag v0 at commit C1
git tag v1 c2         # Create tag v1 at commit C2  
git checkout c5       # Checkout commit C5
git checkout HEAD^    # Move to parent of HEAD
```

#### ⚙️ Commands Used

| Command | Purpose |
|---------|---------|
| `git tag v0 c1` | Create tag named "v0" at commit C1 |
| `git tag v1 c2` | Create tag named "v1" at commit C2 |
| `git checkout c5` | Checkout commit C5 |
| `git checkout HEAD^` | Move HEAD to parent commit |

**Common tag operations:**
```bash
git tag                    # List all tags
git tag v1.0.0 <commit>   # Create annotated tag
git tag -a v1.0.0 -m "Release 1.0.0"  # Tag with message
git push origin v1.0.0    # Push tag to remote
git push origin --tags    # Push all tags
```

#### 📸 Screenshot

<img width="1917" height="473" alt="Lv4-4" src="https://github.com/user-attachments/assets/d8252427-7d6e-4654-aae2-919c2d5b61ce" />


*Screenshot showing tags v0 and v1 placed at commits C1 and C2, with HEAD positioned using relative references*

#### 📝 Explanation & Learning

- **What I learned**:
  - Tags are permanent markers/anchors on specific commits
  - Unlike branches, tags don't move when new commits are made
  - Perfect for marking release points (v1.0, v2.0, etc.)
  - Can create tags at any commit, present or past
  - Tags can be used as references just like commit hashes
  - Two types: lightweight tags and annotated tags

- **Key Concepts**:
  - **Tags as Anchors**: Permanent references that never move
  - **Version Markers**: Used for releases and milestones
  - **Reference Type**: Another way to refer to commits (like branches)
  - **Immutability**: Once created, tags stay at their commit

- **Visual Understanding**:
  - **v0 tag** attached to C1 (early commit)
  - **v1 tag** attached to C2 (next commit)
  - Tags shown as small labels near commits
  - HEAD can be positioned using various references
  - Branches (main, side) can move, but tags stay fixed

- **Tags vs Branches**:
  | Feature | Tags | Branches |
  |---------|------|----------|
  | **Movement** | Never moves | Moves with commits |
  | **Purpose** | Mark milestones | Active development |
  | **Mutability** | Immutable | Mutable |
  | **Use Case** | Releases, versions | Features, work |
  | **Example** | v1.0.0, v2.1.0 | main, feature-x |

- **Tag Naming Conventions**:
  ```
  v1.0.0          - Semantic versioning
  v2.1.3          - Major.Minor.Patch
  release-2024-01 - Date-based
  beta-1          - Pre-release tags
  stable          - Status indicators
  ```

  **Recommendation**: Use annotated tags for releases, lightweight for temporary marks

- **Working with Tags**:
  ```bash
  # Create tag at current commit
  git tag v1.0.0
  
  # Create tag at specific commit
  git tag v1.0.0 abc123
  
  # Create annotated tag
  git tag -a v1.0.0 -m "Release version 1.0.0"
  
  # List all tags
  git tag
  git tag -l "v1.*"    # List matching pattern
  
  # Show tag details
  git show v1.0.0
  
  # Delete tag
  git tag -d v1.0.0
  
  # Push tags to remote
  git push origin v1.0.0      # Push single tag
  git push origin --tags      # Push all tags
  
  # Delete remote tag
  git push origin --delete v1.0.0
  ```

- **Tags in Semantic Versioning**:
  ```
  Format: MAJOR.MINOR.PATCH (e.g., v2.1.3)
  
  MAJOR (2): Breaking changes
  MINOR (1): New features (backwards compatible)
  PATCH (3): Bug fixes
  
  Examples:
  v1.0.0  - Initial release
  v1.0.1  - Bug fix
  v1.1.0  - New feature added
  v2.0.0  - Breaking change introduced
  ```

- **Best Practices**:
  ✅ **Do:**
  - Tag all releases
  - Use annotated tags for releases
  - Follow semantic versioning
  - Include release notes in tag messages
  - Push tags to remote
  
  ❌ **Don't:**
  - Move or delete tags once pushed
  - Tag every commit (only milestones)
  - Use ambiguous names
  - Forget to push tags after creation


---

### 4.5 Git Describe

#### 📋 Problem Statement
Learn to use `git describe` to find the nearest tag and describe where you are in the commit history relative to that tag. This helps identify which version/release a commit is based on.

**Challenge**: Understand how `git describe` works and interpret its output format.

#### 💡 Solution Approach
The `git describe` command outputs information in the format: `<nearest-tag>-<num-commits>-g<hash>`

For example: `v0-2-gC2` means:
- v0 is the nearest tag
- 2 commits away from that tag
- gC2 is the Git hash (g prefix means "git")

The level requires understanding this format and how Git calculates the description. A simple `git commit` on bugFix demonstrates the concept.

#### ⚙️ Commands Used

| Command | Purpose |
|---------|---------|
| `git commit` | Create a commit on bugFix branch |
| `git describe` | (Conceptual) Describe current position relative to nearest tag |

**Git describe syntax:**
```bash
git describe <ref>           # Describe a specific commit/branch
git describe                 # Describe current HEAD
git describe --tags          # Include lightweight tags
git describe --abbrev=0      # Show only the tag name
```

#### 📸 Screenshot

<img width="1919" height="945" alt="Lv4-5" src="https://github.com/user-attachments/assets/4f1001df-6582-4430-802d-923d743ae372" />


*Screenshot showing commit structure with tags v0 and v1, and branches at different positions, demonstrating how git describe calculates distance from nearest tag*

#### 📝 Explanation & Learning

- **What I learned**:
  - `git describe` finds the nearest ancestor tag
  - Output format: `<tag>-<num-commits>-g<hash>`
  - Useful for identifying build versions
  - Helps understand where you are in version history
  - Commonly used in build scripts and CI/CD
  - Makes commit identification human-readable

- **Key Concepts**:
  - **Nearest Tag**: The most recent tag reachable by walking back through ancestors
  - **Distance Count**: Number of commits between current position and tag
  - **Hash Prefix**: Short identifier for the exact commit (with 'g' prefix)
  - **Ancestor Relationship**: Only considers tags in the history path

- **Visual Understanding**:
  - **C0**: Root commit (tagged v0)
  - **C1**: One commit after v0
  - **C2**: Two commits after v0 (tagged v1)
  - **C3**: On side branch
  - **C4, C5**: On side branch, further from tagged commits
  - **C6, C7**: On bugFix branch

  **Examples of git describe output:**
  - At C1: `v0-1-gC1` (1 commit after v0)
  - At C2: would show as `v1` (exactly at tag)
  - At C5: `v1-3-gC5` (3 commits after v1)
  - At C7: `v1-5-gC7` (5 commits after v1, counting through path)

- **Git Describe Options**:
  ```bash
  # Basic describe
  git describe
  
  # Include lightweight tags
  git describe --tags
  
  # Only show tag name (no distance/hash)
  git describe --abbrev=0
  
  # Always show something (hash if no tag)
  git describe --always
  
  # Add 'dirty' if working directory has changes
  git describe --dirty
  
  # First parent only (for merge commits)
  git describe --first-parent
  
  # Match specific pattern
  git describe --match "v*.*.*"
  ```

- **Understanding the Algorithm**:
  ```
  How git describe works:
  
  1. Start at specified commit (or HEAD)
  2. Walk backwards through ancestors
  3. Find first commit with a tag
  4. Count commits between tag and start
  5. Format output: <tag>-<count>-g<hash>
  6. If at tagged commit, return just tag name
  ```

- **Best Practices**:
  ✅ **Do:**
  - Use in automated builds
  - Include in "About" dialogs
  - Log in application startup
  - Use for Docker image tags
  - Include in bug reports
  
  ❌ **Don't:**
  - Rely on it without tags
  - Use as primary versioning (tags are primary)
  - Parse the format (use --abbrev=0 for tag only)
  - Forget to push tags to remote

- **Advanced Usage**:
  ```bash
  # Show full hash
  git describe --long
  # v1.0.0-0-g2a4b6c8f3d...
  
  # Only show if exact match
  git describe --exact-match
  # (only outputs if HEAD is exactly on a tag)
  
  # Describe all refs
  git describe --all
  # Can describe any ref, not just tags
  ```

---

## Level 4 Summary

### Key Concepts Mastered

1. **Selective Commit Application (Cherry-pick)**
   - Grab single commits from complex branch structures
   - Apply specific changes without merging entire branches
   - Non-destructive to source branches

2. **Commit Juggling (Interactive Rebase)**
   - Complex manipulation: Multiple rebase + force moves
   - Simple manipulation: Single rebase with relative refs
   - Reorder, squash, and reorganize commits
   - Two approaches: complex juggling vs elegant simplicity

3. **Tags as Permanent Markers**
   - Mark important milestones and releases
   - Unlike branches, tags never move
   - Essential for version management
   - Two types: lightweight and annotated

4. **Git Describe for Version Identification**
   - Find nearest tag and distance
   - Human-readable version descriptions
   - Perfect for builds and CI/CD
   - Format: `<tag>-<count>-g<hash>`

### Commands Learned

| Command | Description | Use Case |
|---------|-------------|----------|
| `git cherry-pick <commit>` | Copy specific commit to current branch | Selective bug fixes |
| `git rebase -i HEAD~N` | Interactive rebase last N commits | Clean up recent history |
| `git branch -f <branch> <commit>` | Force move branch pointer | Reorganize branches |
| `git tag <name> <commit>` | Create tag at commit | Mark releases |
| `git tag -a <name> -m "msg"` | Create annotated tag | Release with metadata |
| `git describe` | Describe position relative to tags | Version identification |
| `git describe --tags --always` | Always show something | Build versioning |


---
