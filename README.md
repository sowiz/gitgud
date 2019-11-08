# Introduction to Git

## First-Time Git Setup

https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup#_your_identity
https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup#_your_editor

Set identity:
```shell
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```
Check config:
```shell
$ git config --list
$ git config --global user.name
$ git config --global user.email
```

It is possible to set your own configuration variables,
so make sure the variable names a written correctly.
If you make a typo and create the wrong variable just remove it with the --unset option:

```shell
$ git config --global --unset user.namw
```

## Git In A Nutshell

Git is a program for keeping track of project files. It has many powerful features.
You can go back to earlier project stages or organize your project into different branches
e.g. some-feature, development, staging, production.

When you want to develop a new feature for your application you can make a new branch of the project
and experiment in that branch without having to worry about messing up the main branch.
If a high priority issue comes up you can easily switch out of your feature branch to deal with the issue
without code from the unfinished feature getting in your way.

https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging#_basic_branching

Git has three main states that your files can reside in:
modified -> staged -> committed.

https://git-scm.com/book/en/v2/Getting-Started-Git-Basics#_the_three_states

When you commit files you create a snapshot of your project. Git will remember all the snapshots.
You can always go back to previous commits, or switch between branches with the checkout command.

When you do a checkout git will pull out files from the compressed database in the Git directory
and place them on disk for you to use or modify.

## Using A Hosted Git Repository For Collaboration

Git is a distributed version control system that makes it easy for teams to manage a codebase.

Everyone has their own local copy of the repository which makes it possible to work on the project
and persist changes to the repository even when you are offline. Git is not dependant on a central server,
but when working in teams you want to have a hosted repository that everybody can syncronize with.

There are many git hosting services.
https://git.wiki.kernel.org/index.php/GitHosting

GitHub.com and GitLab.com are popular services, they make it easy host a git repository online.
They provide additional features such as pull requests and access permissions.

GitLab's "merge request" feature is equivalent to GitHub's "pull request" feature.
Both are means of pulling changes from another branch or fork into your branch and merging the changes with your existing code.

Users with direct access can create a branch, push commits to it,
and open a merge request from their branch back into master or any other branch.

Users who don’t have push permissions for a repository can “fork” it,
push commits to their fork, and open a merge request from their fork back to the main project.

### GitLab - Merge request steps:

1. Clone/pull the latest repository from remote.
```shell
    $ git clone <url>
```
2. Create branch for new feature.
```shell
    $ git branch <feature>
    $ git checkout <feature>
```
3. Code and commit the new feature.
```shell
    $ git add .
    $ git commit -m 'feature description'
```
4. Push the 'new feature' branch to remote.
```shell
    $ git push <remote> <branch>        # e.g. git push origin feature.
```
5. On GitLab.com, create a new merge request from 'new feature' branch to 'master' branch.

Video demonstrating GitLab merge request:
https://www.youtube.com/watch?v=Ddd3dbl4-2w

https://git-scm.com/book/en/v2/Git-on-the-Server-GitLab#_working_together
https://git-scm.com/book/en/v2/GitHub-Contributing-to-a-Project

When a merge request has been created, a user with Maintainer priviliges for the repository
can choose to merge the merge request into the master branch.
Git will try to automatically merge the branches, but it is sometimes required to manually review
the merge if multiple people have been modifying the same lines of code. When this conflict occurs git
will leave in both versions of the edit and put marks around them so the maintainer can manually edit
code and choose what edits to keep.

Stackoverflow explanation of how to resolve a merge conflict:
https://stackoverflow.com/a/24103709

## Help

Reference: https://git-scm.com/docs
```shell
$ git help <command>        # Open manual.
$ git <command> -h          # Print help.
```

## Common Git Commands

```shell
$ git init  # Create an empty Git repository or reinitialize an existing one.
            # Running git init in an existing repository is safe. It will not overwrite things that are already there.
$ git clone <url>   # Clone existing repository. Adds a remote called origin for the source repository.
                    # The clone command also sets up your local master branch to track the remote master branch (or whatever the default branch is called).
                    # When tracking is set up, the "git pull" command will automatically merge the remote branch into your current branch.
$ git status        # Print modified and staged files.
$ git log           # Print project history, i.e. commits.
$ git add <files>   # Stage files to be committed.
                    # "git add ." will stage all files in the current directory and subdirectories.
                    # "git add *.c" will stage all files in the current directory with names ending in ".c".
                    # "git add" is a multipurpose command — you use it to begin tracking new files,
                    # to stage files, and to do other things like marking merge-conflicted files as resolved.
$ git commit -m "message"   # Commit staged files to repository. Use the -m flag to provide a message describing the changes.
$ git commit --amend        # Overwrite last commit. Use this option if you want to modify the last commit.
                            # You can use the -m flag to change the commit message.
$ git branch        # Print branches with current branch highlighted.
$ git branch -r     # Use the -r flag to list remote branches.
$ git branch <name> # Create a new branch. Alternatively use "checkout -b <branch>".
$ git checkout <branch>     # Switch to branch.
$ git checkout -b <branch>  # Create a new branch and switch to it.
$ git checkout -b <branch> <remote>/<branch>    # Track remote branch.
$ git pull  # Pull down all new data from remote. In simple terms "git pull" does a "git fetch" followed by a "git merge".
$ git push <remote> <branch>        # Push to remote repository from branch.
```

## More Git Commands

```shell
$ git       # Print list of common commands.
$ git reset HEAD <file>     # Unstage file.
$ git checkout -- <file>    # Revert modified (not staged) file back to how it looked in the last commit.
$ git clean -fd             # Remove untracked files from the working tree.
                            # The -f flag deletes files and directories even though the git configuration variable clean.requireForce is not set to false.
                            # The -d flag removes untracked directories in addition to untracked files.
$ git checkout <commit>     # Checkout commit into the working tree. Commits are referenced by their hash.
$ git merge <branch>        # Merge specified branch into current branch.
$ git fetch <remote>        # Pull down all new data from remote that has been added since last fetch.
                            # The fetch command doesn’t automatically merge the new data with any of your work
                            # or modify what you’re currently working on.
                            # You have to merge it manually into your work when you’re ready.
$ git branch -d     # Delete local branch. Use -D instead of -d to force deletion of an unmerged branch.
$ git push <remote> --delete <branch>   # Delete remote branch.
$ git remote        # Print remotes.
$ git remote add <name> <url>       # Add a remote repository.
$ git diff  # Print differences between modified files and staged files.
            # This tells you the changes you’ve made that you haven’t yet staged.
$ git diff --staged # Print differences between last commit and staged files.
$ git diff <commit> <commit>        # Print differences between two commits.
```
