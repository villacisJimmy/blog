 ---
layout: post
title: "Fundamentals of Linux"
date: 2025-08-25
categories: [blog]
 ---
 
# Title  
NOTES: INTRODUCTION TO LINUX



## CLASS 1

Virtualization → Sharing the resources of a computer.

"For virtualization"

Free Software ≠ Free of Charge

Free Software → Non-proprietary; no authorization or contract is required to acquire or use it.

Distributable → You can make as many copies as you like.
It is not allowed to prevent someone else from redistributing it.

Accessible → Source code is available.
Encourages the distribution of source code to foster software development.

Modifiable → Programs can be improved and redistributed with modifications.

Reusable → Previously written code can be reused, as long as the new code preserves the freedoms of the original software.

No Guarantees → Functionality is not guaranteed.
              → Support exists but is different from traditional methods.

Hereditary → Any software derived from free software must also be free (it is forbidden to forbid).

Free Software Foundation (FSF)
- Founded in 1985 by Richard Stallman.
- Promotes the right to use, study, copy, modify, and redistribute software.

FSF's focus:
- Free software eliminates the need for proprietary software.
- Protects, promotes, and preserves free software.

GNU's Not Unix (GNU)
- Project started in 1984 by Richard Stallman to build a fully free operating system compatible with Unix.
- It includes working environments (shells), compilers, editors, text formatters, mail tools, etc.
- GNU had many programs but lacked a kernel.

Licensing and Open Source
- GPL (General Public License)
 - Ensures software remains free using copyleft.
 - Created by Richard Stallman.

Copyleft → A method to turn a program into free software and require all versions, modified or extended, to also remain free.

Open Source (a.k.a. Open Code):
- A license that allows users to study, modify, improve, and redistribute the source code.

Linux and Unix
- Developed in 1991 by Finnish developer Linus Torvalds, based on Minix.
  - Minix: a minimal Unix system for educational purposes by A. Tanenbaum.
- Linux is only the kernel of a Unix-like OS.
- GNU/Linux is 100% free.



## CLASS 2
Advantages
- Less malware
- Command line interface
- Multi-user system
- Package management
- Cost-effective
- Efficient use of resources and greater stability

Disadvantages
- Many distributions
- Occasional software incompatibility
- Case-sensitive

Distribution
- A combination of the Linux kernel and GNU-licensed programs (editors, compilers, admin tools, etc.)

GNU tools can be freely copied, modified, and installed.

All distributions can use the same kernel, but differ in package managers.

Distribution differences:
- Kernel version and compilation
- Number and version of included apps
- Proprietary applications included by the distribution maintainers

VM INSTALLATION - VMware

Enhanced Keyboard Support – For special keys.

Netinstall:
- Installation from the internet using a minimal bootable CD.
- Begins installation with minimal software, then downloads remaining packages from the internet.
- Can also install over LAN.



## CLASS 3

Installation: Disk or ISO Image

When prompted for the FQDN (Fully Qualified Domain Name):
- It includes the hostname and the domain name.
  - Example: Hostname: serv1, Domain: bar.com → FQDN: serv1.bar.com
  - Another example: post.serv1.bar.com

Partitions and File Systems
- File systems: FAT32, NTFS, ext3, ext4
  - Manage space allocation and data organization on storage devices.

Linux minimum partition scheme:
- Primary partition for root "/"
  - Logical partition for swap
  - Logical partition for boot (startup files)

Boot: Stores boot files
Swap: Half the size of the RAM
Boot size: ~1GB

Linux Directory Tree
- Hierarchical file system starting from root /
- Files, directories, and subdirectories have permissions.

The Root user has full privileges.

/              → root  
/bin/          → essential binaries  
/boot/         → static boot files  
/dev/          → device files  
/etc/          → system configuration  
/home/         → user personal folders  
/lib/          → shared libraries and kernel modules  
/media/        → mount point for removable media  
/mnt/          → temporary mount point  
/opt/          → optional software packages  
/sbin/         → system binaries  
/srv/          → service data  
/tmp/          → temporary files  
/usr/          → user utilities and apps (subtree includes bin, include, lib, local, sbin, share)  
/var/          → variable files  
/root/         → root's personal folder  
/proc/         → virtual file system for kernel and process info  


Unlike Windows (C:, D:, etc.), Linux uses mount points in a single file system structure.

Multi-user system: multiple users can work at the same time via a GUI or a terminal.

Useful Commands
$ df -h          # Show partitions
$ free -mh       # Show memory usage


## CLASS 4


$ hostname
$ whoami  # which user I am using
$ su 
$ ip a   # network interfaces
$ w      # see connected users

/var/log > Logs

What is the shell
- It is a command interpreter; it is responsible for reading what is typed on the keyboard and executing the programs or commands we indicate.

Documentation and command help
$ man
$ --help

alumno@alumno:/var$ (username, machine name, last folder, user type)

Commands
- They are words, the syntax of the commands is accompanied by parameters
  - They have one or more options that consist of a letter preceded by a dash
- When the option is a word, it is preceded by 2 dashes

Arguments
- Several commands require the input of certain arguments. Arguments are part of the information

Commands can be:
- Internal, programs built into the shell (export, ulimit, etc...)
- External, programs that are called for execution by the shell (ls, cd, mv, etc...)

Virtual Consoles
- tty1......tty7 (terminals) (from 6 to 7 depending on the distribution)
  - ctrl + alt + (f1...f7), to open the terminals

$ kill -9 (PID) -> kill a process, to get the process (top, htop, ps)
$ ps -aux


## CLASS 5

Absolute path
- The path that is based on the root “/“, every absolute path starts from “/“

Output of ls -l:
“l” —> symbolic link (shortcut in Windows)
“d” is a directory
“-” is a file

Relative path
- Relative paths depend on the current directory the user is in, knowing that each directory in the system contains files

To concatenate 2 commands we use the logical operator &&
$ cd /boot/ && ls -l

List, concatenate, and filter
$ ls -l /etc/ | grep .conf

Files with the extension “.conf” are called daemon files and are configuration files.

List the contents of a directory
$ dir

Show the host machine architecture
$ arch
$ uname -m

Know the kernel we are using
$ uname -r
$ uname -a

Hardware Components
$ dmidecode -q

Redirect
>>

View partitions
$ df -h

Disk sector data, read tests
$ hdparm -i /dev/sda

Check memory
/proc/meminfo

RAM Memory - SWAP
$ free -m

List usb
$ lsusb

Date
$ date

Calendar
$ cal

Shut down the system:
$ shutdown
$ halt
$ init 0

Restart the system
$ reboot

View files and folders in tree form
$ tree

Move and rename
$ mv

Create multiple directories hierarchically
$ mkdir -p /directory1/directory2/directory3/

Create multiple files
$ touch file1.txt file2.txt

Copy multiple files

Wildcard (“.”) replaces destination
- They are characters that represent a set or range. With this, regular expressions are constructed. Also known as a wildcard character

$ cp /var/log/ .

* , the asterisk represents any set of characters in a filename
? , the question mark represents a single character
[ ] , brackets represent character classes

E.g., search for any character that represents a digit [0-9]

The hyphen indicates a range of characters

Recursiveness (-r)

Command history
$ history

The commands are stored with an identifier number, which allows them to be executed from the console by preceding the symbol “!” with the ID

Clear command history
$ history -c

Make a backup of the history and then delete it (Hardening)
$ history >> /var/log/history_date && history -c

Can be automated with a script and crontab

SAMBA service, file sharing service

Text viewers
$ cat “file”

All users created on the system (not system-specific) start from UID 1000

usuario:x:1000:1000:usuario,,,:/home/usuario:/bin/bash

User code UID (usuario:x:1000)
Group code GID (1000:usuario)
User's main folder (/home/usuario)

Groups containing users
/etc/group

Create user
$ useradd
$ adduser (asks for password) (generates more configuration)

Create password
$ passwd “user”

Delete user
$ userdel “user”

DNS information
/etc/resolv.conf

.sh extension

Executable scripts (./script)

Permission structure

Apply to files and directories that are associated with users or groups, and can be for reading, writing, or execution

Permission structure
- Each user is identified by a User ID or UID
- Root or superuser (UID = 0)
- System users. These are linked to certain services, and can assume certain privileges for that service
- Apply to files and directories, are associated with users or groups, and can be for reading, writing, or execution
- Standard Users. There can be as many as required. Each standard user has their personal directory within /home

Permission administration
- User permissions are the first level of privileges, representing the permissions that apply to the owner of a specific file or directory
- Group permissions, which are the second level of privileges, define the rights of reading, writing, and execution that apply only to users belonging to the same group as the file owner
- Other permissions are the last level. Represent the reading, writing, and execution privileges for all other users who do not fall into any of the above levels

Permissions
- R (read) represents the ability to access a file or folder and read its content. In a directory, it refers to the ability to view data
- W (write), Defines the ability to access and modify the contents of a file, or in the case of a directory, the ability to delete or add files to it
- X (execute), These are the most critical. Indicate the ability to execute a specific file in the system. In the case of a directory, execution rights represent the ability to enter the directory

File type / Owner / Group / Others

These 3 permissions can be assigned to the following 4 categories
  u - Owner: owner of the file or directory
  g - Group: group to which the file or directory belongs
  o - Others: all other users who are neither the owner nor belong to the group
  a - All: includes owner, group, and others

Change Permissions
$ chmod (category) (+ to add) (- to remove) “file”

Octal Notation
rwx = 7

r = 4
w = 2
x = 1

$ chmod 777 “file”

Change ownership
$ chown

To change the owner and group of a file, just use:
$ chown user:group “file”

$ chown alumno:alumno "file"

BASH

#!/bin/bash (to start)


25 August 2025
[J x 2] 

 
---

[← Volver al inicio]({{ "/" | relative_url }})
