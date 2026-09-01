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

- Downloading a theme\
    We are going to install Darcula for this one. Just search for [XFCE-look](https://www.xfce-look.org/) on any search engine and open. Now click on GTK3/4 themes, and search for [Darcule](https://www.xfce-look.org/p/1687249). Click on download.

- Making the themes folder\
    Open a file explorer. Ensure that hidden files are visible and check if `.themes` files are present. If not present, create a folder called `.themes`. 
- Installing the theme
    - Open settings > appearance > themes and click on the theme to extract.
    - If that didn't work then extract the folder zip into the `.themes` folder and try it that way.

### Installing icons

- Downloading the icons\
    Search for [Dracula icons](https://www.xfce-look.org/p/1541561) on XFCE-look and download it. During the time of typing we have the round and circle icons.

- Making the icons folder\
    Similar to theme folder, create an icons folder in home if existing folder is not present. Folder name `.icons`

- Installing the icons\
    Extract the icon pack into the `.icons` folder and then go the the settings menu and enable it


### Using an app launcher

The existing XFCE setup contains an old fashioned app menu, to open apps faster installing an app launcher is better. So for the setup we are going to install **Rofi**.

- Installation
    ```bash
    sudo pacman -Syu rofi
    ```

- Creating a dracula theme
    - Creating the themes folder
        ```bash
        mkdir -p ~/.local/share/rofi/themes
        ```
    - Creating the theme
        - Create a dracula theme file
            ```bash
            nano ~/.local/share/rofi/themes/darcula.rasi
            ```
        - Writing this into the themes file
            ```
            * {
                bg:          #282a36;
                current-line:#44475a;
                fg:          #f8f8f2;
                comment:     #6272a4;
                cyan:        #8be9fd;
                green:       #50fa7b;
                orange:      #ffb86c;
                pink:        #ff79c6;
                purple:      #bd93f9;
                red:         #ff5555;
                yellow:      #f1fa8c;

                background-color:   transparent;
                text-color:         @fg;

                margin:     0;
                padding:    0;
                spacing:    0;
            }

            window {
                background-color:   @bg;
                border:             2px;
                border-color:       @purple;
                border-radius:      6px;
                width:              600px;
                padding:            12px;
            }

            inputbar {
                spacing:    8px;
                padding:    8px;
                background-color: @current-line;
                border-radius:   4px;
                children:   [ prompt, entry ];
            }

            prompt {
                text-color: @green;
            }

            entry {
                text-color: @fg;
                placeholder: "Search...";
                placeholder-color: @comment;
            }

            mainbox {
                children: [ inputbar, listview ];
                spacing: 12px;
            }

            listview {
                lines:        8;
                columns:      1;
                fixed-height: 0;
                spacing:      4px;
            }

            element {
                padding:       8px;
                border-radius: 4px;
            }

            element normal.normal {
                background-color: transparent;
                text-color:       @fg;
            }

            element selected.normal {
                background-color: @current-line;
                text-color:       @cyan;
            }
            ```
        - Test the theme
            ```bash
            rofi -show drun -theme darcula
            ```
            If it works out well you can set the theme using the interactive theme selector
        - Setting up the theme
            ```bash
            rofi-theme-selector
            ```
    - Assigning a shortcut
        - Open Settings → Keyboard → Application Shortcuts
        - Click Add
        - Set Command to `rofi -show drun`
        - Press `Alt + Space` when prompted for the shortcut combination.