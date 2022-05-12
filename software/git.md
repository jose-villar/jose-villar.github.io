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
~~~

## Reflog

~~~

// Note: It should be noted that reflogs are personal and not saved in remote
// repositories. By default reflog is kept around for 90 after which Git
// automagically deletes it. Reflogs are kept in path
// .git/logs/refs/heads/{branch}. If you’re actively using stash you should
// also remember that there is a separate reflog for stash.
// Equal to git reflog show HEAD. Shows reference changes in HEAD.
git reflog

// Shows reflog from all branches.
git reflog --all

// Shows reflog from a branch.
git reflog <branch>

// Shows reflog from stash.
git reflog stash

git reflog <branch>@{time}
// Time can be following format:
// 1.minute.ago
// 1.hour.ago
// 1.day.ago
// yesterday
// 1.week.ago
// 1.month.ago
// 1.year.ago
// 2020-01-01.09:00:00

// You can also use plural form (5.minutes.ago) and they can be combined
// (1.year.1.month.ago).
~~~

## Restore

~~~
// If the change has not been added you can just do a:
git restore .

// Discard changes from staged area (they persist in working directory)
git restore --staged <target>

// Remove file from commit but keep changes for later use
git rm -- cached <path>

// Remove from untracked
git rm --cached <target>
// Use git rm -h to see short help or --help to see the verbose version
~~~

## Inspecting

~~~
// Show commits
git log
// Show in a format designed for machine consumption.
// (--porcelain)
git log -p
git log -<n> // show last n commits
git log --oneline
git log --all --graph --decorate
git log <path> // show commits that modified certain path

// Filter commits by day
git log --after aaaa-mm-dd
git log --after="2020-11-31"
git log --after="yesterday"
git log --after="one week ago"
git log --since="one week ago"
git log --before="aaaa-mm-dd"
git log --until="aaaa-mm-dd"

git log --author="Alana"
git log --commiter="Alana"

// Show only commits where message contains certain regex
git log --grep=<regex>

// Press q to exit the commit log.

// See what files were changed on every commit
git log --stat

// Show contributions by author
git shortlog


// Shows the differences in tracked files between index and working tree
git diff

// Shows changes between specified commits or branches
git diff <commit/branch 1> <commit/branch 2>

// Shows changes between HEAD and specified commit/branch.
git diff HEAD <commit/branch>
git diff HEAD <commit/branch> -- <path>

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

## Tags

~~~
// Lists all tags in repository.
git tag --list

// Creates a new tag with a message and a name which references the commit that
the HEAD is at. We could also give third parameter for the tag which would
contain the commit.
git tag -a -m <message> <name>

// Deletes the named tag.
git tag -d <name>

// Tags need to be pushed separately to the repository if you want to make them
public. You should avoid pushing all tags because removing unwanted tags from
remote repository is a bit problematic.
git push <remote repository> <tag name>
~~~

## Various

### Blame

~~~
// Shows every line and who made latest change to that line from the specified
path.
git blame <path>

// Shows only specified lines from path. Start and end can either be integers
or regexp
git blame -L <start>,<end> <path>
~~~


### Remote Repositories

~~~
// List remote repositories
git remote -v

// Add a new remote
git remote add <name> <url>

// Remove a remote
git remote rm <name>

~~~

### Remove Branch From Remote Repository
~~~
git push <remote repository> :<branch>
// Remove branch from remote repository.
git push -d  <remote repository> :<branch>
// Before pushing branch should be removed from local repository.
git push origin :feature/create-awesome
~~~

### Index

~~~
// List files in index
git ls-files
~~~

### Do and Stage in 1 Step

~~~
git rm
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

// The -p flag let us recover hunks of the file
git checkout -p <commit/branch> -- <path>

// Restore a file to a previous version (1 commit before)
git restore --source=HEAD~1 <target file>
~~~

### Modify Commit Message

~~~
git commit --amend
~~~

### Stash

~~~
// Save changes locally, to be used later on and clean up the working
// environment
git stash [<message>]
// Restore stashed changes and deletes the stash
git stash pop [<stash_id>]
// Restore stashed changes
git stash apply
git stash apply stash@{2}
// List all saved stashes
git stash list
// Delete stash
git stash drop [<stash_id>, e.g. stash@{5}]

~~~

### Remove Old Local Branches

~~~
git branch -vv | awk '/: gone]/{print $1}' git remote update --prune | xargs
git branch -d
~~~

### Discard Local Changes

~~~
git reset --hard origin/main
~~~

### Add All Changes to Commit

~~~
git add -A
~~~


### Rename Branch

~~~
git branch -m <branch> <new_name>
~~~

### Recover Single Commit
~~~
// Replay a single commit to your repository.
git cherry-pick <SHA>
~~~

### Find common ancestor(s) between two commits

~~~
git merge-base feature/create-awesome master
~~~

## Different Git Workflows

### Feature Branch Workflow

~~~
git branch feature/create-awesome
~~~


### Gitflow Workflow

Gitflow it is best suited for projects with scheduled releases. It uses feature
branches but also has a special branch for finalizing a release and
integrations.

In addition to having a master branch you’ll also have a develop branch. Actual
releases are kept in master and are identified with tags. Develop is used for
integrating feature branches.

Feature branches are made from develop instead of master. When a feature is
complete it is integrated back to develop.

When release date is starting to get close you’ll create a release branch from
develop. After this no new features can be added to a release. Only bug fixes,
generating documentation and other release related activities are allowed in
release branch. When a release is ready to be shipped, release branch will be
merged into master branch and tagged with a version number. After this release
will be merged back into develop. A separate release branch will allow some of
the team to finalize a release while others can still focus on developing new
features.

Hotfixing a product in production can sometimes be a little tricky. You’ll
create a hotfix branch from master branch. When the fix is ready the hotfix
branch will be merged back into master and develop. After this a new version
number will be updated to master.

### Forking Workflow

In forking workflow, a remote repository is shared between multiple developers.
Every developer has their own remote repository. It’s usually utilized in open
source projects. Also some large corporations might find forking workflow
useful. This would require a separate release master or a similar person to
take care of the official remote repository. Forking workflow might also be a
bit heavy style of version control.

Developers push commits to their own remote repositories but only project
maintainers can push to official remote repository. This allows maintainers to
accept changes from other contributors without giving them a write access to
official remote repository.

As a new developer you’ll start by forking the official remote repository. The
new fork you just created will act as your public repository. Other developers
cannot push their commits to your public repository but they can pull yours. As
with other workflows the next step is to clone your public repository. In this
case your public repository is a clone of the official repository.

With other workflows you’ve had a single remote repository called origin. With
forking workflow you’ll need to add another remote repository to your local
repository. The other remote repository is the official repository of the
project. By convention it is called upstream. Adding a second remote repository
allows you to pull changes from one place and push yours to another. You’ll
pull changes from official repository and push changes to your own public
repository.

~~~
git pull upstream master

git push origin feature/feature-name
~~~

When you are ready to merge a feature into official repository the maintainer
of the repository has to pull your changes from your public repository. After
verifying that everything works fine he’ll update the official repository with
your changes. 

## Tips

- Commit messages should be based on logical units of work, not added or
  removed files.

## Error Solving

- To fix the "*Permission denied (...). Please make sure you have the correct
  access rights and the repository exists.*", you have to add the key to the
  ssh-agent: `ssh-add /path/to/my-non-standard-ssh-folder/id_rsa`. In summary,
  when `ssh-add -l` returns *The agent has no identities*, it means that keys
  used by *ssh* (stored in files such as `~/.ssh/id_rsa`, `~/.ssh/id_dsa`,
  etc.) are either missing, they are not known to *ssh-agent*, which is the
  authentication agent, or that their permissions are set incorrectly.

- To fix the "*Not something we can merge*" error, just fetch from the remote
  repository.
