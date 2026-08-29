+++
title = 'Gparted - a graphical utility to re-partion your drive'
date = 2026-08-29T12:19:17Z
tags = ["os", "storage", "linux"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "Using gparted to repartion and reassign your device storage"
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

# GParted

Suppose you have a dual boot system of Windows and a linux operating system and you need to repartition the drive or maybe expand the storage on the linux os, with Gparted you can do this

## Requirements

- A USB stick (gen 3 with a live os environment). Learn how to get a usb with a live OS running from [here](https://aumpauskar.github.io/blog/posts/os/arch-linux-liveboot/)
- Enough storage on your machine

## Setting up the windows machine
- Open disk manager
- Select the disk where you need to expand the linux os
- Click shrink

## Live booting into OS
- Shutdown the PC
- Use the live boot usb environment, doesn't matter what sort of linux OS you are running. But we are assuming you are using arch as per the manual.
- Install `gparted` via this command
    ```bash
    sudo pacman -Syu gparted
    ```

## Working with gparted
- Open the application
- Click on the the EFI Partition
    - Right click and press Resize/Move
    - Move the storage unit towards the left side
    - Ensure the EFI Partiton is just moved and not resized
- Click on the Arch partition
    - Right click and press Resize/Move
    - Expand the storage space to consume all of the unallocated storage space
- Verify and click apply **WARNING: Data corruption may occur if incorrectly done, always back up your data**

^ image addition pending

## Post gparted
- Shut down the system
- Remove your USB stick
- Boot into your dualboot os
- Open a terminal and type in `df`, check if the storage is increased
- congratulations, you have shifted storage allocations using gparted and expand your total storage in one of your OSes