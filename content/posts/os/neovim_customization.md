+++
title = 'Neovim_customization'
date = 2024-10-30T21:00:45+05:30
tags = [""]
author = "Me"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "Desc Text."
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

# Neovim customization

## Introduction
What is neovim? Neovim is a CLI based text editor that can be used to write documentation, write code etc. it has enough features for regulat text editing but may be lacking for the power users in the stock form, which is what we are going to do here.

## Prerequisites

- If neovim is not installed it can be installed in the following way in the following linux distors

```bash
sudo apt update -y
sudo apt install neovim -y
```

```bash
sudo dnf update -y
```

```bash
sudo pacman -Syu
sudo pacman -S neovim
```

If neovim is alreaddy installed and you already have it setup then the following configuration files may be deleted to start neovim from actual scratch.

```bash
 rm -rf ~/.local/state/nvim/
 rm -rf ~/.config/nvim/
 rm -rf ~/.local/share/nvim/
```

## First steps of configuration
- Open the configuration files, this can be opened by `cd ~/.config/`. Inside this you should make another directory called `nvim` and then you can make a file called as `init.lua`
- Inside the same directory `.config/nvim` you'll be needing another directory called `lua/` inside the lua directory it is mandatory to have ONE directory, the name of this directory can be anything.
- Tree structure for reference
```
├── init.lua
└── lua
    ├── aum
    └── init.lua
```
