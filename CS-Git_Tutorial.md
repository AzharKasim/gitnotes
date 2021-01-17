Corey Schafer
# Git Tutorials
[Playlist](https://www.youtube.com/playlist?list=PL-osiE80TeTuRUfjRe54Eea17-YfnOOAx)


# Git Tutorial for Beginners: Command-Line Fundamentals

Distributed Version Control System

First time set up
    git --version

Set config values
    git config --global user.name "<name>"
    git config --global user.email "<email>"

Need help?
    git help <verb>
    git verb --help
    git verb -h
    man git verb

## Getting Started
Two common scenarios


1. Initialize a repo from existing code
    git init

2. Clone a repo from somewhere else
    git clone
    git clone <url>

To stop tracking a project
remove the git directory
    rm -rf .git

Before first commit
    git status

Add gitignore file
    touch .gitignore

3 stages
1. Working Directory
2. Staging Area
3. .git directory (Repository)

Add file to staging area
    git add <file>

Add all files to staging area
    git add -A

Remove file from staging area
    git reset <file>

Remove everything from staging area
    git reset

Commit 
    git commit -m "<message>"

View commit history
    git log

## Working with remotes
Clone a remote repo
    git clone <url>
    git clone <url> .
    git clone <url> <where to clone>

Viewing information about the remote repository
    git remote -v

Pushing changes
Commit changes 
    git add <files>
    git commit -m "<message>"

Then Push
The code on the repo may have been updated. Update ours first
    git pull <remote> <branch>
    git pull origin master
    
    git push <remote> <branch>
    git push origin master

## Common Workflow

View all branches 
    git branch -a

1. Create a branch for desired feature
    git branch <branchname>

2. Move onto the branch
    git checkout <branchname>

3. Make your changes
    git commit -m "<new code>"

4. After commit, push branch to remote
    git push -u <remote> <branch>

5. Merge a branch
    git checkout master
    git pull origin master
    git branch --merged
    git merge <feature branch>
    git push origin master
    git push --delete <feature branch>

    git checkout < main branch>
    git pull <remote> <feature branch>
    git merge <feature branch>
    git push <remote> <branch>
    git push <remote> --delete <branch> 

# Git Tutorial: Fixing Common Mistakes and Undoing Bad Commits

##1 
Suppose that we have made changes to a file. 
The file has not yet been staged and we don't want those changes.
`git status` will show that file has been modified but it has not yet been staged.
Running `git diff` will show the changes that we have made but not want to stage and commit.
We can run `git checkout <file>` to reset the file to the latest version in the previous commit.
Running `git status` again will show that our working directory is clean.
If we run `git diff` again, we will not see any changes between the file in the working tree and the staging area.

##2 We made a git commit but messed up the commit message.
    git commit --amend -m "<amended> message"

This will change the hash as the commit message is part of the commit.
But if we are the only one who has seen the changes, this is acceptable.

##3 Accidentally left out a file in the commit.
    git commit --amend 

This will change the hash as well.

##4 Commit to the wrong branch. (Example, master instead of feature branch).

View the commit history, copy the abbrev commit.
    git log
    git checkout <feature-branch>
    git cherry-pick <hash>
    git checkout <master>

1. 
    git reset --soft <hash>

This will remove the commit(<hash>) but keep the changes we have made in the staging area.

2. default

    git reset <hash>

This will remove the commit(<hash>) but keep the changes in the working directory instead of stagin area.

3. 
    git reset --hard <hash>

This will remove the commit(<hash>). Reverts all the tracked file to the state that they were in. But it will leave the untracked files alone.

To get rid of the untracked files, run
    git clean -df

`-d` gets rid of untracked directory. `-f` gets rid of untracked files.


##5 `git reset --hard` gets rid of unwanted changes. But suppose we want some of the changes.

It depends on whether git has deleted the information history (git garbage) \\ To read on this
Shows commits in the order of we last reference it
    git reflog

    git checkout <hash>

In detached head state, we are not on a branch. Create a branch.
    git branch <back up>
    git branch

The changes will be in the branch `<back up>`.

##6 Suppose we want to undo some commits but other people has pulled those commits.

Grab the hash of the commit undo
    git revert <hash>

Git finds out the changes from the commit we want to undo, reverse it and makes a new commit.


# Git Tutorial: Using the Stash Command

    git stash save "<message>" 
    git stash list

    git stash apply stash@{0} 

    
Grab first stash, apply those changes and drop the stash
    git stash pop

    git stash drop stash@{n}

    git stash clear

To reset
    git checkout -- .

This can be useful if you have a situtation where you made changes on, say, master branch when you should have made those changes in a feature branch instead. You can stash those changes, checkout the feature branch and then apply those changes from the stash.

# Git Tutorial: Diff and Merge Tools

    git diff

    diffmerge

# Git Tutorial: Difference between "add -A", "add -u", "add ." and "add *"

To unstage all staged files
    git reset


Suppose we have the following conditions:
    a new file:   ./gitignore
    a deleted:    deleted.txt
    a modified:   modified.txt
    a deleted:    my_dir/deleted.txt
    a modified:   my_dir/modified.txt  
    a new_file:   new_file.txt
    a new_file:   my_dir/new_file.txt


Stage all added, modified, deleted in entire working tree.
That is, in the current working directory and sub-directories.
    git add -A, -all, --no-ignore-removal

Using `git add -A` from within a sub-directory will also stage files from the top-level-directory.


Stage only all files added, modified, deleted within a sub-directory but not the top-level directory.
    git add -A <sub-directory>

-A is the default flag
    git add <sub-directory>

This is new to git version 2. In git version 1, the deleted files are ignored.

If you still want the deleted files to be ignored
    git add --no-all <sub-directory>

    git add --ignore-removal <sub-directory>


Stage all modified and deleted files but not any new untracked files for the entire tree.
    git -u, --update

Stage all modified and deleted files only in the sub-directory
    git add -u <sub-directory>


`git add .` is not the same as `git add -A`


`git add .` is the same as `git add -A` in the top directory

It is different when used in a sub-directory.
Running `git add .` in a sub-directory is the same as running `git add -A <sub-directory>`
Only the files within the sub-directory is added to the staging area.


`git add *` 

`*` is a shell command, not a git command.
Git may not find the deleted files or hidden files.
A deleted file in a sub-directory will get detected but not in the parent directory.

Running `git add *` will also not add files in the parent directory. Only the files the shell can see.







