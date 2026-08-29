+++
title = 'Archlinux liveboot'
date = 2026-08-29T03:35:20Z
tags = ["os", "dualboot", "linux", "liveboot", "arch"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "A document on how to set up live booting in a usb drive"
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

# Archlinux liveboot

## Introduction to liveboot

## Requirements

- A USB drive 8gb+ (preferably with usb 3.0 transfer speeds)
- Host machine with rufus installed

## Installing Rufus and Arch ISO

- Arch iso
    - Visit [here](https://archlinux.org/download/)
    - Download the iso via BitTorrent to ensure maximum speed and help to seed to others

- Rufus 
    - Visit [here](https://rufus.ie/en/), windows only. Or for linux machines you can use balena etcher.
    - Use the following setup in Rufus
        - Device: USB Stick
        - Boot selection: Your arch iso
        - Persistent partition size: 0gb (we'll set the persistent storage from the arch window)
        - Partition scheme: MBR, we're targeting maximum number of systems with both BIOS and UEFI compatiblity.
        - Keep the rest of the settings as it is

## Booting into the USB

- Hold the boot key or the BIOS/UEFI key (could be F2, F8 or F10, check your motherboard manufacturer), in case of my Asus it was F2.
- Depending on the BIOS/UEFI software, you either need to change the boot order or boot into the USB drive
- After selecting it wait till you see a terminal

## Initial arch setup

- After booting into the arch terminal, wifi may not work which is essential for the intial setup, for this check iwctl.
- Ethernet will work out of the box and so does USB thethering, so if you don't want to deal with iwctl commands use either one of these
- Run the archinstall script, by typing `archinstall`

## Archinstall setup

- Disk configuration: Use the usb as the target drive **WARNING: INCORRECT DISK CONFIGURATION WILL WIPE YOUR HOST MACHINE**
![disk configuration](https://raw.githubusercontent.com/AumPauskar/repo-media/main/blog/os/liveboot/storage_partitioning.jpg)
- Hostname: Set your device
- Disable swap - since we are using a USB disk, hit times and data transfer speed is already bottlenecked
![swap configuration](https://raw.githubusercontent.com/AumPauskar/repo-media/main/blog/os/liveboot/swap.jpg)
- Set up auth and password for host machine
- Set up user and password for a user and if you intend for using it also add it as a superuser
![user auth](https://raw.githubusercontent.com/AumPauskar/repo-media/main/blog/os/liveboot/user_authentication.jpg)
- Set up bootloader as grub, systemmd would work as well but may not be compatible with computers not having UEFI
![bootloader setup](https://raw.githubusercontent.com/AumPauskar/repo-media/main/blog/os/liveboot/bootloader.jpg)
- Set up applications
    - Enable bluetooth
    - Set audio interface to pipewire
    - Keep everything else as default if you are unsure
- Graphic drivers: For our setup we went with all open source
- Profile: Set it up as a desktop profile and for USB where we aim for least amount of resources used we can set profile as XFCE.
![os profile](https://raw.githubusercontent.com/AumPauskar/repo-media/main/blog/os/liveboot/desktop_profile.jpg)
- Greeter: Any one is fine but we've used sddm
- Disable automatic time sync, if you are using windows
- In Network configuration set it up as set default backend to ensure that the setup targets maximum number of systems
![network config](https://raw.githubusercontent.com/AumPauskar/repo-media/main/blog/os/liveboot/network_configuration.jpg)
- After setup, confirm your settings and select install. Installation process may take around 30 minutes depending on your internet speed.

## Post installation
### Greeter setup
When the greeter asks you for username and password, check on the top left side, it should say XFCE (Wayland) or just XFCE. If it's XFCE wayland, ensure it's set back to XFCE. On some computers XFCE (Wayland) may result in no display outputs and your monitor may remain inactive with the above given configurations.

### Important applications
With this minimal desktop installation of Arch + XFCE many applications will not work on your system so you can use the following commands with pacman to run it.

- System packages upgrade
```bash
sudo pacman -Syu
```

- Firefox - web browser
```bash
sudo pacman -S firefox
```

- Git and vim (must haves)
```bash
sudo pacman -S git vim
```

You can also set up AUR by clicking [here](https://aumpauskar.github.io/blog/posts/os/dualboot/#aur)\
For ZSH setup click [here](https://aumpauskar.github.io/blog/posts/os/dualboot/#my-installed-pacman-packages)