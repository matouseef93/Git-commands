This is a basic tutorial of git. A more advanced one can be found [here](http://git-scm.com/book). This tutorial is based on this [Spanish version](http://asrob.uc3m.es/index.php/Tutorial_git) that I created many years ago.

Git is a version control software designed by Linus Torvalds, designed with the efficiency and reliability of maintaining application versions when there is a large number of source files. At first, Git was thought of as a low-level engine on which others could write the user interface or front end. However, Git has since become a fully functional version control system. There are some very relevant projects that already use Git, in particular, the [Linux kernel](https://github.com/torvalds/linux).

## Git Tutorial for Ubuntu

The following steps work for an Ubuntu machine. However, the procedure (order of operations) is the same for any other Distribution or Operating System.

1. The first thing is to install a Git client. Here I opted for the most basic, the text interface.
```bash
$ sudo apt-get install git
```
2. Next you will have to download the repository on which you are going to work. By default it downloads the last revision ("HEAD").
```bash
$ git clone https://github.com/miguelgfierro/codebase
```
3. As you generate content, it is not "added" to the repository. When checking the status of git by typing:
```bash
$ git status
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
$ git add file.cpp
```
4.b. Or only the latest modifications to previously added files:
```bash
$ git add -u
```
4.c. Or all files added and modified:
```bash
$ git add .
```
5. Looking at the status you will see that:
```bash
$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#	modified:   README.md
#	new file:   file.cpp
```
6. Now you have to upload everything to the local repository that is on the computer itself. This is an intermediate repository between your computer and the global repository.
```bash
$ git commit -m "I have improved my Git level!"
```
7. Finally you have to upload the changes to the global repository. In order to do this the administrator has to give you permission. You are going to push to branch `master`, which is the initial branch available when the repo is created.
```bash
$ git push origin master
```
8. To download the latest version of the server:
```bash
$ git pull origin master
```
## Git configurations

Initial settings to enter your name and email (git will advise if necessary). To configure your user in all PC repositories:
```bash
$ git config --global user.name "Mitch Buchannon"
$ git config --global user.email iammitchbuchannon@users.noreply.github.com
```
*Tips and tricks: the alias `your-github-username@users.noreply.github.com` is a the default hidden email in Github*.