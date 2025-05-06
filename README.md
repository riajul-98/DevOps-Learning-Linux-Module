# DevOps-Learning-Linux-Module.
Repository containing commands and topics I learnt in the CoderCo Linux Module.

## Commands
- `pwd`- Displays the current working directory.
- `cd /tmp` - Changes current working directory to the specified directory. `cd ..` takes you up a level.
- `mkdir newdir` - Creates a new directory in the current directory with the specified name. Add option `-p` to create a new directory within a non-existant path.
- `rmdir newdir` - Removes the specified directory. Must be an empty directory.
- `ls` - Lists files and directories in present working directory.
- `touch hello.txt` - Creates a file with the specified name.
- `rm hello.txt` - Removes specified file. Requires `-r` to remove directories.
- `man ls` - Provides the manual page for the specified command.
- `echo "hello"` - Prints the specified string. Can be used with `>` or `>>` followed by a filename to write the output of the command to the file. e.g. `echo "Hello World" > file.txt`
- `cat file.txt` - Allows you to read the specified file.
- `grep "Hello" file.txt` - Looks for the specified pattern in the given file.
- `head multiline.txt` - Displays first 10 lines of the file. Can add option `-n` followed by the number of lines you wish to see.
- `tail multiline.txt` - Displays last 10 lines of the file. Can add option `-n` followed by the number of lines you wish to see.
- `cp multiline.txt multiline_copy.txt` - Copies multiline.txt and creates a copy of it with the specified name.
- `cp -r my_directory /tmp` - Copies my_directory to the tmp file. -r is required for directories.
- `mv multiline.txt multiline_backup.txt` - Renames specified file.
- `mv multiline.txt /tmp` - Moves file to specified directory.

## Shell, Program and Binaries
When we make commands, the shell communicates this to the operating system. Commands in Linux are programs which are written in a programming language and then compiled into a binary which the OS can run. When we run one of these commands, the shell interpreter will look for these commands in one of the directories specified in $PATH and executes the command. The shell is the user interface which provides access to the OS services. There are different shells which come with different functionalities. You can view the current shell by running the `echo $SHELL` command.

## Linux File System
The top level directory in the Linux file system is the root directory (`/`). The bin directory contains executables such as commands like `pwd`. The boot directory contains files related to the booting process. The dev directory holds device files. The etc directory contains system wide configuration files and scripts.

## Spaces in directory names
To create directories with spaces in their names, you can either use `mkdir` followed by the name of the directory, encapsulated in parenthases or use the backwards slash before each space. For example `mkdir 'new folder 1'` or `mkdir new\ folder\ 2`. You can then use the same methods when using the cd command and other commands.

## VIM Text Editor
VIM is a Linux text editor. You can write to a new file with VIM by running the command `vim` followed by the filename. If the file does not exist, a new file will be created with that name and opened. The default mode is the command mode. To write text, enter insert mode by pressing `i`. To go back to command mode, press `esc`.

## Sudo
Sudo allows you to execute a command as a super user. You must be a permitted user. Examples of commands include `sudo apt-get update`. This would be needed in many administrative tasks such as installing packages, creating users or editing configuration files.

## Root User
Sometimes you might want to switch to the root user. To switch to the root user, you run the `sudo su` command. It is generally better to avoid this as the root user has unrestricted access. You can view the sudo command log in /var/log/auth.log

## Users
- `sudo useradd Riajul` - Creates a new user with the specified name.
- `sudo passwd Riajul` - Follow the prompts to set a new password.
- `su - Riajul` - Switch to the new user.
- `sudo usermod -aG sudo Riajul` - Adds user to sudoers file.
- `sudo deluser Riajul sudo` - Removes user from sudoers file.

## Groups
- `/etc/group` - Contains group information.
- `sudo groupadd devops` - Creates new group called devops
- `sudo usermod -aG devops Riajul` - Adds user to the specified group.
- `groups` - Displays current users groups.
- `sudo gpasswd -d Riajul devops` - Removes user from the group.
- `sudo groupdel devops` - Deletes group.

## Permissions
- `ls -l` - Displays all files along with other information such as ownership and permissions.
The first character represents the file type. The next 3 represent the owners permissions. The following 3 are group permissions and the final 3 characters are the permissions for others.

The octal value for read (r) is 4, for write (w) is 2 and execute (x) is 1. If you want to give the owner read and write permission, the octal value would be 4 + 2 = 6.
Giving permission can be done in three methods which look like the below;

- `sudo chmod 770 example.txt` - This gives read, write and execute permissions to the owner and group but no permissions to others.
- `sudo chmod u+x,g+r,o-w example.txt` - This gives the owner execute permissions on top of the permissions they already have, the group write permissions and takes away execute permissions for others.
- `sudo chmod ug=rw,o=r example.txt` - Gives user and group read and write permissions and read permissions to others.

## Ownership
- `sudo chown Riajul example.txt` - Changes ownership of file.
- `sudo chgrp admin2 example.txt` - Changes group of the file.
- `sudo chown ubuntu:admin2 example.txt` - Changes both user and group of the file.
- `sudo chown -R Riajul my_directory` - Changes ownership of directory and its contents.

## Standard Streams
- Standard Input - Commands we give.
- Standard Output - Output in response to our commands. To redirect to a file, you use `>` or `>>`, followed by the file name.
- Standard Error - Error messages. To redirect to a file, you use `2>` or `2>>`, followed by the file name.
- To redirect both stdout and stderr, use `&>` or `&>>`, followed by the file name.
- You can redirect outputs to `/dev/null` which discards anything written to it. Sort of like a black hole.

## Environment Variables
Variables that are set in the Linux environment which outline how the Linux environment will behave and store configuration settings. E.g. the $PATH variable stores where commands are found.
- `export NAME=value` - Sets an environment variable. Running this on the command line will temporarily set the environment variable until the next reboot. To make it permanent, place this command in the .bashrc file. To apply changes run the command `source .bashrc`
- `printenv` - Prints environment Variables.
- `echo $SHELL` - Prints the specified variable.

## Aliases
- `alias` - Shows a list of current aliases.
- `alias hello='echo "hello world"'` - Temporarily sets a new alias called hello to run the specified command. To make it permanent, add the command to the .bashrc file and then run the `source .bashrc` command.
