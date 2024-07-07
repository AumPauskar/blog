+++
title = 'Dualbooting windows and linux'
date = 2024-07-07T11:26:50+05:30
tags = ["os", "dualboot", "linux", "windows"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "A guide to dual booting Windows and Linux (fedora)"
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

# Dualbooting windows and linux

## About the hardware I'm using
I am using an Asus TUF Gaming A15 laptop with Ryzen 7 5800H and RTX 3060, with 2 SSDs, one 512GB and one 1TB. I have windows installed on the 512GB SSD and I want to install Fedora on the 1TB SSD.

## Prep
- Ensure secure boot is off
    - To disable secure boot go to the bios/uefi and disable it. Every laptop has a different way to access the bios/uefi, so you might have to look it up.
    - (Optional) Disable fast boot
- Download the Fedora ISO from the [official website](https://fedoraproject.org/workstation/download)
- Use a tool like [Rufus](https://rufus.ie/) to create a bootable USB drive. I've used Raspberry Pi Imager on Windows and dd on Linux to create bootable USB drives.
- Backup your data. There is always a risk of data loss when installing a new OS.
- Open disk management on windows and shrink the volume of the drive you want to install Fedora on. I have a 1TB SSD and I've shrunk by 100GB. This will create unallocated space where Fedora will be installed.

## Installing Fedora
- Boot from the USB drive, this can be done via the bios boot menu or by changing the boot order in the bios. The hotkey for bios or boot menu is different for every laptop, so you might have to look it up.
- Select "Start Fedora 40" and press enter.
- Do the setup and continue
- In the installation screen select the unallocated SSD, and hit install. You can also create partitions manually if you want to.

## Post installation
- After the installation fedora 40 most likely has installed a bootloader which will automatically prompt you a menu to select the OS you want to boot into.