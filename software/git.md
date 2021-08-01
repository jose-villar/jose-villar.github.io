# Git

## Configuration

~~~
// Show config
git config --list

git config --global user.name <username>
git config --global user.email <email>
git config --global core.editor nvim
git config --global init.defaultBranch main

// Disable fast forward merges
git config --global ff no

// Handle EOL
// UNIX:
git config --global core.autocrlf input
// WINDOWS:
git config --global core.autocrlf true

// Save credentials to avoid git asking for them every time
git config --global credential.helper cache

// Remove saved credentials
git config --global --unset credential.helper
~~~

## Creating a New Project

### Connect Local Repository to the Cloud

~~~
git init
git remote add origin <cloud repo url>
git push -u origin main // main is the local branch
~~~

### Connect Cloud Repository to the System

~~~
git clone
git pull
~~~

## Basic Flow

~~~
git status
git add
git commit -m 'message'
git push origin <branchName> // pushing changes to origin/<branchName>
~~~

## Branches

~~~
// Create new branch
git branch <branchName>

// Add the new branch to the repo
git push --set-upstream origin <branchName>

// To switch to a branch, there are 2 ways:
git checkout <branchName>
git switch <branchName>

// Delete a branch
git branch -d <branchName>

// Show current branch
git branch
~~~

## Merges

~~~
// Merge target branch into current one
git merge <target>
~~~

## Revert

~~~
// Instead of removing the commit, it figures out how to invert the changes
// in the commit, then appends a new commit with the inverse content
git revert <commitHash>
~~~

## Reset

~~~
git reset <commitDestino>
git push -f

// Examples
// Removes last commit, keeping changes staged
git reset --soft HEAD~1

// Removes last commit, keeping current changes unstaged
git reset --mixed HEAD~1

// Removes last commit, discarding local changes
git reset --hard HEAD~1

// See all commits (including lost commit when doing a reset). Then you can
// reset back to one of them
git reflog
~~~

## Restore

~~~
// If the change has not been added you can just do a:
git restore .

// Discard changes from staged area (they persist in working directory)
git restore --staged <target>

// Remove from untracked
git rm --cached <target>
// Use git rm -h to see short help or --help to see the verbose version
~~~



## Inspecting

~~~
// Show commits
git log
git log -<n> // show last n commits
git log --oneline
git log --all --graph --decorate

// Filter commits by day
git log --after aaaa-mm-dd
git log --after="2020-11-31"
git log --after="yesterday"
git log --after="one week ago"

git log --author="Alana"

// Press q to exit the commit log.

// See what files were changed on every commit
git log --stat

// Show contributions by author
git shortlog
~~~

### Commits


#### Differences

~~~
// Show commit info
git show <commitHash>

// Filter commits by range
git log <some hash> <some other hash>

// Filter by commit message
git log --grep="GUI"

// See the changes
git log --patch

// See commits that changed some file
git log <filename>
~~~

#### Details

~~~
// Show the state of a file in a given commit
git show <commitHash>:<path/to/file>

// Move to a previous state of the project in read-only mode
git checkout <commit id>

// See commits that modified some line
git log -S"some line of code"
~~~

## Rebasing

### Join Commits

~~~
// you should pick the parent of the commit you want to modify
git rebase -i <Target commit>
git rebase --continue // to finish
~~~

### Split Commits

~~~
git rebase -i <Target commit>
// then pick the edit option
git log
git reset HEAD^
git add ...
git commit ...
git rebase --continue
~~~

## Comparing

~~~
// Shows unstaged changes, comparing to the last commit
git diff

// Compare staged files with the version before staging them
git diff --staged
~~~

## Various

### Index

~~~
// List files in index
git ls-files
~~~

### Do and Stage in 1 Step

~~~
git remove
git rename
~~~

### Remove Untracked

~~~
git clean -d -n // dry run
git clean -d -f
~~~

~~~
// Remove the branches that no longer exist in origin
git remote prune origin
~~~


### Restore Older Version of a File

~~~
// Restore the version of a file present in some other commit
git checkout <commitHash> <file>

// Restore a file to a previous version (1 commit before)
git restore --source=HEAD~1 <target file>
~~~

### Modify Commit Message

~~~
git commit --amend
~~~

## Tips

- Commit messages should be based on logical units of work, not added or removed files.
