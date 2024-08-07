#### 1. **Explain the difference between merge and rebase.**
- **Response**:
  - **Merge**: Combines multiple sequences of commits into one unified history. It creates a new commit that ties together the histories of the two branches. This is often used when you want to integrate changes from one branch into another without rewriting commit history.
  - **Rebase**: Reapplies commits from a branch on top of another base tip. This rewrites the commit history, creating a linear progression of commits. It's useful for cleaning up commit history or integrating changes in a way that avoids the "merge commit" clutter.

- **Example**:
  - **Merge**:
    ```bash
    git checkout feature-branch
    git merge main
    ```
    Demonstrate how merge adds a new commit and keeps the history of both branches. Show the resulting commit graph with the merge commit.
  - **Rebase**:
    ```bash
    git checkout feature-branch
    git rebase main
    ```
    Show how rebase rewrites the commit history and places feature-branch commits on top of main, resulting in a linear commit history.

#### 2. **How do you use Git rebase to clean up a feature branch?**
- **Response**:
  - Use `git rebase -i` (interactive rebase) to clean up commits. This allows you to combine multiple commits into one (squash), reorder them, or edit commit messages. It provides an opportunity to present a clean and concise commit history before merging into the main branch.

- **Example**:
  - ```bash
    git checkout feature-branch
    git rebase -i HEAD~4
    ```
    Show the interactive rebase screen, where you can choose actions like `pick`, `squash`, `reword`, etc. Explain each option and demonstrate a simple rebase where multiple commits are squashed into one.

#### 3. **What is a Git stash, and how do you use it?**
- **Response**:
  - Git stash temporarily shelves (or stashes) changes you've made to your working directory. This allows you to switch branches without committing your changes. Stashed changes can be reapplied later.

- **Example**:
  - ```bash
    git stash
    git checkout other-branch
    git stash apply
    ```
    Demonstrate stashing changes, switching to another branch, and then reapplying the stashed changes.

#### 4. **How do you resolve a merge conflict in Git?**
- **Response**:
  - When a merge conflict occurs, Git marks the conflicted areas in the affected files. You need to manually resolve the conflicts by editing the files to make sure they reflect the desired result. After resolving conflicts, you add the resolved files and complete the merge.

- **Example**:
  - ```bash
    git merge feature-branch
    # Git indicates a conflict
    # Open the conflicted file(s) and resolve conflicts
    git add resolved-file
    git commit
    ```
    Create a scenario with a merge conflict, show the conflicted markers (e.g., `<<<<<<< HEAD`), resolve the conflict, and complete the merge.

#### 5. **What is Git cherry-pick and when would you use it?**
- **Response**:
  - Git cherry-pick applies the changes introduced by existing commits to the current branch. It is used to copy specific commits from one branch to another, especially useful when you want to bring a bug fix from a feature branch to a production branch without merging the entire feature branch.

- **Example**:
  - ```bash
    git checkout main
    git cherry-pick <commit-hash>
    ```
    Show how to cherry-pick a specific commit from a feature branch to the main branch, explaining the use case of selectively applying commits.

#### 6. **Explain how Git tags work and how you can create a tag.**
- **Response**:
  - Git tags are references to specific points in Git history, typically used to mark release points (e.g., v1.0.0). Tags can be lightweight (a pointer to a commit) or annotated (a full object in the Git database, containing metadata).

- **Example**:
  - ```bash
    git tag -a v1.0.0 -m "Release version 1.0.0"
    git push origin v1.0.0
    ```
    Demonstrate creating an annotated tag with a message and pushing it to a remote repository.

#### 7. **Can you describe Git Flow and its key branches?**
- **Response**:
  - Git Flow is a branching model that defines a strict branching structure. It includes key branches such as `master` (production-ready code), `develop` (integration branch), `feature/*` (new features), `release/*` (preparing for a new production release), and `hotfix/*` (emergency fixes). Git Flow helps manage releases, hotfixes, and features in a structured manner.

- **Example**:
  - ```bash
    git flow init
    git flow feature start my-feature
    git flow feature finish my-feature
    ```
=============================================================================================================================================================================================
#### 1. **What is Git and why is it used?**
- **Response**: 
  - Git is a distributed version control system designed to handle everything from small to very large projects with speed and efficiency. It allows multiple developers to work on the same codebase simultaneously without conflicts, tracks changes, and enables collaboration.

#### 2. **Explain the difference between `git pull` and `git fetch`.**
- **Response**: 
  - `git fetch` downloads commits, files, and refs from a remote repository into your local repository. It doesn’t merge changes into your working directory.
  - `git pull` does the same as `git fetch` but also immediately merges the downloaded changes into your working branch.

#### 3. **How do you resolve a merge conflict in Git?**
- **Response**: 
  - When a merge conflict occurs, Git will mark the conflicted areas in the affected files. You need to manually resolve the conflicts, then add the resolved files (`git add <file>`) and commit the merge (`git commit`).

#### 4. **What is a Git branch and why is it important?**
- **Response**: 
  - A branch in Git represents an independent line of development. It is important because it allows multiple developers to work on different features or fixes without interfering with each other’s work. Branches can be merged back into the main branch once they are complete.

#### 5. **Describe the Git workflow you use in your current project.**
- **Response**: 
  - Typically, I use a feature branch workflow. Each new feature or bug fix is developed in a separate branch, which is then merged into the main branch after review. This keeps the main branch stable and clean.

#### 6. **How do you create a new branch in Git?**
- **Response**: 
  - To create a new branch:
    ```bash
    git checkout -b <branch-name>
    ```

#### 7. **What is a commit in Git?**
- **Response**: 
  - A commit in Git is a snapshot of your repository at a specific point in time. It records changes to files and directories, allowing you to revert back to that state if needed.

#### 8. **How do you revert a commit in Git?**
- **Response**: 
  - To revert a commit:
    ```bash
    git revert <commit-hash>
    ```
  - This creates a new commit that undoes the changes made by the specified commit.

#### 9. **Explain Git rebase and how it differs from merge.**
- **Response**: 
  - `git rebase` moves or combines a sequence of commits to a new base commit. It re-applies commits on top of another base tip, creating a linear history. In contrast, `git merge` combines changes from two branches and creates a new merge commit, preserving the original history.

#### 10. **What is Git stash and how do you use it?**
- **Response**: 
  - Git stash temporarily shelves changes you have made to your working directory so you can work on something else. To stash changes:
    ```bash
    git stash
    ```
  - To apply stashed changes:
    ```bash
    git stash apply
    ```

#### 11. **How do you delete a branch in Git?**
- **Response**: 
  - To delete a branch locally:
    ```bash
    git branch -d <branch-name>
    ```
  - To delete a branch remotely:
    ```bash
    git push origin --delete <branch-name>
    ```

#### 12. **Explain the use of `.gitignore` file.**
- **Response**: 
  - The `.gitignore` file specifies files and directories that Git should ignore and not track. It helps keep unnecessary files out of your repository.

#### 13. **What is Git cherry-pick and when would you use it?**
- **Response**: 
  - `git cherry-pick` applies the changes introduced by an existing commit to the current branch. It’s useful for applying specific changes from one branch to another without merging the entire branch.

#### 14. **Describe Git Flow and its key branches.**
- **Response**: 
  - Git Flow is a branching model with a predefined set of branches and rules. Key branches include `master` (production), `develop` (integration), `feature/*` (new features), `release/*` (preparing for a new production release), and `hotfix/*` (emergency fixes).

#### 15. **How do you rename a branch in Git?**
- **Response**: 
  - To rename the current branch:
    ```bash
    git branch -m <new-branch-name>
    ```

#### 16. **What is a detached HEAD in Git and how do you fix it?**
- **Response**: 
  - A detached HEAD state occurs when you checkout a commit directly instead of a branch. To fix it, you can create a new branch from that commit:
    ```bash
    git checkout -b <new-branch-name>
    ```

#### 17. **How do you undo the last commit but keep the changes?**
- **Response**: 
  - To undo the last commit but keep the changes:
    ```bash
    git reset --soft HEAD~1
    ```

#### 18. **Explain the difference between `git reset` and `git revert`.**
- **Response**: 
  - `git reset` moves the HEAD to a previous commit, discarding subsequent commits. It can be used to unstage changes (`--soft`) or delete changes (`--hard`).
  - `git revert` creates a new commit that undoes the changes made by a previous commit without altering the commit history.

#### 19. **What is a Git tag and how do you create one?**
- **Response**: 
  - A Git tag is a reference to a specific point in the Git history. To create a tag:
    ```bash
    git tag -a <tag-name> -m "Tag message"
    git push origin <tag-name>
    ```

#### 20. **How do you handle large binary files in Git?**
- **Response**: 
  - Use Git LFS (Large File Storage) to handle large binary files. It replaces large files with text pointers inside Git, while storing the actual file contents on a remote server. To track a file with Git LFS:
    ```bash
    git lfs track "<file>"
    git add .gitattributes
    git add <file>
    git commit -m "Add large file"
    git push
    ```
