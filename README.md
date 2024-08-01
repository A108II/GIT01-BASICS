# Git Basics

Git is a distributed version control system used to track changes in source code during software development. It allows multiple developers to work on a project simultaneously, manage changes, and collaborate efficiently. Git provides features like branching, merging, and version history.

## Initialization and Status

- Initialize Git with `git init`.
- Check the current state of the working directory with `git status`, which includes staged changes, unstaged changes, and untracked files.
- Add changes with `git add .`. The `.` represents the current folder, picking everything in it.
- Apply changes with `git commit -m "version1"`. The `-m` stands for the message, which describes the change.

## Configuration

- If the error `fatal: unable to auto-detect email address` occurs, use:
  ```bash
  git config --global user.email "user@example.com"
  git config --global user.username "Your name"
  ```

## Version History

- Check version history with `git log`.
- To amend a recent commit if you misspelled or forgot something, add changes with `git add .` and use:
  ```bash
  git commit -m "version1" --amend
  ```

## Staging and Unstaging Changes

- To unstage files or folders, use `git reset .`. For a specific file, use `git reset filename.ext`.
- To discard changes in files or folders, use `git checkout -- .`. Replace `.` with a file or folder name if needed.

## Switching Commits

- Switch to different commits with `git checkout commit-hash`.
- `git log` shows commits before the current commit. To see all commits, use `git log --all`.
- `HEAD` indicates the current version.

## Restoring Previous Versions

### Method 1: Direct Checkout (Causes Branching)

1. Restore to a previous commit:
    ```bash
    git checkout version1-commit-hash
    ```
2. Make any necessary changes to version 1.
3. Stage the changes:
    ```bash
    git add .
    ```
4. Commit the changes:
    ```bash
    git commit -m "version1 restored-updated"
    ```
5. This method causes branching. To see the branching effect:
    ```bash
    git log --all --graph
    ```
6. You will see that version1 is branching off, which might not be the desired outcome.

### Method 2: Restoring Without Branching

1. Switch to the `master` branch:
    ```bash
    git checkout master
    ```
2. Verify you are on the correct branch:
    ```bash
    git log --all --graph
    ```
3. Restore the contents of version1:
    ```bash
    git checkout version1-commit-hash .
    ```
4. Check that branching is not happening and `HEAD` points to `master`:
    ```bash
    git log --all --graph
    ```
5.  Make any changes in the commit history and stage the restored files:
    ```bash
    git status
    git add .
    ```
6. Commit the restored version:
    ```bash
    git commit -m "version1 restored-updated"
    ```
7. Verify the new commit is on top without branching:
    ```bash
    git log --all --graph
    ```
8. You will see `version1 restored` at the top, with `HEAD` pointing to it, and no branching.

## Aliases

- Set up aliases in Git:
  ```bash
  git config --global alias.s "status"
  git config --global alias.cm "commit"
  git config --global alias.co "checkout"
  ```
  This allows using shorter commands like `git s` instead of `git status`.

## Ignoring Files

- To ignore certain files, add a `.gitignore` file to the current folder:
  ```bash
  git status
  git add .
  git commit -m "adding gitignore"
  ```

## Removing Git from a Project

- To remove Git completely from a project, use:
  ```bash
  rm -rf .git
  ```