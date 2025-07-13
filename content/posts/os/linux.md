+++
title = 'Linux'
date = 2023-11-23T12:52:03+05:30
draft = false
tags = ["operating system", "linux", "shell", "bash", "debian", "ubuntu", "raspberry pi"]
author = "Aum Pauskar"
description = "A brief overview and commands based on the linux operating system"
+++

# Linux/UNIX shell commands
The UNIX shell is a command-line interface made for interacting with the OS. There are various commands to execute this.

**Note:** The current documentaiton is based on **Ububtu** and similar debian bases operating systems.

## File systems
The linux file system is a tree structure with the root directory at the top. The root directory is denoted by `/`. The directories are separated by `/` and the files are separated by `.`. The file system is case sensitive. The file system is made up of the following:
```bash
bin   dev  home  lib    lib64   lost+found  mnt  proc  run   snap  sys  usr
boot  etc  init  lib32  libx32  media       opt  root  sbin  srv   tmp  var
```
The bin folder comtains the binaries of the programs. The etc folder contains the configuration files. The home folder contains the user files. The lib folder contains the libraries. The root folder contains the root user files. The sbin folder contains the system binaries. The tmp folder contains the temporary files. The var folder contains the variable files. The home folder contains the user files. Everything a user executes is stored in the subfolders of the home folder. When the user creates an account on the linux operation system a new folder gets created in the home folder that contains all the information of the user.

- Connect devices may be mounted in the /media directory, and can be found out by the `lsblk` command.
### File management
- `ls`: running this commmand will list all the files stored in the current directory or folder
- `ls -a`: running this commmand will list all the files stored in the current directory or folder plus the hidden files
- `cd`: change directory command will help you traverse through the file system. Running cd as a standalone command will take you to the home directory. Running `cd ..` will take you to the parent directory. Running `cd <folder name>` will take you to the folder name. Running `cd /` will take you to the root directory.
- `pwd`: running this command will print the current working directory
- `mkdir <foldername>`: running this command will create a new directory
- `touch <filename.fileextension>`: running this command will create a new file
- `rm <filename.fileextension>`: running this command will remove the file
- `rm -r <foldername>`: running this command will remove the folder
- `rm -rf <foldername>`: running this command will remove the folder and all the files in it including the hidden files
- `mv <path/file> <path/file>`: running this command will move the file, if the path is same then it will rename the file.
- `cp <path/file> <path/file>`: running this command will copy the file
- `cp -r <path/folder> <path/folder>`: running this command will copy the folder
- `cat <file>`: running this command will print the contents of the file
	- `cat <file> > <file>`: running this command will copy the contents of the first file to the second file
	- `cat <file> >> <file>`: running this command will append the contents of the first file to the second file
	- `cat <file> | grep <string>`: running this command will print the lines of the file that contain the string
	- `cat <file> | grep -v <string>`: running this command will print the lines of the file that do not contain the string
	- `cat <file> | grep -i <string>`: running this command will print the lines of the file that contain the string irrespective of the case
	- `cat <file> | grep -n <string>`: running this command will print the lines of the file that contain the string along with the line number
- `df` and `df -h` can be used to check the occupied storage by the file system

### File permissions
The file permissions are the permissions that are assigned to the files and the folders. The file permissions are assigned to the files and the folders by the following command
```bash
chmod <permissions> <file>
```
example
```bash
chmod 777 <file>
```
This will give the file all the permissions. The file permissions are assigned by the following numbers
- 0: no permissions
- 1: execute
- 2: write
- 3: write and execute
- 4: read
- 5: read and execute
- 6: read and write
- 7: read, write and execute

This can also be assigned by the following letters
- r: read
- w: write
- x: execute

The file permissions can be seen by the following command
```bash
ls -l
```

### File ownership
The file ownership is the ownership of the file. The file ownership is assigned to the files and the folders by the following command
```bash
chown <user>:<group> <file>
```
example
```bash
chown john:john <file>
```
This will give the file to the user john and the group john. 

### About the file system
- The file system is case sensitive
- The file system is hierarchical
- The file system is a tree structure
- The file system is a multi-user system
- The file system is a multi-tasking and multi-threaded system


## Important commands to remember
- `man`: running the `man` as the prefix to any command will give you the documentation of the whole binary/command
- `-h` or `--help`: running any one of these commnds will give a short listing of the package
- `-v` or `--version`: running any of of these commands will display the version of software you are using. This command is typically used to verify the installation of packages.
## Installation of packages
Apps or packages can be installed in the system via the `apt` or the `apt-get` command. Here are the key things to remember.
- There is a pool where all the system binaries are stored
- These system binaries need to be updated via the following command before installation of every program
	```bash
	sudo apt update
	```
- Binares and packages can be updated in the system by running this command
	```bash
	sudo apt upgrade
	```
- Packages can be installed by this command
	```bash
	sudo apt install <package name>
	```
- Packages can be removed by this command
	```bash
	sudo apt remove --purge <package name>
	```
	and then removing any unused dependencies by running this command
	```bash
	sudo apt autoremove
	```
- Packages can be searched by this command
	```bash
	sudo apt search <package name>
	```

### DPKG
Dpkg is a package manager for Debian based systems. It is used to install, remove, and provide information about `.deb` packages. Dpkg is a low level tool that interacts with the `.deb` packages. Some packages may not be available in the apt pool, then the package can be installed with the `dpkg` command. `.deb` can be installed with the software manager in ubuntu via double clicking but with cli we can use this command to install the package
```bash
sudo dpkg -i <package name>
```
The package can be removed by this command
```bash
sudo dpkg -r <package name>
```
The package can be removed along with the configuration files by this command
```bash
sudo dpkg -P <package name>
```

## Shells
Shells are the command line interpreters that run the commands. There are various shells available in the linux operating system. The default shell in the linux operating system is the bash shell. However the benifit of the linux family is customisablity and hence there are various shells available. The zsh shell is one of the most popular shells. To install this you can follow this [link](https://aumpauskar.github.io/blog/posts/misc/zsh/).

## Things to show off to your non-linux friends
1. `cmatrix`: running this command will show you the matrix effect
	```bash
	sudo apt update
	sudo apt install cmatrix
	cmatrix
	```
2. `sl`: running this command will show you the train running on the terminal
	```bash
	sudo apt update
	sudo apt install sl
	sl
	```
3. `cowsay`: running this command will show you a cow saying something
	```bash
	sudo apt update
	sudo apt install cowsay
	cowsay <message>
	```

## Processes
When a linux operating system is run then many processes are created, these usually run at the user level rather running at the kernal level. \
Processes can be run via the `ps`
```bash
ps
```
Output
```
    PID TTY          TIME CMD
    372 pts/0    00:00:00 zsh
    470 pts/0    00:00:00 ps
```
An alternative to running the ps command is running the `top` or `htop` command. Htop is not natively installed in many systems and can be installed via `sudo apt install htop` in debian based systems.\
To see every process on the system 
```bash
ps -e
```

## Users
Users are the people who use the system. In linux based operating systems there may be multiple users (can be upto hundereds in a shared system like a server). The users in linux have a unique user id (UID) and a group id (GID). The UID is a number that is assigned to the user and the GID is a number that is assigned to the group. The UID and GID are stored in the `/etc/passwd` file. Every users has a home directory that is stored in the `/home` directory. The user may have different privalages that are assigned when the users are created and added to the system.

- Adding a user\
	A user can be added to the system by running the following command
	```bash
	sudo adduser <username>
	```
- Deleting a user\
	A user can be deleted from the system by running the following command
	```bash
	sudo deluser <username>
	```
- Changing the password of a user\
	A user can change the password of the user by running the following command
	```bash
	sudo passwd <username>
	```

## Shell scripting
Shell scripting is a way to automate the tasks that are done on the command line. Shell scripts are written in the bash shell. The shell scripts are saved with the `.sh` extension. The shell scripts can be run by the following command
```bash
bash <filename.sh>
```
The shell scripts can be run in the background by the following command
```bash
./<filename.sh> &
```
The shell scripts can be run in the background and the output can be redirected to a file by the following command
```bash
./<filename.sh> &> <filename.txt> &
```

### How to create a shell scripting file
```bash
#!/bin/bash
echo "Hello World"
```

### Basic operations

- Variables\
	Variables can be created by the following command
	```bash
	<variable name>=<value>
	```
	Variables can be accessed by the following command
	```bash
	echo $<variable name>
	```

	Demonstration
	```bash
	#!/bin/bash
	NAME="John Doe"
	echo "Hello $NAME"
	```

- User input\
	User input can be taken by the following command
	```bash
	read <variable name>
	```
	Demonstration
	```bash
	#!/bin/bash
	echo "Enter your name"
	read NAME
	echo "Hello $NAME"
	```

- If else\
	If else can be used to run a command if a condition is true or false
	```bash
	if <condition>
	then
		<command>
	else
		<command>
	fi
	```
	Demonstration
	```bash
	#!/bin/bash
	echo "Enter your name"
	read NAME
	if [ "$NAME" == "John Doe" ]
	then
		echo "Hello $NAME"
	else
		echo "You are not John Doe"
	fi
	```

- Loops\
	Loops can be used to run a command multiple times
	- For loop\
		For loop can be used to run a command multiple times
		```bash
		for <variable name> in <list>
		do
			<command>
		done
		```
		Demonstration
		```bash
		#!/bin/bash
		for i in 1 2 3 4 5
		do
			echo "Hello $i"
		done
		```
	- While loop\
		While loop can be used to run a command multiple times
		```bash
		while <condition>
		do
			<command>
		done
		```
		Demonstration
		```bash
		#!/bin/bash
		i=1
		while [ $i -le 5 ]
		do
			echo "Hello $i"
			i=$(( i+1 ))
		done
		```

- Comparisons\
	Comparisons can be used to compare two values
	- String comparison\
		String comparison can be used to compare two strings
		```bash
		if [ "$<variable name>" == "<string>" ]
		then
			<command>
		fi
		```
	- Number comparison\
		Number comparison can be used to compare two numbers
		```bash
		if [ $<variable name> -eq <number> ]
		then
			<command>
		fi
		```
	- File comparison\
		File comparison can be used to compare two files
		```bash
		if [ -f <file name> ]
		then
			<command>
		fi
		```
- Greater than or less than\
	Greater than or less than can be used to compare two numbers
	```bash
	if [ $<variable name> -gt <number> ]
	then
		<command>
	fi
	```
- Greater than or equal to or less than or equal to\
	Greater than or equal to or less than or equal to can be used to compare two numbers
	```bash
	if [ $<variable name> -ge <number> ]
	then
		<command>
	fi
	```

## Startup scripts
Startup scripts are the scripts that are run when the system is started. The easiest way to automate the startup scripts is to use crontab. Crontab is a time based job scheduler. Crontab can be used to run the scripts at the startup of the system. The crontab can be edited by the following command
```bash
crontab -e
```

A startup script in crontab may look like this
```bash
@reboot /path/to/script.sh
```

## Alising
Alising is a way to create a shortcut for a command. Alising can be done by the following command
```bash

alias <alias name>="<command>"
```

For example I use python3 a lot an I find it hard typing python3 everytime so I can create an alias _py_ for python3 by running the following command
```bash
alias py="python3"
```

The alias can be removed by the following command
```bash
unalias <alias name>
```

Aliases can be saved in the `.bashrc` file. The `.bashrc` file is a file that is run when the terminal is opened. The `.bashrc` file is stored in the home directory. The `.bashrc` file can be edited by the following command
```bash
nano ~/.bashrc
```

Then you may name the alias in the file like this
```bash
alias py="python3"
```

## Foreground and backgorund processes
Processes can be run in the foreground or the background. The foreground processes are the processes that are run in the terminal. The background processes are the processes that are run in the background. The background processes are run by the following command
```bash
<command> &
```
The background processes can be stopped by the following command
```bash
kill %<job number>
```
In a linux system with just one terminal the simplest way to run a process in the background is to run the process in the background by the following command
```bash
<some command>
```
Then press `ctrl + z` to stop the process and then run the following command
```bash
bg
```
Then the process will run in the background. The process can be stopped by the following command
```bash
kill %<job number>
```

## Users and groups
### Definitions
- Users: Users are the people who use the system. In linux based operating systems there may be multiple users (can be upto hundereds in a shared system like a server). The users in linux have a unique user id (UID) and a group id (GID). The UID is a number that is assigned to the user and the GID is a number that is assigned to the group. The UID and GID are stored in the `/etc/passwd` file. Every users has a home directory that is stored in the `/home` directory. The user may have different privalages that are assigned when the users are created and added to the system.
- Groups: Groups are the collection of users. The groups are used to assign the permissions to the users. The groups are stored in the `/etc/group` file


### Commands
- Users can be added by the following command
	```bash
	sudo adduser <username>
	```
- Users can be deleted by the following command
	```bash
	sudo deluser <username>
	```
- Users can be added to a group by the following command
	```bash
	sudo usermod -aG <groupname> <username>
	```
- Users can be removed from a group by the following command
	```bash
	sudo deluser <username> <groupname>
	```
- Groups can be added by the following command
	```bash
	sudo addgroup <groupname>
	```
- Groups can be deleted by the following command
	```bash
	sudo delgroup <groupname>
	```

## Services in linux
In Linux, a service is a type of software that runs in the background and performs certain tasks without user intervention. These tasks could be anything from handling requests on a server, monitoring system events, or running scheduled tasks. 

Services in Linux are also known as "daemons". They start at system boot and continue to run until the system is shut down. 

You can manage services in Linux using system commands like `systemctl`, `service`, or `init` scripts depending on your Linux distribution and the init system it uses (System V, Upstart, or systemd). For example, you can start, stop, restart, enable, or disable services. 

Here's an example of how you might use `systemctl` to manage a service:

```bash
# To start a service
sudo systemctl start serviceName

# To stop a service
sudo systemctl stop serviceName

# To restart a service
sudo systemctl restart serviceName

# To enable a service to start on boot
sudo systemctl enable serviceName

# To disable a service from starting on boot
sudo systemctl disable serviceName
```

### Creating a service
Creating a custom service in Linux involves writing a service unit file. This file tells systemd how to manage your service. Here's a basic example of how to create a custom service using systemd, which is the init system used by most modern Linux distributions.

1. Create a new service file in `/etc/systemd/system` with a `.service` extension. For example, `my_service.service`. Use `sudo` because this is a system directory.

```bash
sudo nano /etc/systemd/system/my_service.service
```

2. In the service file, define the service with `[Unit]`, `[Service]`, and `[Install]` sections.

```ini
[Unit]
Description=My Custom Service
After=network.target

[Service]
ExecStart=/usr/bin/my_service
Restart=always
User=username
Group=groupname
Environment=PATH=/usr/bin:/usr/local/bin
Environment=NODE_ENV=production
WorkingDirectory=/home/username/my_service

[Install]
WantedBy=multi-user.target
```

Replace `/usr/bin/my_service` with the path to the script or executable that your service will run. Replace `username` and `groupname` with the user and group that should own the process. Replace `/home/username/my_service` with the working directory of your service.

3. After saving and closing the file, reload the systemd manager configuration.

```bash
sudo systemctl daemon-reload
```

4. Enable your service so that it starts on boot.

```bash
sudo systemctl enable my_service
```

5. Start your service.

```bash
sudo systemctl start my_service
```

6. Check the status of your service.

```bash
sudo systemctl status my_service
```

Remember to replace `my_service` with the name of your service.

Replace `serviceName` with the name of the service you want to manage.
### Extra commands
- Getting user list
	```bash
	cat /etc/passwd
	```
- Get only the usernames
	```bash
	awk -F':' '{ print $1}' /etc/passwd
	```

### Other important services
1. **Transmission**: Transmission is a bittorrent client that can be used to download torrents. Transmission can be installed by the following command
	```bash
	sudo apt update
	sudo apt install transmission-qt
	```
	**Known issues of previous transmission versions** Some the the previously installed versions may support normal torrent transmissions but may fail in magnet links. This can be fixed by installing the following package
	```bash
	sudo apt remove transmission-gtk
	sudo apt install transmission-qt
	```
Yoy may check the [references](https://askubuntu.com/questions/1002986/transmission-is-not-downloading-any-magnet-links) from here.

2. **Apache**: Apache is a web server that can be used to host websites. Apache can be installed by the following command
	```bash
	sudo apt update
	sudo apt install apache2
	```
3. **Nginx**: Nginx is a web server that can be used to host websites. Nginx can be installed by the following command
	```bash
	sudo apt update
	sudo apt install nginx
	```
4. **VIM**: Vim is a text editor that can be used to edit text files. Vim can be installed by the following command. There may be a chance that it is preinstalled. To check wheter its preinstalled the following command may be used.

	```bash
	vim --version
	```

	Any output like the following means that it is already installed

	```
	VIM - Vi IMproved 8.2 (2019 Dec 12, compiled Mar 14 2024 09:05:11)
	Included patches: 1-579, 1969, 580-1848, 4975, 5016, 5023, 5072, 2068, 1849-1854, 1857, 1855-1857, 1331, 1858, 1858-1859, 1873, 1860-1969, 1992, 1970-1992, 2010, 1993-2068, 2106, 2069-2106, 2108, 2107-2109, 2109-3995, 4563, 4646, 4774, 4895, 4899, 4901, 4919, 213, 1840, 1846-1847, 2110-2112, 2121
	```

	If the output is mentioning it is not installed then this command may be used.
	```bash
	sudo apt update
	sudo apt install vim
	```
	You may check the commands [here](https://aumpauskar.github.io/blog/posts/cheatsheet/vim/)

## Misc commands
1. `vcgencmd measure_temp`: running this command will give you the temperature of the raspberry pi. Using this with the `watch` command will give you the temperature in real time (`watch vcgencmd measure_temp`).
2. `history`: running this command will give you the history of all the commands you have run in the terminal.
