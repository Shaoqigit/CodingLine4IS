# Linux shell notion/commands
---

- prompt is the first concept you should know, which is simply you see on a terminal such as below:
  `[shaoqi@MYPC:~/Document (main)$]`
- `echo` as a printer function to display the variable or commands.

- `$PATH` is a very important variable as **environment variable**
this variable stores all the path that will be used sequently to search for certain program/commands
For example, if you install/build/compile a new program on your Linux, you may need to add your program **path** into the variable `$PATH`. Otherwise, your system can not find your program anywhere via shell.
dollar symbol represent the variable `$`,
`$_` the last used argument as varaiable

- `which` is to return you the path of a program:
  e.g. if you type
  `which echo` 
  `>>> /usr/bin/echo` showing that the commands `echo` is installed in above absolute path in command linux system.

- `pwd`: print work directory
  as indicated as name, which return the **absolute path** of current work directory.

- `cd` represents **c**hange **d**irectory , which is the **most** daily command you will use
  some special directory:
  `cd .` current direct
  `cd ..` parent direct
  `cd -` the previous direct you are in

- `ls`: list the files/folder in current directory
  `ls -l` use a long listing format
  `ls -a` list **all** files including *hidden* files

- `find`: find the file
  e.g `find -name '*XX'`
  `find . -name src -type d` find all the file in *current directory*(`.`) with *name* src and *type* d. 
  `locate`
  anther similar command `grep` to search for content in file: `grep -R CONTENT`
- `history`:
- `xdg open`

- Ownership needs to be cared in Linux: permission and group
  `chmod`, `chown` and `chgrp`
  `chown OWNERNAME file_name`
  `chrgp GRP_NAME file_name`
   

- `mv CURR_PATH TARG_PATH` move, can be used to **rename** a file
- `rm` remove/delete
  `rm -r` remove the directory recursively
- `cp` copy and `scp` secure copy
- `man COMMAND` manual
- `CTRL+L` or `clear`: clear the terminal and prompt to top
- Disk related: check disk usage information -> `df`, check current directory disk ranking -> `du -hs $PATH | sort -rh | head -16`

---
## Tricky commands

- `convert` e.g `convert image.png image.jpg`
- `{}` make you do some combined things, e.g
  `touch toto{,1,2,30}.txt` equivalent to `touch toto.txt toto1.txt toto2.txt toto30.txt`
- `diff` compare two files
- Tool call `tree`
- `shellcheck`

---

## concept of stream

- `>` and `<` overwrite
  e.g `echo hello > hello.txt` the echo returned content will be stored in file hello.txt
  `>>` append

## concept of pip: wire/combine different program/commands

- `|`
  `ls -l | tail -n1`

---

`cd /sys` kernel
run shell as root `sudo su`

## dirctory system
- bin: binaries, all the functions and applications used
  sbin: system binary 
- dev: devices
- etc: system-wide configuration
- lib/lib32/lib64
- media&mnt : external disks
- opt:
- proc: process
- root
- sys
- usr: user application
- var: variables
- **home**:
