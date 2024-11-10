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

# Dual booting arch and win11

## Prerequisites

Before installing arch we need to do the following things

### Disk partition

We’ll need to make a disk partition in windows 11 before proceeding to make sure both the OS run isolated, this can be done by the following steps

1. **Right-click on the Start menu** and select **Disk Management**. Alternatively, you can press `Win + X` and choose **Disk Management** from the list.
2. In the Disk Management window, locate the drive you want to partition (usually the C: drive). In my case I’ve installed in D drive on a separate disk
3. **Right-click on the drive** and select **Shrink Volume**
4. In the dialog that appears, enter the amount of space to shrink (in MB). This will be the size of the new partition for Arch Linux. Make sure to leave enough space for Windows. In my case I’ve allocated 100 gigs for Arch.
5. Click **Shrink**. The unallocated space will appear in the Disk Management window.

### Bios settings

1. Disable Fast Startup
2. Disable secure boot

### Arch ISO setup

1. Download arch ISO from the [official site.](https://archlinux.org/)
2. Install a tool such as Rufus or Etcher and burn the ISO onto a USB drive.

### Booting onto Arch

1. Insert the drive into the computer
2. Restart the computer into the BIOS/UEFI/Bootloader menu
3. Select the boot option as the USB drive

## Installing Arch

(under progress)

## Crutial services
### IWCTL - wifi configuration
To check whether you are connected to internet one of two commands can be used
1. `ip a`: Can be used for showing all the ip information that are ongoing, shows the ip address of all the networking devices, these include, looplack device, wifi adaptor and ethernet (if you have one)
2. `ping (domain name)`: Can be used to hit a ping or do a packet transfer towards a domain on the net. Usage: `ping www.exampleanydomainname.com`.

The IWCTL CLI can be used via
    1. IWCTL can be installed via the following command.
        ```bash
        sudo pacman -S iwd
        ```
    2. We can iuse the iwctl cli app by just typing in `iwctl`
    3. When inside iwctl the following command can be used to list the devices inside the computer, this can be done via 
        ```bash
        device list
        ```
    4. To scan for the available netowrks
        ```bash
        station <device_name> scan
        ```
    5. To list hte available networks
        ```bash
        station <device_name> get-networks
        ```
    6. Connect to a Wi-Fi network
        ```bash
        station <device_name> connect <SSID>
        ```
    7. Get details of the connection
        ```bash
        station <device_name> show
        ```
    8. Can be exited via 
        ```bash
        exit
        ```

Sometimes IWCTL may not work because of DHCP issue, this can be resolved via
1. Check installation of `dhcpcd`
    ```
    dhcpcd --help
    ```
2. If not already installed install it via
    ```
    sudo pacman -S dhcpcd
    ```
3. Start the service
    ```
    sudo systemctl enable dhclient --now
    ```
## Apps and user config

### Pacman

Lets first see the base docs of pacman

The `pacman` command is a package manager used in Arch Linux and its derivatives to manage software packages. Here’s a basic guide on how to use it:

1. **Update Package Database:**
    
    ```bash
    sudo pacman -Sy
    
    ```
    
    Updates the package database to the latest version.
    
2. **Upgrade All Packages:**
    
    ```bash
    sudo pacman -Su
    
    ```
    
    Upgrades all installed packages to their latest versions.
    
3. **Install a Package:**
    
    ```bash
    sudo pacman -S package_name
    
    ```
    
    Replace `package_name` with the name of the package you want to install.
    
4. **Remove a Package:**
    
    ```bash
    sudo pacman -R package_name
    
    ```
    
    This removes the specified package.
    
5. **Remove a Package and Its Dependencies:**
    
    ```bash
    sudo pacman -Rns package_name
    
    ```
    
    This removes the package along with its unused dependencies.
    
6. **Search for a Package:**
    
    ```bash
    pacman -Ss search_term
    
    ```
    
    This searches the package database for the specified term.
    
7. **Show Package Information:**
    
    ```bash
    pacman -Si package_name
    
    ```
    
    Displays detailed information about a specified package.
    
8. **List Installed Packages:**
    
    ```bash
    pacman -Q
    
    ```
    
9. **Check for Package Updates:**
    
    ```bash
    pacman -Qu
    
    ```
    
    Lists all packages that have updates available.
    

Additional options

- **Verbose Mode:** Add `v` for verbose output.
- **Help:** Use `pacman -h` to see all available options.

### My installed pacman packages

1. Zsh - [Ref](https://beebom.com/how-install-zsh-and-oh-my-zsh-linux/)
    1. Setup and install
        
        ```bash
        sudo pacman -S zsh
        chsh -s $(which zsh) # enter your password when prompted
        sh -c "$(curl -fsSL [https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh](https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh))" # this will install zsh
        ```
        
    2. My configuration - extensions [Ref](https://catalins.tech/zsh-plugins/)
        
        Extensions list
        
        1. Zsh autosuggest
        2. Zsh syntax highlight
        3. You should use
        4. Zsh-bat
        
        ```bash
        # cloning all the repos
        git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
        git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
        git clone https://github.com/MichaelAquilina/zsh-you-should-use.git $ZSH_CUSTOM/plugins/you-should-use
        git clone https://github.com/fdellwing/zsh-bat.git $ZSH_CUSTOM/plugins/zsh-bat
        ```
        
        Now go to the line that says `plugins=(git)` and replace them with the following
        
        ```bash
        plugins=(git zsh-autosuggestions zsh-syntax-highlighting you-should-use zsh-bat)
        ```
        
        A note that **bat** needs a package dependency also, this may be done via running the following command
        
        ```bash
        sudo pacman -S bat
        ```
        
        Now refresh the shell by using
        
        ```bash
        source ~/.zshrc
        ```
        
    3. Configuring the theme
        
        For this install we are going to use [powerlevel10k](https://github.com/romkatv/powerlevel10k?tab=readme-ov-file#oh-my-zsh), via this command
        
        ```bash
        git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
        ```
        
        then we are going to configure the `~/.zshrc` file to reflect the theme, this can be done via opening the `~/.zshrc` file and paste the following
        
        ```bash
        # file can be opened by
        nano ~/.zshrc
        ```
        
        paste the following in place of `ZSH_THEME="robbyrussell`
        
        ```bash
        ZSH_THEME="powerlevel10k/powerlevel10k"
        ```
        
2. NodeJS: For installing the 20x version we are using the following command
    
    ```jsx
    sudo pacman -S nodejs npm
    ```
    
3. Pip: A package manager for python
    
    ```jsx
    sudo pacman -S python-pip
    ```
    
4. Hugo: A static site builder
    
    ```jsx
    sudo pacman -S hugo
    ```
    
5. LibreOffice: Documentation and productivity suite
    
    ```bash
    sudo pacman -S libreoffice-fresh # or libreoffice-still for stable version 
    ```
    
6. Neovim: CLI based text editor
    
    ```bash
    sudo pacman -S neovim
    ```
    
    Optional: I’ve set up [neovim kickstart](https://github.com/nvim-lua/kickstart.nvim) to quick start neovim.
    

### AUR

1. Setting up `yay` and basics of AUR
    
    For the initial setup of the AUR first you need to update all the packages inside it this can be done via. Then install the packages. This can be checked below. [Ref](https://youtu.be/EYiN8vDkacc?si=JySf9AVfAYe3ycLl).
    
    ```bash
    sudo pacman -Syu
    sudo pacman -S git base-devel
    ```
    
    Firstly we need to install `yay` which is a helper for installing software via AUR this can be done by the following commands
    
    ```bash
    git clone https://aur.archlinux.org/yay.git
    cd yay
    makepkg
    ```
    
    if the program doesn’t compile then you may need to install the following dependencies (optional)
    
    ```bash
    sudo pacman -Syu go
    makepkg
    ```
    
    now we can install yay via `pacman`
    
    ```bash
    sudo pacman -U yay-12.4.2-1-x86_64.pkg.tar.zst
    ```
    
    the install can be checked and verified via 
    
    ```bash
    yay -h
    ```
    
2. My AUR packages
    
    **Note:** Packages installed via `yay` may not need `sudo` privalages
    
    1. Notion: A note taking app
        
        ```jsx
        yay -S notion-app-electron
        ```
        
    2. VSCode (official version): Text ediitor by microsoft
        
        ```jsx
        yay -S visual-studio-code-bin
        ```
        
    3. Google Chrome: Web browser
        
        ```jsx
        yay -S google-chrome
        ```
        

## Additional settings

1. Battery threshold
    
    In a laptop where the laptop is always plugged in it is important to set up a battery threshold to preserve the battery life. In KDE Plasma 6 this feature is already baked in, however in Plasma 6.2.1 (the one which I’m using the time of writing) resets the threshold value on every boot, this can be fixed in the following way. [Ref](https://www.pclinuxos.com/forum/index.php?topic=161667.0).
    
    To achieve this i did the following steps
    
    1. Create a service - I named it `kde-battery-threshold-workaround.service`, this can be located in `/etc/systemd/system`
    2. Paste the following in it
        
        ```bash
        [Unit]
        Description=Set Battery Charge Control Threshold
        
        [Service]
        ExecStart=/usr/bin/sudo /bin/sh -c 'echo "60" > /sys/class/power_supply/BAT1/charge_control_end_threshold' # you can change this line accordingly to your battery dir
        Type=oneshot
        RemainAfterExit=yes
        ExecStartPre=/bin/sleep 10
        
        [Install]
        WantedBy=multi-user.target
        ```
        
    3. Run the following commands
        
        ```bash
        sudo systemctl daemon-reload
        sudo systemctl enable kde-battery-threshold-workaround.service
        sudo systemctl start kde-battery-threshold-workaround.service
        sudo systemctl daemon-reload
        ```
        
2. Git setup
    
    ```bash
      git config --global user.email "you@example.com"
      git config --global user.name "Your Name"
    ```
