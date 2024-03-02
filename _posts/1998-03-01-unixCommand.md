---
layout: single
title: "Unix Commands"
categories: commands
tags: [unix]
author_profile: false
search: true
---

### shortcuts

| Command            | Description                                                |
| ------------------ | ---------------------------------------------------------- |
| Navigation         | ---------------------------------------------------        |
| ------------       | ---------------------------------------------------        |
| **ctrl + A**       | move to the beginning of the line                          |
| **ctrl + E**       | move to the end of the line                                |
| **ctrl + U**       | delete from the cursor to the beginning of the line        |
| **ctrl + K**       | delete from the cursor to the end of the line              |
| **ctrl + W**       | delete the word to the left of the cursor                  |
| **ctrl + L**       | clear the screen                                           |
| History            | ---------------------------------------------------        |
| **ctrl + R**       | search backward in history                                 |
| **ctrl + G**       | escape from history searching mode                         |
| **!!**             | repeat the last command                                    |
| **!n**             | repeat the nth command in history                          |
| **!$**             | refer to the last argument of the previous command         |
| process management | ---------------------------------------------------        |
| **ctrl + C**       | interrupt/kill the current foreground process              |
| **ctrl + Z**       | suspend the current foreground process                     |
| **bg**             | put a suspended process in the background                  |
| **fg**             | bring the most recent background process to the foreground |
| file and directory | ---------------------------------------------------        |
| **tab**            | auto-complete file and directory names                     |
| **ctrl + D**       | exit the current shell(or end of input)                    |
| miscellaneous      | ---------------------------------------------------        |
| **ctrl + S**       | stop the output to the screen (XOFF)                       |
| **ctrl + Q**       | resume the output to the screen (XON)                      |
| **ctrl + T**       | swap the last two characters before the cursor             |
| **ctrl + Y**       | paste the last deleted text                                |
| **ctrl + _**       | undo the last change                                       |

### file system

| Command                   | Description                           |
| ------------------------- | ------------------------------------- |
| **ls**                    | list directories and files            |
| **ls -a**                 | list all files including hidden files |
| **ls -lh**                | formatted list including more data    |
| **ls -t**                 | list sorted by date                   |
| **pwd**                   | return path to working directory      |
| **cd {dir}**              | change directory                      |
| **cd ..**                 | go to parent directory                |
| **cd /**                  | go to root directory                  |
| **cd**                    | go to home directory                  |
| **touch**                 | create en empty file                  |
| **cp {file} {file_copy}** | copy a file                           |
| **cp -r**                 | copy files contained in directories   |
| **rm {file}**             | delete a file                         |
| **rm -r {dir}**           | delete a directory and its files      |
| **mv {file1} {file2}**    | move or renames a file                |
| **mkdir {dir_name}**      | create a directory                    |
| **rmdir {dir_name}**      | delete a directory                    |
| **locate {file_name}**    | search a file                         |
| **man {command}**         | show commands manual                  |
| **top**                   | show process activity                 |
| **df -h**                 | show disk space info                  |
| **apt-get install**       | install applications in linux         |

### text handling

| Command                           | Description                                        |
| --------------------------------- | -------------------------------------------------- |
| **cat {file}**                    | concatenate and print files                        |
| **cat {file1} {file2} > {file3}** | merge files 1 and 2 into file3                     |
| **head {file}**                   | print first lines from a file                      |
| **head -n 5 {file}**              | print first five lines from a file                 |
| **tail {file}**                   | print last lines from a file                       |
| **tail -n 5 {file}**              | print last five lines from a file                  |
| **more {file}**                   | display the content of a file one screen at a time |
| **less {file}**                   | view a file                                        |
| **less -N {file}**                | lnclude line numbers                               |
| **less -S {file}**                | wrap long lines                                    |
| **grep 'pattern' {file}**         | print lines matching a pattern                     |
| **grep -c 'pattern' {file}**      | count lines matching a pattern                     |
| **cut -f 1,3 {file}**             | remove sections from each line of a file           |
| **sort {file}**                   | sort lines from a file                             |
| **sort -u {file}**                | sort and return unique lines                       |
| **uniq -c {file}**                | filter adjacent repeated lines                     |
| **wc {file}**                     | count lines, words and bytes                       |
| **paste {file1} {file2}**         | concatenate the lines of input files               |
| **paste -d ","**                  | concatenate the lines of input files by commas     |
| **sed**                           | Stream Editor for filtering and transforming text  |
| **echo {message or variable}**    | display a message or the value of a variable       |
| **nano {file}**                   | a simple text editor                               |
| **vim {file}**                    | a powerful text editor                             |
| **comm {file1} {file2}**          | compare two sorted files line by line              |

### compression

| command                                       | description                                 |
| --------------------------------------------- | ------------------------------------------- |
| **gzip {file}**                               | compress a file                             |
| **gunzip {file}**                             | decompress a file                           |
| **tar -cvf archive.tar {files/directories}**  | group files                                 |
| **tar -xvf archive.tar {files/directories}**  | ungroup files                               |
| **tar -zcvf archive.tar {files/directories}** | group and gzip files                        |
| **tar -zxvf archive.tar {files/directories}** | gunzip and ungroups files                   |
| **zcat {files/gz}**                           | view compressed files without decompressing |

### networking

| Command                 | Description                                    |
| ----------------------- | ---------------------------------------------- |
| **ping {host or IP}**   | ping host and output results                   |
| **wget {url}**          | download a file from an url                    |
| **wget -c {url}**       | continue a stopped download                    |
| **dig domain**          | get DNS information for domain                 |
| **ssh user@server**     | connect to a server                            |
| **scp**                 | copy files between computers                   |
| **ifconfig**            | configure and display network interfaces       |
| **route**               | show or manipulate the IP routing table        |
| **curl {url}**          | a command-line tool for making HTTP requests   |
| **ssh {user@hostname}** | onnect to a remote server securely             |
| **iptables {options}**  | tool to manage kernel Netfilter firewall rules |
| **hostname**            | show or set the system's host name             |
