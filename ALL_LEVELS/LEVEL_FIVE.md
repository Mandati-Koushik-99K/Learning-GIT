## Table of Contents

- [Level 5: Advanced Topics](#level-5-advanced-topics)
  - [5.1 Rebasing over 9000 times](#51-rebasing-over-9000-times)
  - [5.2 Multiple Parents](#52-multiple-parents)
  - [5.3 Branch Spaghetti](#53-branch-spaghetti)

---


## Level 5: Advanced Topics

### 5.1 Rebasing over 9000 times

#### 📋 Problem Statement
Master the art of complex rebasing by performing multiple rebase operations across different branches. This level tests your ability to reorganize a complex commit structure with many branches (bugFix, side, another) using interactive rebasing and branch manipulation.

**Challenge**: Navigate through multiple branches and use a combination of checkout, rebase, and branch force-move operations to achieve a clean, linear history.

#### 💡 Solution Approach
This advanced challenge requires orchestrating multiple rebase operations across several branches. The solution involves:

1. Checking out different branches sequentially
2. Using `git rebase -i` to interactively reorganize commits
3. Dropping unwanted commits via interactive rebase
4. Using `git branch -f` to position branches correctly

The command sequence shown in screenshots:
```bash
git checkout bugFix
git rebase -i main
git checkout side
git rebase -i bugFix
git checkout another
git rebase -i side
git branch -f main c7'
```

This creates a clean, linear history by stacking branches on top of each other.

#### ⚙️ Commands Used

| Command | Purpose |
|---------|---------|
| `git checkout bugFix` | Switch to bugFix branch |
| `git rebase -i main` | Interactive rebase bugFix onto main |
| `git checkout side` | Switch to side branch |
| `git rebase -i bugFix` | Interactive rebase side onto bugFix |
| `git checkout another` | Switch to another branch |
| `git rebase -i side` | Interactive rebase another onto side |
| `git branch -f main c7'` | Force move main branch to final commit c7' |

#### 📸 Screenshots

<img width="1919" height="940" alt="Lv5-1" src="https://github.com/user-attachments/assets/ad07f5ac-9a6e-446e-a66a-278b3f455679" />


*First interactive rebase dialog showing "Rebasing 3 Commits" with options to pick/drop C4, C5, and C7*

<img width="1911" height="938" alt="Lv5-1 1" src="https://github.com/user-attachments/assets/e4b6438b-fac5-41f2-b01d-5692f8f51902" />


*Mid-process showing the complex branch structure being reorganized with multiple branches (bugFix, side, another, main) and their commits*

<img width="1918" height="947" alt="Lv5-1 2" src="https://github.com/user-attachments/assets/97b21feb-86a1-420d-91af-4bb02afc4ff5" />


*Second interactive rebase dialog showing "Rebasing 3 Commits" with C4, C5, C6 being reorganized*

<img width="1916" height="919" alt="Lv5-1 3" src="https://github.com/user-attachments/assets/7aaafc96-3f1b-4469-a8ba-b5540ee855ea" />


*Final clean linear history achieved with properly stacked branches and main at c7', another at c7'*

#### 📝 Explanation & Learning

- **What I learned**:
  - Complex multi-branch rebasing requires careful sequencing
  - Each rebase builds on the previous one
  - Interactive rebase can drop unwanted commits during reorganization
  - Branch stacking creates clean, linear histories from complex structures
  - `git branch -f` is essential for positioning branches after rebasing
  - The order of operations matters significantly
  - Prime notation (c7', c6', etc.) indicates commits recreated through rebasing

- **Key Concepts**:
  - **Sequential Rebasing**: Rebase branches one after another in logical order
  - **Branch Stacking**: Place branches on top of each other linearly
  - **Commit Filtering**: Use interactive rebase to drop unnecessary commits
  - **Final Positioning**: Use branch force-move to position branches at final commits
  - **Complex Workflow**: Combining multiple Git operations to achieve clean history

- **Visual Understanding from Screenshots**:

  **Screenshot 1 (First Interactive Dialog)**:
  - Shows "Rebasing 3 Commits"
  - Commits C4, C5, C7 available to pick/drop
  - This is likely rebasing one of the branches onto another
  - Can choose which commits to include in final history

  **Screenshot 2 (Process View)**:
  - Complex initial state with multiple diverging branches
  - bugFix, side, another, and main branches visible
  - Shows the messy structure that needs cleanup
  - Multiple paths and branches that will be linearized

  **Screenshot 3 (Second Interactive Dialog)**:
  - Another "Rebasing 3 Commits" dialog
  - Shows C4, C5, C6 being processed
  - Part of the sequential rebasing process
  - Continuing to build the linear history

  **Screenshot 4 (Final Clean State)**:
  - Beautiful linear history achieved!
  - Clean path from C0 → C1 → C2 → C3' → C4' → C5' → C6' → C7'
  - All branches properly positioned
  - main and another both at c7'
  - Perfect example of complex reorganization

- **Best Practices for Complex Rebasing**:

  ✅ **Do:**
  - Plan the sequence before starting
  - Work on local branches only
  - Create backup branch: `git branch backup-main main`
  - Test after each rebase step
  - Use `git log --graph` to visualize
  - Document the strategy
  
  ❌ **Don't:**
  - Rebase published branches
  - Skip testing between steps
  - Rush through interactive dialogs
  - Forget which branch you're on
  - Rebase without understanding the graph

---

### 5.2 Multiple Parents

#### 📋 Problem Statement
Work with merge commits that have multiple parents. Learn to navigate and reference commits with multiple parent relationships using special syntax like `^` with numbers to specify which parent to follow.

**Challenge**: Understand and manipulate commits in a history with merge commits, where commits can have two parents. Use commands like `git branch -f main c2` to position branches correctly and `git branch bugWork` to create branches at specific merge points.

#### 💡 Solution Approach
When dealing with merge commits (commits with multiple parents), you need to understand parent relationships:
- First parent: Created by the branch you're on when merging
- Second parent: The branch you merged in

The solution involves:
```bash
git branch -f main c2     # Force main to commit c2
git branch bugWork         # Create bugWork branch at current location
git branch -f main c7     # Move main to c7
```

This demonstrates working with a commit graph where C1 has two parents (C2 and C3), showing the merge point.

#### ⚙️ Commands Used

| Command | Purpose |
|---------|---------|
| `git branch -f main c2` | Force move main branch to commit c2 |
| `git branch bugWork` | Create new branch bugWork at current HEAD |
| `git branch -f main c7` | Move main branch to commit c7 |


#### 📸 Screenshots

<img width="1919" height="907" alt="Lv5-2" src="https://github.com/user-attachments/assets/a2c164be-d918-4e7b-b9fa-2b2f65be25a8" />


*Initial state showing merge commit structure where C1 has two parents: C2 (via bugWork) and C3, demonstrating multiple parent relationships*

<img width="1899" height="935" alt="Lv5-2 1" src="https://github.com/user-attachments/assets/ccf657b2-ccc6-4405-bae2-7bcf172d3e81" />


*Mid-process showing branch manipulations with bugWork at C2, main being moved, and the complex parent relationships between C1, C2, C3, and beyond*

<img width="1912" height="889" alt="Lv5-2 2" src="https://github.com/user-attachments/assets/b54223c4-0f9c-4ab2-b333-382f4dd27af0" />


*Final state with main at c7, bugWork properly positioned, showing the full merge commit graph with multiple parent relationships*

#### 📝 Explanation & Learning

- **What I learned**:
  - Merge commits have TWO parents (or more in octopus merges)
  - First parent is from the branch you were on when merging
  - Second parent is from the branch you merged in
  - `^` with numbers specifies which parent to follow: `^1` or `^2`
  - `~` only follows first parent in the chain
  - Understanding parent relationships is crucial for complex history navigation
  - Branch positioning with `git branch -f` works with merge commits too

- **Key Concepts**:
  - **Merge Commits**: Commits with multiple parents that join branches
  - **First Parent**: The commit on the branch you were on when merging
  - **Second Parent**: The tip of the branch you merged
  - **Parent Notation**: `^1`, `^2` to specify which parent lineage to follow
  - **Multiple Parent Graph**: DAG (Directed Acyclic Graph) structure

- **Visual Understanding from Screenshots**:

  **Screenshot 1 (Initial State)**:
  - C0 → C1 with two branches diverging
  - bugWork branch at C2
  - main branch split showing merge structure
  - C1 is a merge commit connecting C2 and C3 paths

  **Screenshot 2 (Process)**:
  - Shows the complex relationship structure
  - Multiple paths through history
  - bugWork branch at C2
  - main branch in the process of being positioned
  - Demonstrates the graph nature of Git history

  **Screenshot 3 (Final State)**:
  - Clean final structure achieved
  - main at C7 (final commit after merge path)
  - bugWork at C2
  - Shows complete merge commit graph
  - All parent relationships visible


- **Difference Between ^ and ~**:

  | Operator | Behavior with Merges | Use Case |
  |----------|---------------------|----------|
  | `^` | Can specify which parent (^1, ^2) | Navigate merge branches |
  | `~` | Always follows first parent only | Linear ancestry |
  | `^2` | Follows second parent (merged branch) | See merged work |
  | `~2` | Two generations via first parent | Count back linearly |

  **Example:**
  ```
       C1 (merge)
      /  \
    C2    C5
    |     |
    C3    C6
    |
    C4
  
  From C1:
  C1^   = C2  (first parent)
  C1^2  = C5  (second parent)
  C1~1  = C2  (same as C1^)
  C1~2  = C3  (C2's first parent)
  C1^2~1 = C6 (C5's first parent)
  ```

- **Working with Merge Commits**:

  **Creating a Merge Commit:**
  ```bash
  git checkout main
  git merge feature
  # Creates merge commit with two parents:
  # - First parent: previous main commit
  # - Second parent: feature branch tip
  ```

  **Examining Merge Commits:**
  ```bash
  # Show merge commit info
  git show HEAD         # Shows combined diff
  git log --graph       # Visual representation
  git log --first-parent  # Only main line
  git log HEAD^2        # Only merged branch line
  ```


- **Merge Commit Best Practices**:

  ✅ **Do:**
  - Use merge commits for feature integration
  - Preserve branch context with merge commits
  - Use `--no-ff` to force merge commits
  - Document merges with good messages
  - Understand parent relationships
  
  ❌ **Don't:**
  - Lose track of which parent is which
  - Use fast-forward when history matters
  - Ignore second parent in investigations
  - Forget that ~ only follows first parent

---

### 5.3 Branch Spaghetti

#### 📋 Problem Statement
The ultimate Git challenge! Navigate an incredibly complex branching structure that looks like a plate of spaghetti. Use cherry-pick and branch positioning to extract specific commits and reorganize them into a clean structure with branches named "one", "two", and "three".

**Challenge**: From a massively complex commit graph with multiple intertwined branches, selectively cherry-pick specific commits and position branches correctly to achieve the goal state.

#### 💡 Solution Approach
This level tests mastery of ALL Git concepts learned. The solution requires:

1. Understanding the complex graph structure
2. Identifying target commits among the chaos
3. Cherry-picking specific commits in the right order
4. Positioning branches precisely

Command sequences shown:
```bash
git checkout one
git cherry-pick c4 c3 c2

git checkout two  
git cherry-pick c5 c4' c3' c2'

git branch -f three c2
```

Alternative approaches might work, but the key is extracting the right commits to the right branches from the spaghetti structure.

#### ⚙️ Commands Used

| Command | Purpose |
|---------|---------|
| `git checkout one` | Switch to branch "one" |
| `git cherry-pick c4 c3 c2` | Copy commits c4, c3, c2 to branch "one" |
| `git checkout two` | Switch to branch "two" |
| `git cherry-pick c5 c4' c3' c2'` | Copy commits to branch "two" (primed versions) |
| `git branch -f three c2` | Force position branch "three" at commit c2 |

**Note**: The exact commits and order may vary depending on which commits need to be extracted from the spaghetti.

#### 📸 Screenshots

<img width="1919" height="940" alt="Lv5-3" src="https://github.com/user-attachments/assets/25c9b6ad-f73c-4d5f-802b-f35de3bc0e6e" />


*Initial state showing incredibly complex "spaghetti" structure with multiple intertwined branches and commits scattered everywhere - truly looks like tangled spaghetti!*

<img width="1917" height="943" alt="Lv5-3 1" src="https://github.com/user-attachments/assets/6ec217d9-801c-4932-836d-1183d717ff3b" />


*Mid-process showing the extraction of specific commits from the chaos, with branches "one", "two", and "three" being organized*

<img width="1917" height="753" alt="Lv5-3 2" src="https://github.com/user-attachments/assets/43e187dc-9655-400c-bc71-310bc3253c76" />


*Final beautiful clean state with three organized branches (one, two, three) each containing the correct cherry-picked commits in proper order - from spaghetti to perfection!*

#### 📝 Explanation & Learning

- **What I learned**:
  - Git mastery means navigating ANY level of complexity
  - Cherry-pick is essential for extracting value from chaos
  - Complex graphs can be tamed with systematic approach
  - Visualization is crucial when dealing with spaghetti
  - Branch naming (one, two, three) provides clear organization
  - Every piece of work in Git can be reorganized
  - The "spaghetti" name is very literal - the graph really looks like tangled pasta!

- **Key Concepts**:
  - **Spaghetti Code**: Git history can become very tangled
  - **Systematic Extraction**: Cherry-pick to extract valuable commits
  - **Branch Organization**: Use meaningful branch names
  - **Graph Untangling**: Transform chaos into order
  - **Commit Selection**: Identify and extract needed commits
  - **Clean Architecture**: End with organized, maintainable structure

- **Visual Understanding from Screenshots**:

  **Screenshot 1 (Initial Spaghetti)**:
  - EXTREMELY complex graph structure
  - Multiple branches criss-crossing
  - Commits scattered throughout
  - Nearly impossible to follow any single path
  - Truly deserves the name "spaghetti"
  - Branch "three" with label "two" visible
  - Multiple merge points creating tangled web

  **Screenshot 2 (Process)**:
  - Starting to extract order from chaos
  - Branches "one", "two", "three" being organized
  - Some commits being cherry-picked
  - Structure starting to emerge
  - Still shows some of the original complexity
  - Transitional state between chaos and order

  **Screenshot 3 (Final Clean)**:
  - Beautiful, clean, organized structure!
  - Branch "one" at C1 with proper lineage
  - Branch "three" (marked "three two") showing organization
  - Branch "two" positioned correctly
  - Linear or near-linear paths
  - From spaghetti to perfection
  - Main branch clearly marked
  - Tags visible at C1 (one, three, two)

- **The "Spaghetti" Phenomenon**:

  **How It Happens:**
  ```
  - Multiple developers working simultaneously
  - Many feature branches created
  - Frequent merges back and forth
  - Experimental branches not cleaned up
  - Long-lived feature branches
  - Cross-merges between features
  - Result: Tangled commit graph
  ```
  

- **Tools for Navigating Spaghetti**:

  **Visualization:**
  ```bash
  # GUI tools
  gitk --all
  git log --graph --all --oneline --decorate
  
  # See all branches
  git branch -a -vv
  
  # Find merge base
  git merge-base branch1 branch2
  
  # Show relationship
  git show-branch
  ```

  **Search Tools:**
  ```bash
  # Find commits by message
  git log --all --grep="pattern"
  
  # Find commits by code change
  git log --all -S"code_string"
  
  # Find commits by author
  git log --all --author="name"
  
  # Find commits by date
  git log --all --since="2 weeks ago"
  ```

- **Prevention is Better Than Cure**:

  **Avoiding Spaghetti:**
  ✅ **Do:**
  - Use short-lived feature branches
  - Rebase feature branches on main regularly
  - Delete merged branches
  - Use linear history (rebase instead of merge)
  - Clean up experimental branches
  - Document branch purposes
  - Regular history cleanup
  
  ❌ **Don't:**
  - Keep branches alive forever
  - Cross-merge feature branches
  - Create branches from branches from branches
  - Merge partially completed work
  - Ignore branch hygiene
  - Create "temporary" branches that stay permanent

---

## Level 5 Summary

### Key Concepts Mastered

1. **Complex Multi-Branch Rebasing**
   - Sequential rebasing across multiple branches
   - Stacking branches for linear history
   - Interactive rebase with commit filtering
   - Strategic use of branch force-moves

2. **Multiple Parent Navigation**
   - Understanding merge commit structure
   - First parent vs second parent
   - Parent notation (`^1`, `^2`, `~`)
   - Working with complex merge histories

3. **Branch Spaghetti Untangling**
   - Navigating extremely complex graphs
   - Systematic commit extraction
   - Cherry-picking from chaos
   - Rebuilding clean structure

### Commands Master List

| Command | Description | Advanced Use Case |
|---------|-------------|-------------------|
| `git rebase -i <base>` | Interactive rebase | Sequential branch stacking |
| `git branch -f <branch> <commit>` | Force move branch | Positioning after complex operations |
| `git cherry-pick <commits...>` | Copy specific commits | Extracting from spaghetti |
| `git checkout HEAD^1` | Navigate to first parent | Exploring merge history |
| `git checkout HEAD^2` | Navigate to second parent | Following merged branch |
| `git log --graph --all` | Visualize full history | Understanding spaghetti |
| `git reflog` | See all HEAD movements | Recovering from mistakes |

### Parent Navigation Reference

```
For merge commit C1:
     C1
    /  \
  C2    C3
  |     |
  C4    C5

From C1:
C1^   → C2 (first parent, same as C1^1)
C1^2  → C3 (second parent)
C1~1  → C2 (same as C1^, first parent only)
C1~2  → C4 (C2's first parent)
C1^2~1 → C5 (C3's first parent)

Rule: ^ can specify parent number, ~ only follows first parent
```

---
