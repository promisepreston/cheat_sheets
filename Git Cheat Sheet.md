# Git Cheat Sheet

Git is the open source distributed version control system that facilitates remote repositories activities on your local machine. This cheat sheet summarizes the commonly used Git command line instructions for quick reference. It saves you time when you just can't remember what a command is or don't want to use git help in the command line.

## Glossary
**git**: An open source, distributed version-control system.
**Branch**: A lightweight movable pointer to a commitclone: a local version of a repository, including all commits and branches.
**Commit**: A Git object, a snapshot of your entire repository compressed into a SHA.
**Fork**: A copy of a repository on GitHub owned by a different user.
**HEAD**: Representing your current working directory, the HEAD pointer can be moved to different branches, tags, or commits when using git checkout.
**Pull request**: A place to compare and discuss the differences introduced on a branch with reviews, comments, integrated tests, and more.
**Remote**: A common repository on that all team member use to exchange their changes.
**.gitgnore file**: Sometimes it may be a good idea to exclude files from being tracked with Git. This is typically done in a special file named `.gitignore`.

## Basic Commands
Command | Description | Example(s)
------------ | ------------- | -------------
git add `file` | Snapshot the file in preparation for versioning | git add `index.rb`
git blame `file` | Show who changed what & when in a file | git blame `file`
git clone `url` | Clone an entire repository from a remote location onto a local machine | git clone `https://github.com/promisepreston/example.git`
git commit -m `message` | Commit staged snapshots permanently in version history | git commit -m `initial commit`
git commit --amend | Modify the last commit’s message | git commit --amend
git init | Initialize the current directory as a git repository | git init
git init `directory` | Create an empty git repository in specified directory | git init `myapp`
git show `commit` | Output metadata and content changes of the specified commit | git show `4a0b8b5`
git status | List which files are staged, unstaged, and untracked | git status

## Branch Commands
Command | Description | Example(s)
------------ | ------------- | -------------
git branch | List all local branches | git branch
git branch -a | List all local branches and remote branches as well  | git branch -a
git branch `branch` | List all local branches | git branch `develop`
git branch -d `branch` | Delete a local branch | git branch -d `develop` 
git branch -m `new name` | Rename current branch | git branch -m    `stable`
git checkout `branch` | Switch to an existing branch | git checkout `develop`
git checkout -b `branch` | Create a local branch and switch to it | git checkout -b `develop`
git merge `branch` | Merge the specified branch's history into the current branch | git merge `develop`
git push origin `branch` | Push branch to remote | git push origin `develop`

## Clean Commands
Command | Description | Example(s)
------------ | ------------- | -------------
git clean -f | Delete all untracked files | git clean -f
git clean -n | Show all untracked files that would be removed from working directory | git clean -n
git clean -df | Delete all untracked files and directories    
git checkout -- | Undo local modifications to all files
git reset HEAD myfile | Unstage a file

## Config Commands
Command | Description | Example(s)
------------ | ------------- | -------------
git config --global alias.`alias-name` `git-command` | Create shortcut for a Git command | git config --global alias.`graphlog` `log --graph`
git config --global color.ui auto | Enable helpful colorization of command line output for git | git config --global color.ui auto
git config --global user.name "`name`" | Set the author name to be used for all commits by the current user | git config --global user.name "`Promise Chukwuenyem`"
git config --global user.email "`email address`" | Set the author email to be used for all commits by the current user | git config --global user.email "`promise@example.com`"
git config --system core.editor `editor` | Set text editor to be used by commands for all users on the current machine | git config --system core.editor `code`

## Difference Commands
Command | Description | Example(s)
------------ | ------------- | -------------
git diff | Show all unstaged local file changes in the working tree | git diff
git diff HEAD | Show difference between the working directory and the last commit | git diff HEAD
git diff --cached | Show difference between staged changes and last commit | git diff --cached
git diff `branch A`...`branch B` | Show difference between two branches | git diff `develop`...`stable` 
git diff `file` | Show changes made to a file | git diff `index.rb`

## Log Commands
Command | Description | Example(s)
------------ | ------------- | -------------
git log | List commit history for the current branch | git log
git log `branch A`..`branch B` | List the commits on one branch that are not on another branch. Args can be a `commit ID`, `branch name`, `HEAD` , or any other kind of revision reference. | git log `develop`..`stable`
git log -p | Display the full difference of each commit for the current branch | git log -p
git log -`N` | List commit history for last N commits | git log -`2`
git log --author="`name`" | List commit history by a particular author | git log --author="`Promise Chukwuenyem`"
git log -- `file` | List commit history that have the specified file | git log -- `index.rb`
git log --follow `file` | List commits for a file, including renames | git log --follow `index.rb`
git log --graph | Draws a text based graph of commits on left side of commit history | git log --graph
git log --grep="`pattern`" | List commit history with a commit message that matches the specified pattern | git log --grep="`initial`"
git log --oneline | List each commit history in a single line for the current branch | git log --oneline
git log --stat | List commit history for the current branch including which files were altered and the relative number of lines that were added or deleted from each of them | git log --stat

## Pull Commands
Command | Description | Example(s)
------------ | ------------- | -------------
git fetch `alias` `branch` | Download the remote copy of the specified current branch, but don't combine it into the current local branch | git fetch `origin` `master`
git merge `alias` `branch` | Combine the fetched copy of the remote branch into the current local branch | git merge `origin` `master`
git pull `alias` `branch` | Update the current local branch with all new commits from the corresponding remote branch. `git pull`  is a combination of `git fetch` and `git merge` | git pull `origin` `master`
git pull --rebase `alias` `branch` | Fetch the remote’s copy of the current branch and rebases it into the local copy | git pull --rebase `origin` `master`

## Push Commands
Command | Description | Example(s)
------------ | ------------- | -------------
git push `alias` `branch` | Upload all current local branch commits to remote branch | git push `origin` `master`
git push `alias` --all | Upload all local branches to remote repository | git push `origin` --all
git push `alias` `branch` --force | Upload all current local branch commits forefully to remote branch even if it results in a non-fast-forward merge | git push `origin` `master` --force
git push `alias` --tags | Upload all local tags to remote repository. Tags aren’t automatically pushed when you push a `branch` or use the `--all` flag | git push `origin` -tags

## Rebase Commands
Command | Description | Example(s)
------------ | ------------- | -------------
git rebase `branch` | Apply any commits of current branch ahead of specified one | git rebase `develop`

## Remote Commands
Command | Description | Example(s)
------------ | ------------- | -------------
git remote -v |
git remote add `alias` `url` | Add remote branch and its mapping to local | git remote add `origin` `https://github.com/promisepreston/example.git`
git remote remove `alias` | Remove remote branch and its mapping to local | git remote remove `origin` 
git remote set-url `alias` | Edit remote branch and its mapping to local | git remote set-url origin
git remote show `alias` | Show remote branches and their mapping to local | git remote show `origin`

## Reset Commands
Command | Description | Example(s)
------------ | ------------- | -------------
git reset | Reset staging area to match most recent commit, but leave the working directory unchanged | git reset
git reset --hard | Reset staging area and working directory to match most recent commit and overwrite all changes in the working directory | git reset --hard
git reset `commit` | Reset staging area to the specified commit, but leave the working directory unchanged | git reset `4a0b8b5`
git reset --hard `commit` | Reset staging area and working directory to the specified commitand overwrite all changes in the working directory | git reset --hard `4a0b8b5`

## Stash Commands
Command | Description | Example(s)
------------ | ------------- | ------------- 
git stash | Save modified and staged changes temporarily | git stash
git stash drop | Discard a stash from top of stash stack | git stash drop
git stash list | List stack-order of stashed file changes | git stash list
git stash pop | Apply a stash from top of stash stack and delete it from stash list | git stash pop

## Tag Commands
Command | Description | Example(s)
------------ | ------------- | -------------         
git checkout `tag` | Switch to an existing tag | git checkout `develop`
git tag | List all tags | git tag
git tag -d `tag` | Delete a tag from a local repository | git tag -d `develop`
git pull `alias` --tags | Download all remote tags to the current local branch | git pull `origin` -tags
git push `alias` --tags| Upload all local tags to remote repository. Tags aren’t automatically pushed when you push a `branch` or use the `--all` flag | git push `origin` -tags




# How to update/checkout a single file from remote origin master?

**The scenario**:
I make some changes in a single file locally and run git add, git commit and git push

The file is pushed to the remote origin master repository

I have another local repository that is deployed via Capistrano with the "remote_cache" method from that remote repository

Now I don't want to deploy the whole application but just update/checkout that single file.

**Answer**:
It can be done in the deployed repository: 

    git fetch

The git fetch command will download all the recent changes, but it will not put it in your current checked out code (working area).

    git checkout origin/master -- path/to/file

Then the checkout command will update the working tree with the particular file from the downloaded changes (origin/master).

## Resources
1. [GitHub Git Cheat Sheet](https://github.github.com/training-kit/downloads/github-git-cheat-sheet.pdf)
2. [GitHub Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
3. [BitBucket Git Cheat Sheet](https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet)
4. [GitLab Git Cheat Sheet](https://about.gitlab.com/images/press/git-cheat-sheet.pdf)
5. 



