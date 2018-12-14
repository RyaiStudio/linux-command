# Standard Linux Command

#### `ls` - List Directory Contents
List down the files on current path directory
#### `ls -l` - Long Format Listing
display long format listing and which provides a lot more information about the contents. The size of a file or directory is displayed in `bytes`.
    
    [root@centos7 ~]# ls -l
    total 1051924
    -rw-r--r--. 1 root root         41 Sep  1 11:24 abc.zip
    -rw-------. 1 root root        984 Aug 29 14:21 anaconda-ks.cfg

- The `1st column` represents the permissions set on the file or directory. The first character here represents the type of file, for example files start with ‘-‘ while directories start with ‘d’. Therefore we can tell that ‘Downloads’ and ‘test’ are directories as they start with ‘d’.
- The `2nd column` refers to the number of links to the file or directory.
- The `3rd column` shows the user that owns the file or directory.
- The `4th column` shows the group that owns the file or directory.
- The `5th column` shows the file size in bytes of the file or directory.
- The `6th column` shows the last modified date of the file or directory.
- The `7th column` shows the actual name of the file or directory.

#### `li -lh` - Human Readable
use the `-h` option to change the size to human readable format.

    [root@centos7 ~]# ls -lh
    total 1.1G
    -rw-r--r--. 1 root root   41 Sep  1 11:24 abc.zip
    -rw-------. 1 root root  984 Aug 29 14:21 anaconda-ks.cfg
    
#### `ls -la` - Show Hidden Files
display hidden files or directories, that is files or directories that start with the `.` full stop symbol. We can view all hidden contents with ls by using the `-a` option to display all.

    [root@centos7 ~]# ls -la
    total 1051972
    -rw-------.  1 root root      12045 Aug 31 16:41 .bash_history
    -rw-r--r--.  1 root root         18 Dec 29  2013 .bash_logout
    
#### `ls -lr` - Reverse Order
We can reverse this order with the `-r` option.

    [root@centos7 ~]# ls -lr
    total 1051924
    -rw-r--r--. 1 root root    3407872 Sep  1 11:29 z.mp3
    -rw-r--r--. 1 root root        532 Aug 31 12:18 wget-log.txt
    drwxr-xr-x. 4 root root         66 Aug 30 10:32 test
    
#### `ls -lt` - Sort By Modification Time
We can use the -t option to sort the output of `ls` by newest to oldest content. `ls -lrt` to reverse the output.

    [root@centos7 ~]# ls -lrt
    total 1051924
    -rw-r--r--. 1 root root        406 Dec 11  2015 file.txt
    -rw-------. 1 root root        984 Aug 29 14:21 anaconda-ks.cfg

#### `ls -lS` - Sort By File Size
sort the files and directories by size `-S`, largest to smallest.
Again we could combine this with the `-r` option to reverse the results, or `-h` to make the file sizes more readable. Here we do both, and sort files from smallest to largest with human readable sizes.

    root@centos7 ~]# ls -lrSh
    total 1.1G
    -rw-r--r--. 1 root root   41 Sep  1 11:24 abc.zip
    drwxr-xr-x. 4 root root   66 Aug 30 10:32 test
    -rw-r--r--. 1 root root  406 Dec 11  2015 file.txt

#### `ls -ld` - List Only Directories
In the below example, we run `ls -la` on the test directory, and see that the contents within are returned. Once we change it to also use `-d`, we instead see information about the test directory itself, though it’s worth noting this also displays with `-la` as the current directory is shown as `.`

    [root@centos7 ~]# ls -la test/
    total 66192
    drwxr-xr-x. 4 root root       66 Aug 30 10:32 .
    dr-xr-x---. 6 root root     4096 Sep  1 11:41 ..
    -rw-r--r--. 1 root root  2823796 Aug 30 09:39 1.txt
    drwxr-xr-x. 3 root root       30 Aug 30 09:39 test1
    drwxr-xr-x. 3 root root       38 Aug 30 09:40 test2
    
    [root@centos7 ~]# ls -lad test/
    drwxr-xr-x. 4 root root 66 Aug 30 10:32 test/
    
#### `ls -Z` - View SELinux Context
The ls command can display SELinux contexts, which is useful for Linux distributions such as RHEL or CentOS that have SELinux enabled and set to enforcing mode by default.

    [root@centos7 ~]# ls -Z
    -rw-r--r--. root root unconfined_u:object_r:admin_home_t:s0 abc.zip
    -rw-------. root root system_u:object_r:admin_home_t:s0 anaconda-ks.cfg
    drwxr-xr-x. root root unconfined_u:object_r:admin_home_t:s0 Downloads
    -rw-r--r--. root root unconfined_u:object_r:admin_home_t:s0 file.txt

**Note** the size and date columns have now been replaced with SELinux context information, this remains true even if we specify `ls -lZ.`

#### `ls -lR` - List Contents Recursively
We can list the contents recursively with the `-R` option, this will also list the contents within any sub directories that exist inside the directory we are running ls against.

    [root@centos7 ~]# ls -lR test/
    test/:
    total 66188
    -rw-r--r--. 1 root root  2823796 Aug 30 09:39 1.txt
    drwxr-xr-x. 3 root root       30 Aug 30 09:39 test1
    drwxr-xr-x. 3 root root       38 Aug 30 09:40 test2

    test/test1:
    total 2760
    -rw-r--r--. 1 root root 2823796 Aug 30 09:39 1

    test/test2:
    total 5520
    -rw-r--r--. 1 root root 2823796 Aug 30 09:40 7
    -rw-r--r--. 1 root root 2823796 Aug 30 09:40 8

Here we can see that the contents of the test directory are listed, as well as the sub directories inside it called test1 and test2 which both contain some numbered files.

#### `ls -li` - Inode Information
The `-i` option prints the index number of each file, allowing us to see its inode.

    [root@centos7 ~]# ls -li
    total 1051924
    67191492 -rw-r--r--. 1 root root     41 Sep  1 11:24 abc.zip
    67869919 -rw-------. 1 root root    984 Aug 29 14:21 anaconda-ks.cfg
    145701 drwxr-xr-x. 2 root root     4096 Aug 31 13:58 Downloads
    145703 drwxr-xr-x. 4 root root       66 Aug 30 10:32 test

#### `ls -p` - Indicate Directory
We can also use the `-p` option which will add a `/` to the end of directories, making it a little more obvious.

    [root@centos7 ~]# ls -p
    abc.zip  anaconda-ks.cfg  Downloads/  file.txt  test/  wget-log.txt
    
#### `ls -F` - Classify Content With Symbols
`-F` can also be used to append various symbols to the end of different types of files. The `-F` option will also add a `/` to the end of a file, but will also add a `@` to the end of a link, and a `*` to the end of an executable file, allowing us to easily visually classify the file and directory output of ls.

    [root@centos7 ~]# ls -F
    abc.zip  Downloads/  file.txt  script.sh*  swapfile  test/  tmp-link@

#### `alias | grep ls` - Classify Content With Colours
We can also classify by adding colour using the --color option, as you may have noticed this is enabled by default in many Linux distributions such as CentOS.

In CentOS this is aliased to actually run ls with `--color=auto` every time, which will change the colours of the output based on things like file extension. It can help you visually distinguish between files and directories.

    [root@centos7 ~]# alias | grep ls
    alias l.='ls -d .* --color=auto'
    alias ll='ls -l --color=auto'
    alias ls='ls --color=auto'
![Alt text](https://github.com/private-ryan23/linux-command/blob/master/img/linux-ls-color.png)
We can disable the colouring with `--color=never`

#### `ls -gG` - Hide User Or Group
With the `-l` option we can see the user and group that owns a file or directory. Using the `-g` option we can hide the user, and while using the `-G` option we can hide the group. Both can be run together to hide both the user and group information.

    [root@centos7 ~]# ls -gG
    total 1051928
    -rw-r--r--. 1         41 Sep  1 11:24 abc.zip
    -rw-------. 1        984 Aug 29 14:21 anaconda-ks.cfg
    drwxr-xr-x. 2       4096 Aug 31 13:58 Downloads

#### `ls -n` - List User And Group IDs
We can see the `UID/GID` owner of a file or directory with the `-n` option. By default the `UID/GID` values are enumerated if the user or group exists, however we can force ls to display the `UID/GID` number with this.

    [root@centos7 ~]# ls -l /home/
    total 0
    drwx------. 2 user1 user1 79 Aug 30 11:29 user1
    drwx------. 2 user2 user2 79 Aug 30 11:30 user2

    [root@centos7 ~]# ls -n /home/
    total 0
    drwx------. 2 1000 1000 79 Aug 30 11:29 user1
    drwx------. 2 1001 1001 79 Aug 30 11:30 user2

#### `ls -lX` - Sort By File Extension
We can also sort the ls output based on the file extension with the `-X` option, which will arrange the output in alphabetical order based on the extension.

    [root@centos7 ~]# ls -lX
    total 1051928
    drwxr-xr-x. 2 root root       4096 Aug 31 13:58 Downloads
    -rw-------. 1 root root        984 Aug 29 14:21 anaconda-ks.cfg
    -rw-r--r--. 1 root root    3407872 Sep  1 11:29 z.mp3
    -rwxr-xr-x. 1 root root         45 Sep  1 12:02 script.sh

#### `ls -A` - Show Almost All
We can show almost all with the `-A` option, this works in a similar way to `-a` discussed previously, but ignores the current directory `.` and the directory above `..` from the results.

    [root@centos7 ~]# ls -A
    abc.zip          .bash_history  .bash_profile  Downloads  .lesshst  test 
    anaconda-ks.cfg  .bash_logout   .bashrc        tmp-link     wget-log.txt

    [root@centos7 ~]# ls -a
    .   abc.zip          .bash_history  .bash_profile  Downloads  .lesshst 
    ..  anaconda-ks.cfg  .bash_logout   .bashrc        tmp-link    wget-log.txt

We can see that `-a` includes `.` and `..` listed in the output while the results from `-A` do not.

#### `ls -1` - isplay One Entry Per Line
with the -1 option we can instead list one file or directory per line.

    [root@centos7 ~]# ls -1
    abc.zip
    anaconda-ks.cfg
    Downloads
    file.txt

#### `ls --version` - Show Version
We can display the verison of our ls command with the --verison option.

    [root@centos7 ~]# ls --version
    ls (GNU coreutils) 8.22
    Copyright (C) 2013 Free Software Foundation, Inc.
    License GPLv3+: GNU GPL version 3 or later .
    This is free software: you are free to change and redistribute it.
    There is NO WARRANTY, to the extent permitted by law.

    Written by Richard M. Stallman and David MacKenzie.

#### `ls --help` - Show Help
If you need any further assistance with the ls command, run it with the `--help` option which will provide further information and documentation.

    [root@centos7 ~]# ls --help
    Usage: ls [OPTION]... [FILE]...

**NOTE** that I have not included all of the output here for brevity.
