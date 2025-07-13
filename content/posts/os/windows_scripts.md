+++
title = 'Windows scripts with powershell and cmd'
date = 2023-12-07T22:42:51+05:30
draft = false
tags = ["windows", "powershell", "cmd", "batch", "shell", "operating system"]
+++

# Windows prompts

## PowerShell
**PowerShell** is a command-line shell and scripting language built on the .NET Framework. It is the successor to the **Command Prompt**.
Commands are called **cmdlets** and are written in the form `Verb-Noun`. For example, `Get-ChildItem` lists the contents of a directory.
There are a few **aliases** for common commands, such as `ls` for `Get-ChildItem` and `rm` for `Remove-Item`.

1. `Write-Output`: Prints a line in the shell
2. `New-Item`: Creates a new file within the same directory
3. `Get-Content`: Reads the contents of a file
4. `Set-Content`: Writes the contents of a file
5. `Remove-Item`: Deletes a file
6. `Get-ChildItem`: Lists the contents of a directory

| Command | Alias | Description |
| --- | --- | --- |
| `Write-Output` | `echo` | Prints a line in the shell |
| `New-Item` | `touch` | Creates a new file within the same directory |
| `Get-Content` | `type` | Reads the contents of a file |
| `Set-Content` | `echo` | Writes the contents of a file |
| `Remove-Item` | `del` | Deletes a file |
| `Get-ChildItem` | `dir` | Lists the contents of a directory |

## CMD
1. `echo <line>`: Prints a line in the shell
2. `type <file>`: Reads the contents of a file
3. file operations
	1. `copy <source> <target>`: Copies a file
	2. `move <source> <target>`: Moves a file
	3. `del <file>`: Deletes a file
4. `dir`: Lists the contents of a directory
5. `cd` commands: required to change the current directory
	1. `cd <dir>`: Changes the current directory
	2. `cd ..`: Changes the current directory to the parent directory
	3. `cd`: Changes the current directory to the home directory
8. `mkdir <dir>`: Creates a new directory
9. system boot options
	1. `shutdown /s`: Shuts down the system
	2. `shutdown /r`: Restarts the system
	3. `shutdown /l`: Logs off the current user
	4. `shutdown /h`: Hibernates the system
	5. `shutdown /a`: Aborts the system shutdown
10. computer processes
	1. `tasklist`: Lists all running processes
	2. `taskkill /pid <pid>`: Kills a process by its PID
	3. `taskkill /im <name>`: Kills a process by its name
11. network operations
	1. `ipconfig`: Lists the network configuration
	2. `ping <host>`: Pings a host
12. software management
	- Note: These commands may require administrator privileges
	1. `winget install <package>`: Installs a package
	2. `winget uninstall <package>`: Uninstalls a package
	3. `winget search <package>`: Searches for a package
	4. `winget show <package>`: Shows information about a package
	5. `winget source`: Lists the package sources
	6. `winget source add <source>`: Adds a package source
	7. `winget source remove <source>`: Removes a package source
13. system information
	1. `systeminfo`: Lists the system information
	2. `systeminfo | findstr /B /C:"OS Name" /C:"OS Version"`: Lists the OS information
	3. `systeminfo | findstr /B /C:"System Boot Time"`: Lists the system boot time
	4. `systeminfo | findstr /B /C:"System Manufacturer" /C:"System Model"`: Lists the system manufacturer and model
	5. `systeminfo | findstr /B /C:"Total Physical Memory"`: Lists the total physical memory
	6. `systeminfo | findstr /B /C:"Available Physical Memory"`: Lists the available physical memory
	7. `systeminfo | findstr /B /C:"Virtual Memory: Max Size"`: Lists the maximum virtual memory
14. computer troubleshooting
	1. `sfc /scannow`: Scans the system for corrupted files
	2. `chkdsk`: Scans the system for corrupted disks
	3. `dism /online /cleanup-image /restorehealth`: Scans the system for corrupted images
	4. `dism /online /cleanup-image /startcomponentcleanup`: Cleans up the system
	5. `dism /online /cleanup-image /startcomponentcleanup /resetbase`: Cleans up the system and resets the base
	6. `dism /online /cleanup-image /restorehealth /source:<source>`: Scans the system for corrupted images using a source
	7. `dism /online /cleanup-image /startcomponentcleanup /resetbase /source:<source>`: Cleans up the system and resets the base using a source

## Batch files
A **batch file** is a text file containing a series of commands to be executed by the command interpreter. It is similar to a shell script. Batch files have the `.bat` extension.

- Running a _hello world_ script
	1. Create a file named `hello.bat` with the following contents:
		```bat
		@echo off
		echo Hello, world!
		```
	2. Run the script by double-clicking on it
	3. The output should be:
		```
		Hello, world!
		```

- Fibonacci sequence
	```bat
	@echo off
	set /a a=0
	set /a b=1
	set /a c=0
	:loop
	echo %a%
	set /a c=%a%+%b%
	set /a a=%b%
	set /a b=%c%
	if %a% leq 100 goto loop
	```

- Logical operations in batch files
	```bat
	@echo off
	set /a a=1
	set /a b=2
	set /a c=3
	if %a% equ 1 if %b% equ 2 if %c% equ 3 echo True
	```
### Components of a batch file
1. `@echo off`: Disables the echoing of commands
2. `echo <line>`: Prints a line in the shell
3. `pause`: Pauses the script until a key is pressed
4. `goto <label>`: Jumps to a label
