+++
title = 'Using a plex server for media streaming'
date = 2024-04-14T16:53:10+05:30
tags = ["plex", "server", "raspberry pi", "multimedia"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "Article shows how to use a raspberry pi as a plex server for media streaming"
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

# Using a plex server for media streaming

## What is a plex server?
Plex is a client-server media player system and software suite comprising two main components. The Plex Media Server desktop application runs on Windows, macOS, and Linux-compatibles including some types of NAS devices. The server desktop application organizes video, audio, and photos from a user's collections and from online services, enabling the players to access and stream the contents.

## Why use a plex server?
Plex is a great way to stream your media content to any device. It is a great way to organize your media content and stream it to any device. Plex is a great way to stream your media content to any device. It is a great way to organize your media content and stream it to any device.

## Components required
- Any computer, lower the power consumption, the better (raspberry pi is a great option)
- A LAN/WLAN connection
- SD card
- Additional storage (optional)

## Setting up the plex server
- Update the raspberry pi
    ```bash
    sudo apt update
    sudo apt upgrade -y
    ```

- Package to update apt via https
    ```bash
    sudo apt install apt-transport-https
    ```

- Add the plex repository to the system
    ```bash
    curl https://downloads.plex.tv/plex-keys/PlexSign.key | gpg --dearmor | sudo tee /usr/share/keyrings/plex-archive-keyring.gpg >/dev/null
    echo deb [signed-by=/usr/share/keyrings/plex-archive-keyring.gpg] https://downloads.plex.tv/repo/deb public main | sudo tee /etc/apt/sources.list.d/plexmediaserver.list
    ```

- Update mirrors and install plex server
    ```bash
    sudo apt update
    sudo apt install plexmediaserver -y
    ```
- Reboot the system
    ```bash
    sudo reboot
    ```
- Make sure the plex server is running
    ```bash
    sudo systemctl status plexmediaserver
    ```
- Open the browser and enter the ip address of the raspberry pi followed by the port number 
    ```bash
    <ip_address>:32400/web
    ```
- Now you must sign in to your plex account or create a new one

## Adding media to the plex server
Media can be added to the plex server by following these steps:
- Open the plex server in the browser
- Go to the following path
    settings > manage > libraries > add library
- Select the type of media you want to add
- Select the folder where the media is stored
- Click on add library
