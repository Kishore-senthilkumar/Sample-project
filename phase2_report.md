# Git Assignment – Phase 2 Report

**Name:** Kishore S  
**Project:** Daily Habit Tracker  
**Repository:** https://github.com/Kishore-senthilkumar/Sample-project

---

# 1. Objective

The objective of this phase was to practice advanced Git operations that are commonly used in real software development. Unlike basic Git commands such as commit and merge, these operations help developers recover lost work, undo mistakes safely, maintain a clean commit history, and selectively move changes between branches.

In this assignment, I continued working on my **Daily Habit Tracker** project and performed various Git operations including **git revert**, **git reflog**, **interactive rebase**, **git cherry-pick**, and repository cleanup.

---

# 2. Task 1 – Git Revert

## Objective

To safely undo a previously committed change without deleting the project history.

## Commands Used

```bash
git add .
git commit -m "Morning walk added to notes"

git add .
git commit -m "Learning activity added to notes"

git add .
git commit -m "Sleeping activity added to notes"

git log --oneline

git revert "commit id"

git log --oneline
```

## Screenshot

> - Befor Revert:
![Before revert](<Images/Screenshot 2026-08-07 122110.png>)
> - After Revert:
![After revert](<Images/Screenshot 2026-08-07 122928.png>)

## Explanation

The `git revert` command created a new commit that reversed the changes made by the selected commit. Instead of removing the incorrect commit from history, Git preserved all previous commits and added another commit that cancelled its effect.

This approach is considered safer because it does not rewrite project history, making it suitable for shared repositories.

## What I Learned

- `git revert` never deletes commits.
- It creates a new commit that reverses an older commit.
- It is the safest way to undo changes that have already been shared with other developers.

---

# 3. Task 2 – Git Reflog

## Objective

To recover work after accidentally modifying the repository history.

## Scenario

I intentionally removed the latest commit using `git reset --hard` and then recovered it using `git reflog`.

## Commands Used

```bash
git reset --hard HEAD~1

git reflog

git reset --hard HEAD@{1}

git log --oneline
```

## Screenshot
> - Before 
![Before](<Images/Screenshot 2026-08-07 122928-1.png>)
> - Deleting last commit
![Deleting last commit](<Images/Screenshot 2026-08-07 135422-1.png>)
> - git reflog output
![Reflog output](<Images/Screenshot 2026-08-07 135511.png>)
> - Repository after recovery
![After recovery](<Images/Screenshot 2026-08-07 135637.png>)

## Explanation

After executing `git reset --hard`, the latest commit disappeared from the normal commit history. However, Git still remembered the previous location of the HEAD pointer inside the reflog.

Using the reflog reference, I restored the repository back to its previous state.

This demonstrated that Git internally keeps track of branch movements even when commits are no longer visible through `git log`.

## What I Learned

- `git log` only displays current commit history.
- `git reflog` records every movement of HEAD.
- Lost commits can often be recovered using reflog.

---

# 4. Task 3 – Interactive Rebase

## Objective

To clean the commit history by combining multiple related commits into a single meaningful commit.

## Scenario

While developing the hydration tracking feature, I made several small commits such as fixing typos and updating descriptions. Before completing the feature, I combined those commits into one clean commit.

## Commands Used

```bash
git checkout -b rebase-demo

git add .
git commit -m "Added new activity to notes"

git add .
git commit -m "Fixed typo in notes"

git add .
git commit -m "New learning activity added"

git add .
git commit -m "Assignment Time added to notes"

git log --oneline

git rebase -i HEAD~4
```

---

> - Before Rebbase
![Before rebase](<Images/Before rebase.png>)

Example:

```
Added new activity to notes
Fixed typo in notes
New learning activity added
Assignment Time added to notes
```

> - Pick squase Consolde
![Console](<Images/PICk squash console.png>)
> - After Rebase
![After rebase](<Images/After rebase.png>)

Example:

```
Added and updated activities in notes with typos fixed
Assignment Time added to notes
```

---

## Explanation

Interactive rebase allowed me to combine multiple related commits into one meaningful commit.

Instead of showing several small commits such as typo fixes and minor updates, the repository history became much cleaner and easier to understand.

This improves readability for both current developers and future contributors.

## What I Learned

- Interactive rebase helps maintain a clean commit history.
- Small intermediate commits can be combined before sharing code.
- A clean history makes projects easier to review and maintain.

---

# 5. Task 4 – Git Cherry-pick

## Objective

To copy a specific commit from one branch into another branch without merging the entire branch.

## Scenario

I created two feature branches:

- **feature-theme**
- **feature-export**

The theme branch contained two commits:

- Added dark mode
- Added color customization

The export feature only required the dark mode functionality, so I copied only that commit using `git cherry-pick`.

## Commands Used

```bash
git checkout -b feature-theme

git add .
git commit -m "Dark mode feature is added"

git add .
git commit -m "Colour customization feature is added"

git checkout main

git checkout -b feature-export

git cherry-pick <commit-hash>

git log --oneline
```

## Screenshot

> - Feature Theme:
![theme feature](<Images/feature theme.png>)
> - Befor Cherry pick in Export branch
![Before cherry pick](<Images/featrure export before CP.png>)
> - After Cherry pick in Export branch
![After Cherry pick](<Images/feature export after CP.png>)

## Explanation

Instead of merging the entire `feature-theme` branch, I copied only the required commit into the `feature-export` branch.

This prevented unrelated changes from entering the branch while still reusing previously completed work.

## What I Learned

- Cherry-pick copies only selected commits.
- It is useful when only one feature is required from another branch.
- It avoids unnecessary merges.

---

# 6. Task 5 – Repository Cleanup

## Objective

To prepare the repository for release by cleaning unused branches and creating a version tag.

## Commands Used

```bash
git branch -d feature-theme

git branch -d feature-export

git branch -d rebase-demo

git tag -a v1.0 -m "Habit Tracker Version 1"

git tag

git push origin v1.0
```

## Screenshot

> - After Cleaning branches
![After clean](<Images/Deleted all branch.png>)
> - Tag creation
![Tag creation](<Images/Tag created.png>)
> - Tag created
![Tag created](<Images/Tage created.png>)

## Explanation

After completing all features, I deleted branches that were no longer required.

I then created an annotated Git tag named **v1.0** to represent the first stable version of the project.

Using tags makes it easier to identify important project versions during future development.

## Final Repository State

- All completed work merged successfully.
- Unused branches removed.
- Version **v1.0** created.
- Repository history remained clean and organized.

---

# 7. Difficulties Faced

During this assignment, I initially found **interactive rebase** confusing because rewriting commit history requires careful attention. Understanding the difference between **git revert** and **git reset** also took some practice.

Another challenge was recovering commits using **git reflog**, since it was my first time using HEAD references.

After performing each operation step by step, I gained confidence in using these commands and understood when each one should be applied in real-world projects.

---

# 8. Conclusion

This assignment helped me understand advanced Git operations beyond the basic workflow.

I learned how to safely undo changes using **git revert**, recover lost commits using **git reflog**, organize commit history through **interactive rebase**, selectively reuse commits with **git cherry-pick**, and prepare a project for release by cleaning branches and creating version tags.

Overall, this phase improved my understanding of Git as a version control system and showed how these advanced commands are used in professional software development to manage code efficiently.