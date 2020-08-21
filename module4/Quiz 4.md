# Quiz 4

1. Of the following, which character denotes an ordinary file on the output of the  `ls -l` command? 
   1. `-`
   2. `d`
   3. `l`
   4. `o`
2. Which of the following best describe symbolic links: 
   1. Symbolic links create a link to a specific file anywhere else on the machine, ultimately acting as a shortcut, so that there is one single source of truth.
   2. Symbolic links copy the data of a file into a new directory, similar to the `cp` command, duplicating the data
   3. Symbolic links change the symbols of text so that they link from unicode to their ASCII counterparts.
   4. Symbolic links are directories that used for I/O devices
3. Which of the following is true of a directory with no `read` permissions for a user: 
   1. The user can not see what is in the directory, but can still access its files and subdirectories (given that the user has permissions for those specific files), so long as they know the proper path name. 
   2. The user cannot access any files or subdirectories of the directory, regardless of file permissions. All access is denied. 
   3. The user can still use commands such as `ls` to see the contents of the directory, but the files and subdirectories are not editable.
   4. File permissions only exist on ordinary files. It is not possible for directories to have file permissions. 
4. If a user has no execute permissions for a particular directory, which of the following is true: 
   1. The user will not be able to access the files within the directory or any files in any subdirectories. 
   2. The user will be able to access the files within the directory and subdirectory, but will not be able to view the files (i.e. the directory will appear empty)
   3. The user will only be able to access files if they specifically have a mode of `rwx`, otherwise, they will be inaccessible. 
   4. File permissions only exist on ordinary files. It is not possible for directories to have file permissions. 
5. A file's `i-node` is: 
   1. A special file that contains metadata and pointers to which data blocks contain the file's data
   2. A special file used for connecting input/output devices. 
   3. A name for a file used to store another file's output.
   4. A file that acts as a central node for all files to communicate through via standard input/output.
6. The `i-list` is: 
   1. A single dimensional array of i-nodes that the operating system searches through for commands and files. 
   2. A list of all users on the linux environment
   3. A multi-dimensional array matrix of all users and their associated groups
   4. A list of all input/output devices connected to the system
7. Which of the following is true about using the `-exec` flag with `find`: 
   1. `exec` executes a command with the files returned from find. 
   2. `exec` deletes all files returned by the `find` command
   3. `exec` excludes all files matching the provided string. 
   4. `exec` ensures that the `find` command does not traverse through other directories. 
8. Which of the following is true for the `tar` command: 
   1. `tar` combines, compresses, and decompresses files by differing compression algorithms depending on the argument provided. 
   2. `tar` follows a protocol to connect files over `ssh`
   3. `tar` is a protocol to allow for file transfer
   4. `tar` is a command that traverses the file tree to search files by their mode. 
9. The `sftp` command is used for which of the following: 
   1. Logging into a remote server and securely transferring files back and forth. 
   2. Finding background processes so that they can be killed
   3. The same as `ssh`. `sftp` is an older version of `ssh`, no longer used. 
   4. Logging errors from the file system to the `/etc/errors` file. 
10. Which of the following commands will stop the shell script `doingstuff.sh`: 



```bash
ps
 
 PID TTY          TIME CMD

15688 pts/0    00:00:00 bash

20837 pts/0    00:00:00 cron

20830 pts/0    00:00:00 doingstuff.sh

20831 pts/0    00:00:00 childProcess.sh

20832 pts/0    00:00:00 ps
```



1. `kill -9 20830`
2. ` rm doingStuff.sh`
3. ` stop -9 20832`
4. ` kill 20832`

