# The Filesystem

Filesystems are comprised of 4 main components:

1. namespace: a way to name things and organize them in a hierarchy
2. API: a set of system calls for navigating and manipulating objects
3. Security models: schemes for protecting, hiding, and sharing things
4. Implementation: software to tie the logical model to the hardware

**Pathname** shows the list of directories that must be traversed to locate a particular file

- relative or absolute

**`mount`** allows users to attach a external or new filesystem into the tree

- `sudo mount /dev/sda4 /users` mounts `/dev/sda4` under the path `/users`

`mount` by itself will show all the current filesystems mounted

`/etc/fstab` file contains a list of filesystems that are normally mounted to the system

**`unmount`** will do the opposite

The file that contains the OS kernel lives under `/boot`, but can be anywhere under it

`/etc` contains critical system configuration files

`/bin` contains important utilities

`/dev` is now a virtual filesystem that is seperately mounted

`/lib` contains shared libraries and other oddments

`/usr` contains standard but non critical programs

`/var` contains spool directories, log files, accounting information, and various other items that change depending on host

`/tmp` and user directories are usually given their own partitions

## File Types

7 types of files

1. Regular files
2. Directories
3. Character device files
4. Block device files
5. Local domain sockets
6. Named pipes
7. Symbolic links

**`file`** command will tell you the type of file and common formats used

**`ls`** lists all files and directories in a directory

**`rm`** is the universal file removal tool

**Hard links** is basically another name for the same file content

- can be made with the **`ln`** command

**Device files** provide a standard interface for applications to access hardware devices

**Device drivers** are what allow the OS to communicate to the hardware

_Note: Device files allows for communications with drivers_

Device files are characterized by 2 numbers called the major and the minor device numbers:

- major: tells kernel which driver the file refers to
- minor: tells the driver which physical unit to address

**Local domain sockets**: sockets accessible only from the local host and referred to through a filesystem object rather than a network port

- are connections between processes that allow them to communicate
- can be created with the **`socket`** command

**Named pipes (FIFO)**: is an outdated communication mechanism for processes

**Symbolic links** is a refrence to the directory

- basically if you delete a link the directory its pointed to won't be deleted
- created with **`ln -s`**

## File Attributes

Nine permission bits determine what operations can be performed on a file and by whom

- 3 sets of persmission for owner, group, and everyone else
  1. read
  2. write
  3. execute

These bits are usually in terms of octal (base 8)

- 400, 200, 100 for owner
- 40, 20, 10 for group
- 4, 2, 1 for everyone else

Bits with octal values 4000 and 2000 are the setuid and setgid bits which allow programs to access files and processes otherwise off-limits to the user that runs them

- makes it easier to share a directory amongst several users

**`chmod`** allows you to change the permissions of the files

```
0   000   ---       4   100   r--
1   001   --x       5   101   r-x
2   010   -w-       6   110   rw-
3   011   -wx       7   111   rwx
```

So doing 711 is the same as assigning the permissions `rwx --x --x`

**`chown`** and **`chgrp`** changes owner and owner group of a file

- you can also change the ownership of everything under the file with the `-R` flag

**`umask`** can change the default permissions for all files you create

```
0   000   rwx       4   100   -wx
1   001   rw-       5   101   -w-
2   010   r-x       6   110   --x
3   011   r--       7   111   ---
```

## Access Control Lists

**ACLs** are lists the permissions and rules applied to a file

- have no set length and can include specs for multiple users and groups
- each rule is called an **access control entry (ACE)**

Two types of ACLs:

1. POSIX ACLs: the traditional UNIX ACL
2. NFSv4 ACLs: the attempt to unify all ACLs currently out there

Support is OS and filesystem dependent

- ACL could be unable to cross platform
- some systems support multiple ACLs

### POSIX ACLs

Extension of the standard 9 bit UNIX permission model (read, write, execute)

Here are some entries that may appear

```
user::perms
user:username:perms
group::perms
other::perms
```

When a process tries to access a file, its EUID is compared to the UID that owns it

### NFSv4 ACLs

Main difference from POSIX is then specs of the entity to which ACE refers

NFSv4 have:

- distinguishes permission to create files within a directory from permissions to create from subdirectories
- sperate "append" permission bit
  -seperate read and write permissions for data, file attributes, extended attributes, and ACLs
- controls a user's ability to change the ownership of a file through the standard ACL
