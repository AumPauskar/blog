+++
title = 'Minimalist XFCE Ricing'
date = 2026-09-01T12:30:12Z
tags = ["xfce", "linux", "arch", "archlinux", "ricing"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "A basic guide on how to customize your Arch linux + XFCE desktop to make it look good"
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
    URL = "https://github.com/AumPauskar/blog/blob/main/content"
    Text = "Suggest Changes"
    appendFilePath = true
+++

# Minimalist XFCE ricing

This guide is targeted for users who want to do a minalmalistic archlinux installation - USB liveboot, memory constraint or zen users. So we'll keep it simple

## Prerequisites

1. Archlinux installtion with XFCE DE
2. An archiever
    - XArchiever would do good, since its bundled in the DE. Here is how you install it if it's not already bundled.
        ```bash
        sudo pacman -Syu xarchiver
        ```
    - You'll also need to have zip compatiblity. Here is how you do it
        ```bash
        sudo pacman -Syu zip unzip p7zip
        ```

## Modifying the DE

### Installing a theme

We are going to install Darcula for this one.