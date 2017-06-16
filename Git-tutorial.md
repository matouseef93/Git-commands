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
# On branch master  **<-- This is the branch you are currently in**
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#	modified:   README.md  <--  Este es el archivo que se ha modificado
#
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#	fichero.cpp <--  Este es el archivo nuevo que se ha creado
#
no changes added to commit (use "git add" and/or "git commit -a")
```