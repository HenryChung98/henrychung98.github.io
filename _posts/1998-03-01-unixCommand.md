---
layout: single
title: "Unix Commands"
categories: commands
tags: [unix]
author_profile: false
search: true
---

### shortcuts

| **Command**        | **Description**                                            |
| ------------------ | ---------------------------------------------------------- |
| Navigation         | ---------------------------------------------------        |
| ------------       | ---------------------------------------------------        |
| `ctrl + A`         | move to the beginning of the line                          |
| `ctrl + E`         | move to the end of the line                                |
| `ctrl + U`         | delete from the cursor to the beginning of the line        |
| `ctrl + K`         | delete from the cursor to the end of the line              |
| `ctrl + W`         | delete the word to the left of the cursor                  |
| `ctrl + L`         | clear the screen                                           |
| History            | ---------------------------------------------------        |
| `ctrl + R`         | search backward in history                                 |
| `ctrl + G`         | escape from history searching mode                         |
| `!!`               | repeat the last command                                    |
| `!n`               | repeat the nth command in history                          |
| `!$`               | refer to the last argument of the previous command         |
| process management | ---------------------------------------------------        |
| `ctrl + C`         | interrupt/kill the current foreground process              |
| `ctrl + Z`         | suspend the current foreground process                     |
| `bg`               | put a suspended process in the background                  |
| `fg`               | bring the most recent background process to the foreground |
| file and directory | ---------------------------------------------------        |
| `tab`              | auto-complete file and directory names                     |
| `ctrl + D`         | exit the current shell(or end of input)                    |
| miscellaneous      | ---------------------------------------------------        |
| `ctrl + S`         | stop the output to the screen (XOFF)                       |
| `ctrl + Q`         | resume the output to the screen (XON)                      |
| `ctrl + T`         | swap the last two characters before the cursor             |
| `ctrl + Y`         | paste the last deleted text                                |
| `ctrl + _`         | undo the last change                                       |

### navigation

| **Command**      | **Description**                       |
| ---------------- | ------------------------------------- |
| `pwd`            | Print current working directory.      |
| `ls`             | List files in the current directory.  |
| `ls -a`          | list all files including hidden files |
| `ls -lh`         | formatted list including more data    |
| `ls -t`          | list sorted by date                   |
| `cd [directory]` | Change directory.                     |
| `cd ..`          | Move to the parent directory.         |
| `cd /`           | go to root directory                  |
| `cd ~`           | Move to the home directory.           |

### file operation

| **Command**                     | **Description**                        |
| ------------------------------- | -------------------------------------- |
| `cp [source] [destination]`     | Copy files/directories.                |
| `mv [source] [destination]`     | Move/rename files/directories.         |
| `rm [file]`                     | Remove/delete files.                   |
| `rm -r [dir]`                   | Delete a directory and its files       |
| `mkdir [directory]`             | Create a new directory.                |
| `rmdir [directory]`             | Remove an empty directory.             |
| `touch [file]`                  | Create an empty file.                  |
| `cat [file]`                    | Display the content of a file.         |
| `cat [file1] [file2] > [file3]` | Merge files 1 and 2 into file3         |
| `more [file]` or `less [file]`  | Display content one screen at a time.  |
| `less -N [file]`                | lnclude line numbers                   |
| `less -S [file]`                | wrap long lines                        |
| `man {command}`                 | Display commands manual                |
| `apt-get install`               | Install applications in linux          |
| `head [file]`                   | Display the first few lines of a file. |
| `head -n 5 [file]`              | Display first five lines from a file   |
| `tail [file]`                   | Display the last few lines of a file.  |
| `tail -n 5 [file]`              | Display last five lines from a file.   |

### text handling

| **Command**                           | **Description**                               |
| ------------------------------------- | --------------------------------------------- |
| `echo [message]`                      | Display a message.                            |
| `grep [pattern] [file]`               | Search for a pattern in files.                |
| `sed 's/pattern/replacement/' [file]` | Stream Editor for text replacement.           |
| `awk '{print $1}' [file]`             | Text processing and pattern matching.         |
| `sort [file]`                         | Sort lines of text files.                     |
| `uniq [file]`                         | Remove duplicate lines from a sorted file.    |
| `cut -f [fields] [file]`              | Remove sections from each line of a file.     |
| `tr 'A-Z' 'a-z' < [file]`             | Translate or delete characters.               |
| `wc [file]`                           | Count lines, words, and characters in a file. |
| `paste file1 file2`                   | Merge lines of files.                         |
| `comm file1 file2`                    | Compare two sorted files line by line.        |
| `tee file1 file2`                     | Redirect output to multiple files.            |
| `fmt [file]`                          | Reformat paragraph text.                      |
| `nano [file]`                         | A simple text editor                          |
| `vim [file]`                          | A powerful text editor                        |

### compression

| **Command**                                | **Description**                     |
| ------------------------------------------ | ----------------------------------- |
| `tar -cvf archive.tar [files/directories]` | Create a tar archive.               |
| `gzip [file]`                              | Compress a file using gzip.         |
| `gunzip [file.gz]`                         | Decompress a gzip-compressed file.  |
| `bzip2 [file]`                             | Compress a file using bzip2.        |
| `bunzip2 [file.bz2]`                       | Decompress a bzip2-compressed file. |
| `xz [file]`                                | Compress a file using xz.           |
| `unxz [file.xz]`                           | Decompress an xz-compressed file.   |
| `zip [archive.zip] [files/directories]`    | Create a zip archive.               |
| `unzip [archive.zip]`                      | Extract files from a zip archive.   |

### networking

| **Command**                                | **Description**                                        |
| ------------------------------------------ | ------------------------------------------------------ |
| `ping [hostname or IP]`                    | Test network connectivity.                             |
| `traceroute [hostname or IP]`              | Display the route packets take to reach a destination. |
| `wget [url]`                               | Download a file from an url                            |
| `wget -c [url]`                            | Continue a stopped download                            |
| `nslookup [hostname or IP]`                | Query DNS information.                                 |
| `dig [hostname or IP]`                     | DNS lookup utility.                                    |
| `ifconfig` or `ip a`                       | Display network interfaces.                            |
| `netstat` or `ss`                          | Display network connections.                           |
| `ssh [user@]hostname`                      | Connect to a remote server securely.                   |
| `scp [file] [user@]hostname:[destination]` | Securely copy files between hosts.                     |
| `telnet [hostname or IP] [port]`           | User interface to the TELNET protocol.                 |
| `hostname`                                 | Display or set the system's host name                  |
| `nc [hostname or IP] [port]`               | Netcat - TCP/IP Swiss Army knife.                      |
| `route`                                    | Display or manipulate the IP routing table             |
| `curl {url}`                               | A command-line tool for making HTTP requests           |
| `iptables {options}`                       | Tool to manage kernel Netfilter firewall rules         |

### process management

| **Command**               | **Description**                                     |
| ------------------------- | --------------------------------------------------- |
| `ps`                      | Display your currently active processes             |
| `ps aux`                  | Display information about running processes.        |
| `top` or `htop`           | Display real-time system information and processes. |
| `kill [PID]`              | Terminate a process.                                |
| `killall [process_name]`  | Terminate all processes with a specific name.       |
| `pkill [process_name]`    | Terminate processes based on their name.            |
| `nice [command]`          | Run a command with modified scheduling priority.    |
| `renice [priority] [PID]` | Change the priority of a running process.           |
| `pgrep [process_name]`    | Return process IDs based on their name.             |
| `pmap [PID]`              | Display the memory map of a process.                |
| `pstree`                  | Display running processes in a tree-like structure. |
| `jobs`                    | List background jobs in the current shell session.  |
| `bg [job_number]`         | Put a suspended job in the background.              |
| `fg [job_number]`         | Bring a background job to the foreground.           |

### searching

| **Command**                              | **Description**                                        |
| ---------------------------------------- | ------------------------------------------------------ |
| `find [directory] -name [filename]`      | Search for files and directories.                      |
| `grep [pattern] [file]`                  | Search for a pattern in files.                         |
| `locate [filename]`                      | Quickly find the location of files.                    |
| `which [command]`                        | Show the full path of an executable.                   |
| `whereis [command]`                      | Locate the binary, source, and manual page files.      |
| `ag [pattern] [directory]`               | A faster code searching tool.                          |
| `rg [pattern] [directory]`               | A line-oriented search tool.                           |
| `grep -r [pattern] [directory]`          | Recursively search for a pattern in files.             |
| `find [directory] -exec [command] {} \;` | Find files by name and execute a command on each file. |
| `grep -i [pattern] [file]`               | Search for a pattern in a case-insensitive manner.     |
| `grep -n [pattern] [file]`               | Show line numbers along with matching lines.           |
| `grep -A 2 -B 2 [pattern] [file]`        | Display lines of context around matching lines.        |

### system information

| **Command**          | **Description**                                     |
| -------------------- | --------------------------------------------------- |
| `date`               | Display the current date and time                   |
| `cal`                | Display this month's calendar                       |
| `uname -a`           | Display system information.                         |
| `hostname`           | Display the system hostname.                        |
| `lsb_release -a`     | Display distribution-specific information.          |
| `top` or `htop`      | Display real-time system information and processes. |
| `w`                  | Display who is online                               |
| `whoami`             | Who you are logged in as                            |
| `finger {user}`      | Display information about user                      |
| `uname -a`           | Display kernel information                          |
| `free -m`            | Display memory usage.                               |
| `df -h`              | Display disk space usage.                           |
| `uptime`             | Display system uptime and load average.             |
| `ifconfig` or `ip a` | Display network interfaces.                         |
| `dmesg`              | Display kernel ring buffer.                         |
| `lshw`               | Display detailed hardware configuration.            |
| `lscpu`              | Display CPU information.                            |
| `lsusb`              | Display USB devices.                                |
| `lspci`              | Display PCI devices.                                |
