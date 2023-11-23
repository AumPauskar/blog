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

