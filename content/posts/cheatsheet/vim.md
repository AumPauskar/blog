+++
title = 'Vim'
date = 2024-05-15T12:26:55+05:30
tags = [""]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "A small cheatsheet of vim commands"
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

| Sr. No. | Command | Description |
| --- | --- | --- |
| 1 | `:q` | Quit |
| 2 | `:q!` | Quit without saving |
| 3 | `:w` | Save |
| 4 | `:wq` | Save and quit |
| 5 | `:wq!` | Save and quit without saving |
| 6 | `:e` | Open file |
| 7 | `:e!` | Discard changes |
| 8 | `:e <filename>` | Open file |
| 9 | `:e! <filename>` | Discard changes |
| 10 | `:sp` | Split window horizontally |
| 11 | `:vsp` | Split window vertically |
| 12 | `:q` | Quit window |
| 13 | `:tabnew` | Open new tab |
| 14 | `:tabn` | Next tab |
| 15 | `:tabp` | Previous tab |
| 16 | `:tabc` | Close tab |
| 17 | `:tabo` | Close other tabs |
| 18 | `:tabm` | Move tab |
| 19 | `:tabfirst` | First tab |
| 20 | `:tablast` | Last tab |
| 21 | `:tabe` | Edit tab |
| 22 | `:tabfind` | Find tab |
| 23 | `:tabclose` | Close tab |
| 24 | `:tabonly` | Close other tabs |
| 25 | `:tabmove` | Move tab |
| 26 | `:tabnext` | Next tab |
| 27 | `:tabprevious` | Previous tab |
| 28 | `:tabedit` | Edit tab |
| 29 | `:set number` | Show line numbers |
| 30 | `:set nonumber` | Hide line numbers |
| 31 | `:set relativenumber` | Show relative line numbers |
| 32 | `:set norelativenumber` | Hide relative line numbers |
| 33 | `:set list` | Show whitespace characters |
| 34 | `:set nolist` | Hide whitespace characters |
| 35 | `:set listchars=tab:>-,trail:.` | Set whitespace characters |
| 36 | `:1` | Go to line 1, may be changed by adding approprite number |
| 37 | `:$` | Go to last line |
| 38 | `:!` | Run shell command, may be used to test program |
| 38.1 | `! gcc -o test test.c` | Compile C program |
| 38.2 | `! ./test` | Run C program |
| 39 | `dd` | Delete line (copy in clipboard) |
| 40 | `yy` | Copy line |
| 41 | `p` | Paste line |
| 42 | `u` | Undo |
| 43 | `Ctrl + r` | Redo |
| 44 | `Ctrl + w` | Delete word |
| 45 | `Ctrl + u` | Delete line |
| 46 | `Ctrl + y` | Scroll up |
| 47 | `Ctrl + e` | Scroll down |
| 48 | `Ctrl + f` | Page down |
| 49 | `Ctrl + b` | Page up |
| 50 | `Ctrl + d` | Half page down |
| 51 | `Ctrl + u` | Half page up |
| 52 | `Ctrl + o` | Go to previous location |
| 53 | `Ctrl + i` | Go to next location |
| 54 | `Ctrl + g` | Show file information |
| 55 | `Ctrl + l` | Refresh screen |
| 56 | `Ctrl + a` | Increment number |
| 57 | `Ctrl + x` | Decrement number |
| 58 | `Ctrl + v` | Enter visual block mode |
| 59 | `v` | Enter visual mode |
| 60 | `V` | Enter visual line mode |
| 61 | `i` | Enter insert mode |
| 62 | `a` | Enter insert mode after cursor |
| 63 | `o` | Enter insert mode after line |
| 64 | `O` | Enter insert mode before line |
| 65 | `:` | Enter command mode |
| 66 | `/` | Search forward |
| 67 | `?` | Search backward |
| 68 | `n` | Next search result |
| 69 | `N` | Previous search result |
| 70 | `*` | Search word under cursor |
| 71 | `esc` | Exit mode |
| 72 | `gg` | Go to first line |
| 73 | `G` | Go to last line |