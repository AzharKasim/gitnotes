Codecademy 
How to push code to github
[Video](https://www.youtube.com/watch?v=wrb7Gge9yoE)


Suppose we have a local repository on our system.
1) Create a repository on github.
2) Copy the remote repository URL.

3)
    git remote add origin <url>
    git push -u origin master

For every branch that is up to date, or successfully pushed, add upstream (tracking) reference, used by argument-less, `git pull` and other commands. 
    git push -u <remote name> <branch name>
    -u, --set-upstream

Add a remote named <name> for the repository at <url>. The command `git fetch <name>` can then be used to create and update remote-tracking branches <name>/<branch>.
    git remote add <remote name> <url>
