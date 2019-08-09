This is a basic tutorial of git. A more advanced one can be found [here](http://git-scm.com/book). This tutorial is based on this [Spanish version](http://asrob.uc3m.es/index.php/Tutorial_git) that I created many years ago.

Git is a version control software designed by Linus Torvalds, designed with the efficiency and reliability of maintaining application versions when there is a large number of source files. At first, Git was thought of as a low-level engine on which others could write the user interface or front end. However, Git has since become a fully functional version control system. There are some very relevant projects that already use Git, in particular, the [Linux kernel](https://github.com/torvalds/linux).

## Begin from the beginning

The first step is to be able to download a repository, add files and send these files back to the repository.

1. The first thing is to install a Git client. This is the instruction for Ubuntu, but you can install them in [other operating systems](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git). 
```bash
sudo apt-get install git
```
2.a. Next you will have to download the repository on which you are going to work. By default it downloads the last revision ("HEAD").
```bash
git clone https://github.com/miguelgfierro/codebase
```
2.b. Alternatively, you can create a new repository. 
```bash
cd /path/to/your/folder
git init
```
3. As you generate content, it is not "added" to the repository. When checking the status of git by typing:
```bash
git status
# On branch master  <-- This is the branch you are currently in
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#	modified:   README.md  <--  This is the modified file
#
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#	file.cpp <--  This is the new file created
#
no changes added to commit (use "git add" and/or "git commit -a")
```
4.a. You can add a file:
```bash
git add file.cpp
```
4.b. Or only the latest modifications to previously added files:
```bash
git add -u
```
4.c. Or all files added and modified:
```bash
git add .
```
5. Looking at the status you will see that:
```bash
git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#	modified:   README.md
#	new file:   file.cpp
```
6. Now you have to upload everything to the local repository that is on the computer itself. This is an intermediate repository between your computer and the global repository.
```bash
git commit -m "I have improved my Git level!"
```
*Tips and tricks: You can do `$ git commit -a -m = "I have improved my Git level!"`, this also uploads files marked as modified, without having to re-do `git add`*.

7. Finally you have to upload the changes to the global repository. In order to do this the administrator has to give you permission. You are going to push to branch `master`, which is the initial branch available when the repo is created.
```bash
git push origin master
```
8. To download the latest version of the server:
```bash
git pull origin master
```
## Git configurations

Initial settings to enter your name and email (git will advise if necessary). To configure your user in all PC repositories:
```bash
git config --global user.name "Bruce Wayne"
git config --global user.email iambatman@users.noreply.github.com
```
*Tips and tricks: the alias `your-github-username@users.noreply.github.com` is a your default hidden email in Github*.

To configure your user in a single repository:
```bash
git config user.name "Bruce Wayne"
git config user.email iambatman@users.noreply.github.com
```
To view the user and email configured in the repository:
```bash
git config user.name
git config user.email
```

## Basic management of branches

The branches are used to develop in parallel to the main repository. When you create a new functionality in the code, you should create a branch. Then you develop the functionality, test it and when it **works perfectly** is integrated into the main branch (which is usually the master branch).

*Tips and tricks: In master there should always be working code, please don't be the guy who sends breaking code to master, karma will hunt you!*

1. View the state of the branches
```bash
git branch  <-- This tells you the branches in your local repository
git branch -a  <-- It tells you the branches in local and global repositories (listed as remotes/origin/...)
git fetch -p  <-- Update the list of branches taking into account remote branches deleted by other people
```
2. Create and upload/download a branch
```bash
git branch testing <-- Create a new branch in the local repository called testing 
git checkout testing <-- Change from the current branch to testing branch (can be done whenever you want to change branches)
git add new_file.cpp <-- We add a new file in the testing branch
git commit -m "added new_file.cpp to the testing branch" <-- commit local repository
git push origin testing <-- upload changes to the global repository (if you are prompted to do something else, do so)
git pull origin testing <-- you can download the latest changes from the global repository to your computer
```
3. If you want to merge a branch (eg testing) with the master branch 
```bash
git checkout master <-- changes from the current branch to the master branch
git merge testing <-- merge the testing branch with the main
```
4. Delete a branch (eg testing, which would make sense after the merge) you have to do the next two steps
```bash
git branch -d testing <-- locally clears the testing branch
git push origin --delete testing <-- delete the testing branch in the global repository
```
When working with branches, many times you have lots of local branches that have been already merged in remote, but you still have them in local. To [delete them](https://stackoverflow.com/questions/7726949/remove-tracking-branches-no-longer-on-remote/28464339#28464339) (with a file review before you delete them):
```bash
git branch --merged >/tmp/merged-branches && vi /tmp/merged-branches && xargs git branch -d </tmp/merged-branches
```
5. Another good practice is to tag locate an important point of your code is to make a "tag". Typically this is done when you want to make a release.
```bash
git tag <-- shows a list of all tags
git show 1.0 <-- shows detailed tag information called v1.0
git tag -a 1.0 -m "version 1.0: first release" <-- creates a tag named v1.0 in the local repository
git push origin 1.0 <-- upload the tag to the remote server
```
6. In some situations there can be conflicts. A conflict occurs when two developers have modified the same file at the same time and then server doesn't know which is the final version of the file. The conflicts usually appear after pulling a branch and are visible when you see the status:
```bash
git status
# On branch master
# You have unmerged paths.
#   (fix conflicts and run "git commit")
#
# Unmerged paths:
#   (use "git add ..." to mark resolution)
#
# both modified:      file.cpp
```
To solve this you can open the file and manually fix the conflicts. Alternatively, you could choose to maintain the version of the global server
```bash
git checkout --theirs file.cpp
```
or you choose your local version
```bash
git checkout --ours file.cpp
```
7. A good way to avoid conflicts when developing in branches is to [rebase](https://git-scm.com/book/en/v2/Git-Branching-Rebasing). Put in simple words, when rebasing you are telling git to automatically solve the conflicts generated when two developers are modifying the same file locally, with a not up-to-date repo version. This behavior typically appears when you pull the last changes of a repo and another developer has modified a file at the same time. A nice explanation can be found [here](https://gist.github.com/leesmith/8441773). To avoid this conflict, you can rebase when pulling:
```bash
git pull --rebase origin master
```  
8. Sometimes you have modified files in a branch, but you would like to [move these changes](https://stackoverflow.com/questions/7217894/moving-changed-files-to-another-branch-for-check-in/7218106) to a different branch. Using `git stash` you can save your changes locally, switch the branch and make the changes available again.  
```bash
git stash
# Saved working directory and index state WIP on master: 654088c message of the previous commit
git checkout new_branch
git stash pop
```

## Roll back to a previos version of the repo
In git is easy to roll back to a previous version of your repo, for that we only need the identifier of the commit. First we need to find the commit we want to roll back:
```bash
git log
# commit 8af5d69e4bbc9aec8b5e268e2ba94c49fbffee37 <- this is the commit hash
# Author: Miguel Fierro <miguelgfierro@users.noreply.github.com>
# Date:   Fri Jun 16 08:27:17 2017 +0100
#
#     clean string js fix #76
# commit 8168c0c18c28488b0d1cf12c98f93ebc4f1e40e1
# Author: Miguel Fierro <miguelgfierro@users.noreply.github.com>
# Date:   Fri Jun 16 08:21:20 2017 +0100
#
```
To roll back to a specific commit:
```bash
git checkout 8af5d69e4bbc9aec8b5e268e2ba94c49fbffee37 
```
In case you have a repo with submodules, which are different subrepos whithin the main repo ([more info here](https://git-scm.com/book/en/v2/Git-Tools-Submodules)), you need to update them:
```bash
git submodule update --recursive
```

## Statistics

This [script](python/utilities/git_stats.py) has several statistics for GitHub repos.

Statistics of commits:
```bash
git rev-list HEAD --count <-- allows you to see the total number of commits
git shortlog -sne <-- allows to see the number of commits of each developer
```
Count number of lines. Some of the following statistics are computed with [CLOC](https://github.com/AlDanial/cloc) using `npm install -g cloc`. An alternative to CLOC is [linguistic](https://github.com/github/linguist), which is the library used by GitHub to get code statistics:
```bash
git ls-files | xargs cat | wc -l <-- total number of lines (including comments)
git ls-files | xargs wc -l <-- number of lines per file
cloc --vcs=git <-- number of files and code statistics (code, blanks and comments)
cloc --git --diff b35dfc0866bce3bcf284b9eeecf3fa50b54a9691 HEAD <- differences in code statistics of a commit and current master
```
Statistics of number of lines per developer:
```bash
git log --format='%aN' | sort -u | while read name; do echo -en "$name\t"; git log --author="$name" --pretty=tformat: --numstat | awk '{ add += $1; subs += $2; loc += $1 - $2 } END { printf "added lines: %s, removed lines: %s, total lines: %s\n", add, subs, loc }' -; done
```
Show the number of added, removed and total lines:
```bash
git log  --pretty=tformat: --numstat | awk '{ add += $1 ; subs += $2 ; loc += $1 - $2 } END { printf "added lines: %s removed lines: %s total lines: %s\n",add,subs,loc }'
```
Show an sorted list of the repo elements with their size and commit
```bash
git rev-list --objects --all | git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' | awk '/^blob/ {print substr($0,6)}' | sort --numeric-sort --key=2 | cut --complement --characters=13-40 | numfmt --field=2 --to=iec-i --suffix=B --padding=7 --round=nearest
```
Other statistics:
```
git ls-remote --heads origin | wc -l <-- number of active branches
```

## Other commands
Next a list of useful commands:

```bash
git diff <-- shows differences between a modified file and one that has been modified before but is stagged, i.e. it is in the local repository.
git diff --cached <-- differences between a modified file and the same file saved in the HEAD
git rm file.txt <-- delete a file
git mv file.txt new_file.txt <-- rename a file
git log <-- view commit history
git log --since=2.weeks <-- view commit history from 2 weeks ago
git log --reverse <-- view the commit history in reverse order, starting with the first commit
git config --global alias.ci commit <-- alias for not having to type `git commit` and just do `git ci`
git config --global alias.st status <-- alias not to have to type `git status` and just do `git st`
git config --global core.excludesfile ~ / .gitignore <-- within `.gitignore` you list the files to be ignored
git config --global credential.helper cache <-- save your password in cache for 15 min, so you do not have to write it over and over again
git config --global credential.helper 'cache --timeout=3600' <-- save your password for one hour
git revert <commit hash> <-- Reverts a commit hash
git fetch origin <-- this command along with the one below removes all local changes and sets the server version.
git reset --hard origin/master
```


Happy gitting!