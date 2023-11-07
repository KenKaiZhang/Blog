# 7 Scripting and the Shell

Writing scriptlets to complete tedious tasks is common

```sh
function backup() {
    newname = $1.`date +%Y-%m-%d.%H%M.bak`;
    mv $1 $newname;
    echo "Backed up $1 to $newname.";
    cp -p $newname $1;
}
```

_Heres a script that will backup files and can be called with `backup filename`_

Shell functions are not stored in memory so needs to be reparsed every time a new shell starts

- annoying but negligible in todays' systems

Good script making practices:

- should print a message for usage and exit
- validate inputs and sanity check derived values
- return meaningful exit code
- use appropriate naming conventions
- develop a style guide
- add comment block that describes what the script does and the parametes
- comment more
- dont' clutter
- it's ok to run scripts as root but avoid making them setuid
- don't script dumb shit
- adapt code
- use `-x` to echo commands before execution and `-n` to check commands for syntax

## Shell

**Bash** is the standard **sh** option

**Emac** (a POSIX command editor) commands are available in the shell:

- `Control-P`: step backward through recently executed commands
- `Control-R`: searches incrmentally through history
- `Control-E`: go to end of line
- `Control-A`: go to the beginning of line

Each process has 3 communication channels available at least:

0. STDIN (standard input)
1. STDOUT (standard output)
2. STDERR (standard error)

There are 3 symbols for rerouting commands input or ouput to or from file

- **`>`**: redirects the outputs and replaces contents of file if to a file
- **`>>`**: redirects the outputs and appends to the contents of file if to a file
- **`<`**: redirects the output of the right argument as an input for the left

**`&&`** will run the second command if and only if the first one executes properly

**`||`** will run if the preceding command fails

**`;`** combines multiple commands onto one line

**`$`** in front of a variable indicates an actual variable and called for refrence

```sh
$ etcdir='/etc'
$ echo ${etcdir}
/etc
```

_Note: You don't need the {}, but it makes the code more readable_

Variable names are cases sensitve

Backticks will be treated as double quotes but will be replaced with the command's output

```sh
$ echo "There are `wc -l < /etc/passwd` lines in the passwd file"
There are 19 lines in the passwd file
```

Set up environment variables that you want to set up on start up in **~/.profile**

**`cut`** command prints selected portions of its inputlines

**`sort`** will sort its input lines

**`uniq`** will remove any **ADJACENT** repeating lines

- usually used with `sort` to remove all of them

**`wc`** counts the number of lines (`-l`), word (`-w`), and characters (`-c`) in a file

- without any flags it does all 3

**`tee`** sends its standard input both to standard out and to a file specified

- `find / -name core | tee /dev/tty | wc -l` will look for files named `core` in the `/` directory and then pipe the result to `tee /dev/tty` which will write the result into `dev/tty` and pipe it to the `wc -l`
  - anything written into `/dev/tty` will be written to terminal

**`head`** and **`tail`** will read the beginning or the end of a file

**`grep`** search text using regular expressions

## `sh` Scripting

Always start with a **`#!/bin/sh` (shebang)** which indicates the file to be script interpreted by bash

Usually needs to be given execution permissions and then called with **`sh scriptname`**
