+++
title = 'Apache Subversion (SVN) Basics'
date = 2025-07-22T12:18:20+07:00
tags = ["vcs", "subversion", "svn", "version control", "agile", "git"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "Learn the basics of Apache Subversion (SVN), a version control system."
disableShare = false
disableHLJS = false
hideSummary = false
searchHidden = true
ShowReadingTime = true
ShowBreadCrumbs = true
ShowPostNavLinks = true
ShowWordCount = true
ShowRssButtonInSectionTermList = true
UseHugoToc = true
[editPost]
    URL = "https://github.com/AumPauskar/blog/content/posts/"
    Text = "Suggest Changes"
    appendFilePath = true
+++

# Apache Subversion (SVN) Basics

Apache Subversion (often abbreviated as SVN) is a centralized version control system. It is an open-source tool used by software developers and other professionals to manage and track changes to files, such as source code, web pages, and documentation. At its core, SVN operates on a client-server model. A single, central repository stores all versioned files and their complete history. Users "check out" a copy of the files they need from this repository to a local working directory, make their changes, and then "commit" those changes back to the central server.

## Difference between SVN and Git?

| Feature | Git | Apache SVN |
| :--- | :--- | :--- |
| **Architecture** | Distributed | Centralized |
| **Repository** | Every developer has a full, local copy of the entire repository and its history. | There is a single, central repository. Developers check out a working copy of a specific directory or file. |
| **Offline Work** | Fully supported. You can commit, branch, and merge locally without a network connection. | Limited. Most operations (commit, update) require a connection to the central server. |
| **Branching** | Branches are lightweight and fast. They are simply pointers to a commit, making it easy to create, switch, and delete branches. | Branches are created as subdirectories inside the repository. This can make branching and merging more cumbersome and slower. |
| **Commits** | Commits are local first, then you **push** them to a remote repository. | Commits are sent directly to the central server. |
| **File Tracking** | Tracks content changes (snapshots). Renaming and moving files is done implicitly by Git. | Tracks files and directories. You must explicitly tell SVN when you move, copy, or rename a file. |
| **Binary Files** | Can be slow with large binary files that change often, as the entire file is stored in each version. | Handles large binary files more efficiently as it stores only the differences (deltas) for each version. |
| **Learning Curve** | Has a steeper learning curve due to a more complex and flexible workflow. | Generally considered easier to learn because of its simpler, centralized model. |


## SVN commands

Here are some crucial SVN commands, what they do, and their Git alternatives.

1.  svn checkout
    * Explanation: Creates a local working copy from a repository. It's the first step to start working on a project.
    * Git Alternative: `git clone`

2.  svn update
    * Explanation: Fetches the latest changes from the repository and merges them into your local working copy.
    * Git Alternative: `git pull`

3.  svn add
    * Explanation: Puts new files and directories under version control.
    * Git Alternative: `git add`

4.  svn commit
    * Explanation: Sends changes from your local working copy to the repository. The changes become visible to other users. You must provide a log message.
    * Git Alternative: `git commit` followed by `git push`

5.  svn delete
    * Explanation: Deletes a file or directory from your working copy and schedules it for deletion from the repository on the next commit.
    * Git Alternative: `git rm`

6.  svn move
    * Explanation: Moves a file or directory within the repository. It's a combination of `svn delete` and `svn copy`.
    * Git Alternative: `git mv`

7.  svn status
    * Explanation: Shows the status of files and directories in your working copy. It tells you which files are modified, added, deleted, or unversioned.
    * Git Alternative: `git status`

8.  svn log
    * Explanation: Displays commit log messages and other metadata for a file or directory.
    * Git Alternative: `git log`

9.  svn diff
    * Explanation: Shows the differences between files. You can see the changes in your local working copy or compare different revisions.
    * Git Alternative: `git diff`

10. svn branch (or `svn copy`)
    * Explanation: Creates a new branch (or tag) in the repository by copying a specific revision. SVN branches are directory-based.
    * Git Alternative: `git branch` followed by `git checkout -b` or `git checkout`

11. svn merge
    * Explanation: Merges changes from one branch into another.
    * Git Alternative: `git merge` or `git rebase`

12. svn switch
    * Explanation: Changes the working copy to point to a different URL, which is often used to switch between branches.
    * Git Alternative: `git checkout`

13. svn revert
    * Explanation: Discards local changes to a file or directory and restores it to the state it was in before you made the changes.
    * Git Alternative: `git restore` or `git checkout --`

14. svn info
    * Explanation: Displays information about a file, directory, or URL, such as the repository URL, revision number, and last author.
    * Git Alternative: `git remote show origin` or `git ls-files -v`
