+++
title = 'Git and GitHub cheatsheet'
date = 2023-11-25T09:46:03+05:30
draft = false
tags = ["git", "github", "version control", "cheatsheet"]
author = "Aum Pauskar"
description = "A basic cheatsheet of git and github commands"
+++

# Git / github cheatsheet

## Installation of git
1. Download git from [here](https://git-scm.com/downloads)
	- or use on debian based linux
		```bash
		sudo apt update
		sudo apt install git
		```
2. Check if git is installed
	```bash
	git --version
	```
3. Configure git
	```bash
	git config --global user.name "Your Name"
	git config --global user.email "Your email"
4. (Optional) Change the default brach name from `master` to `main`
	```bash
	git config --global init.defaultBranch main
	```
5. Configuring SSH keys to github \
	Run these commands on the terminal
	```bash
	ssh-keygen -t ed25519 -C "$Your email"
	eval "$(ssh-agent -s)"
	ssh-add ~/.ssh/id_ed25519
	cat ~/.ssh/id_ed25519.pub
	```
	Go to [Github](https://github.com/)>[Settings](https://github.com/settings/profile)>[SSH and GPG keys](https://github.com/settings/keys). Click on New SSH key. Give a title and paste the key in the key field. Click on Add SSH key. The key should be available from the last command on the terminal.
## Git commands
1. `git init` - initialize a git repository
2. `git add <file>` - add a file to the staging area
3. `git add .` - add all files to the staging area
	- `git add -A` - add all files to the staging area
4. `git commit -m "message"` - commit changes to the local repository
5. `git push` - push changes to the remote repository
	- `git push -u origin <branch_name>` - push changes to a branch
	- `git push origin <branch_name>` - push changes to a branch
6. `git pull` - pull changes from the remote repository
	- `git pull origin <branch_name>` - pull changes from a branch
7. `git status` - check the status of the repository
8. `git log` - view the commit history
9. `git branch` - view the branches
10. `git branch <branch_name>` - create a new branch
11. `git checkout <branch_name>` - switch to a branch
12. `git checkout -b <branch_name>` - create and switch to a branch
13. `git merge <branch_name>` - merge a branch into the current branch
14. `git clone <url>` - clone a remote repository
15. `git remote add origin <url>` - add a remote repository
16. `git remote -v` - view the remote repositories
17. `git remote set-url origin <url>` - change the url of the remote repository
18. `git remote remove origin` - remove the remote repository
19. git submodule: git submodule is used to add a git repository inside another git repository. This is useful when you want to use a git repository inside another git repository. For example, you can use git submodule to add a git repository that contains a library to your project. This way, you can use the library in your project without having to copy the library files into your project directory.
	- `git submodule add <url>` - add a submodule
	- `git submodule init` - initialize the submodule
	- `git submodule update` - update the submodule
	- `git submodule update --remote` - update the submodule to the latest commit