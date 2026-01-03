# ✅Linux Interview Questions And Answers✅

## ✅ Basic Linux Questions

## 1) What is Linux?
### Ans: Linux is an open-source operating system where the kernel manages hardware, and users interact using the shell through a terminal.

## 2) Difference between Linux and Windows?
### Ans: 
| Linux                         | Windows                    |
| ----------------------------- | -------------------------- |
| Open source                   | Proprietary                |
| Free to use                   | Paid license               |
| Highly secure & stable        | More vulnerable to malware |
| Mostly command-line driven    | GUI-focused                |
| Preferred for servers & cloud | Mostly desktop use         |


## 3) What is the Linux kernel?
### Ans: The kernel is the core of the Linux operating system.
### It is responsible for:
* Process management
* Memory management
* Device drivers
* File system management
* Hardware communication

## 4) What is a shell?
### Ans: A shell is a command-line interface that allows users to interact with the Linux operating system.
### Examples:
* bash
* sh
* zsh
### It interprets user commands and passes them to the kernel.

## 5) What are the different Linux distributions?
### Ans: Linux distributions (distros) are Linux-based operating systems bundled with tools and package managers.
### Common distros:
* Ubuntu
* CentOS / Rocky Linux
* Red Hat Enterprise Linux (RHEL)
* Amazon Linux
* Debian
* Fedora

## 6) What is the root user?
### Ans: The root user is the superuser in Linux with full administrative privileges.
### Root can:
* Access all files
* Install/remove software
* Modify system configurations

## 7) What is the home directory?
### Ans: The home directory is the personal directory of a user where user files and settings are stored.
### Example:
* /home/username
* /root

## 8) Difference between CLI and GUI?
### Ans: 
| CLI (Command Line Interface) | GUI (Graphical User Interface) |
| ---------------------------- | ------------------------------ |
| Text-based commands          | Visual interface               |
| Faster & powerful            | Easy for beginners             |
| Preferred for servers        | Preferred for desktops         |
| Uses less resources          | Uses more resources            |

## 9) What is open source?
### Ans: Open source means the source code is freely available for anyone to view, modify, and distribute.
### Linux is open source, which makes it:
* Free
* Secure
* Customizable

## 10) What is a terminal?
### Ans: A terminal is a program that provides access to the shell.
### It allows users to:
* Execute commands
* Run scripts
* Manage system operations

## ✅ File & Directory Management

## 1) What is the Linux file system hierarchy?
### Ans: The Linux file system hierarchy is a tree-like structure where all files and directories start from the root / directory.
### Important directories:
* / – Root directory
* /bin – Essential user commands
* /sbin – System/admin commands
* /etc – Configuration files
* /home – User home directories
* /var – Logs and variable data
* /usr – User programs & libraries
* /tmp – Temporary files
* /opt – Optional software packages

## 2) Difference between absolute and relative path?
### Ans: 
| Absolute Path                  | Relative Path                 |
| ------------------------------ | ----------------------------- |
| Starts from `/` (root)         | Starts from current directory |
| Full path                      | Shorter path                  |
| Always same location           | Depends on current directory  |
| Example: `/home/user/file.txt` | Example: `./file.txt`         |


## 3) What are file permissions?
### Ans: File permissions define who can access a file or directory and what actions they can perform.
### Permissions are set for:
* Owner
* Group
* Others

## 4) Explain rwx permissions?
### Ans: 
* r (read) – View file contents / list directory
* w (write) – Modify file / create or delete files in directory
* x (execute) – Run file as program / access directory
### Owner: rwx | Group: r-x | Others: r--

## 5) Difference between file and directory permissions?
### Ans: 
| File Permissions | Directory Permissions      |
| ---------------- | -------------------------- |
| r → Read file    | r → List directory         |
| w → Modify file  | w → Create/Delete files    |
| x → Execute file | x → Enter/access directory |


## 6) What is umask?
### Ans: umask defines the default permission assigned to newly created files and directories.
### Example:
* Default file permission: 666
* Default directory permission: 777
* If umask = 022
* File → 644
* Directory → 755

## 7) Difference between soft link and hard link?
### Ans: 
| Soft Link (Symbolic)   | Hard Link                   |
| ---------------------- | --------------------------- |
| Points to file path    | Points to inode             |
| Can link directories   | Cannot link directories     |
| Breaks if file deleted | Still works if file deleted |
| Uses different inode   | Uses same inode             |


## 8) How do you find a file in Linux?
### Ans: Common commands:
* find /path -name filename
* locate filename
* which command

## 9) How do you check file size?
### Ans: Commands:
* ls -lh filename
* du -h filename
* stat filename

## 10) What is inode?
### Ans: An inode is a data structure that stores metadata about a file.
### It contains:
* File size
* Owner & permissions
* Timestamps
* Disk block location

## ✅ User & Permission Management

## 1) How do you create and delete users?
### Ans: Create a user:
* useradd username
* passwd username
* adduser username
### Delete a user:
* userdel username
### Delete user along with home directory:
* userdel -r username

## 2) What is /etc/passwd and /etc/shadow?
### Ans: /etc/passwd
* Stores user account information
* Readable by all users
* Contains: username, UID, GID, home directory, shell
### /etc/shadow
* Stores encrypted passwords
* Accessible only by root
* Improves system security

## 3) What is a group?
### Ans: A group is a collection of users used to manage permissions easily.
* Users can belong to multiple groups
* Defined in /etc/group
* Simplifies access control

## 4) What is sudo?
### Ans: sudo allows a normal user to run commands with root privileges.
### Benefits:
* Improves security
* Command-level access
* Logged actions
### Configured in:
* /etc/sudoers

## 5) Difference between su and sudo?
### Ans:
| su                     | sudo                            |
| ---------------------- | ------------------------------- |
| Switch user            | Execute command as another user |
| Requires root password | Requires user password          |
| Full root shell        | Limited access                  |
| Less secure            | More secure                     |


## 6) How do you change file ownership?
### Ans:
### Use the chown command: chown user filename
### Change owner and group command: chown user:group filename 

## 7) What is chmod, chown, and chgrp?
### Ans: 
| Command | Purpose                 |
| ------- | ----------------------- |
| `chmod` | Change file permissions |
| `chown` | Change file owner       |
| `chgrp` | Change group ownership  |
### Examples: Command is:
* chmod 755 file.sh
* chown user file.txt
* chgrp dev file.txt

## ✅ Process & System Management

## 1) What is a process?
### Ans: A process is an instance of a running program.
### It includes:
* Program code
* Memory
* CPU usage
* Open files
* Environment variables
### Each process in Linux has a unique ID (PID).

## 2) Difference between process and thread?
### Ans: 
| Process                       | Thread                            |
| ----------------------------- | --------------------------------- |
| Independent program execution | Lightweight unit inside a process |
| Has its own memory space      | Shares memory with other threads  |
| More resource usage           | Less resource usage               |
| Slower context switching      | Faster context switching          |


## 3) What is PID?
### Ans: PID (Process ID) is a unique number assigned to each process by the Linux kernel.
### It is used to:
* Track processes
* Control or terminate processes

## 4) What is zombie process?
### Ans: A zombie process is a process that has completed execution but still has an entry in the process table.
* Occurs when parent does not collect child’s exit status
* Identified by state Z
* Consumes no resources except PID

## 5) What is orphan process?
### Ans: An orphan process is a running process whose parent process has terminated.
* Adopted by init or systemd
* Continues running normally

## 6) Difference between ps, top, and htop?
### Ans: 
| Command | Description                         |
| ------- | ----------------------------------- |
| `ps`    | Static snapshot of processes        |
| `top`   | Real-time process monitoring        |
| `htop`  | Enhanced interactive version of top |

## 7) How do you kill a process?
### Ans: Using kill command: kill PID
### Force kill Command: kill -9 PID
### By name Command: pkill process_name

## 8) What is nice and renice?
### Ans: nice and renice control process priority.
* Priority range: -20 (highest) to 19 (lowest)
* Default priority: 0
### Start process with priority:
* Command is: nice -n 10 command
### Change priority of running process:
* Command is: renice -5 -p PID

