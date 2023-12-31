+++
title = 'Linux'
date = 2023-11-23T12:52:03+05:30
draft = false
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
## Misc commands
1. `vcgencmd measure_temp`: running this command will give you the temperature of the raspberry pi. Using this with the `watch` command will give you the temperature in real time (`watch vcgencmd measure_temp`).
2. `history`: running this command will give you the history of all the commands you have run in the terminal.
