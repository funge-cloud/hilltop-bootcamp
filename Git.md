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
