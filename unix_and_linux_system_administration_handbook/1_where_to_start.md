# 1. Where to Start

Essential duties of a system admin:

- controlling access
  - create, remove, and handle user accounts (typically automated by a configuration management system)
- adding hardware
- automating tasks
- overseeing backups
- installing and upgrading software
- monitoring
- troubleshooting
- maintaining local documentation
- security
- performance tuning
- developing site policies
- working with vendors
- fire fighting

## Man Pages

**_Concise description of individual commands, drivers, file formate, or library routines_**

Finds the appropriate page wherever it's stored

Sections include

1. user level commands and applications
2. system calls and kernel error codes
3. library calls
4. device drivers and network protocols
5. standard file formats
6. games and demonstrations
7. miscellaneous files and documents
8. system admin commands
9. obscure kernel specs and interfaces

Use `mandb` (Ubuntu) or `makewhatis` (Red Hat and FreeBSD) to update changes made to the man page

`manpath` allows you to view the default search path for the command

- search path can be changed via `export MANPATH=path`

## Software

Use `which` or `whereis` or `locate` to view what binary packages have already been installed

- `which` and `whereis` looks for commands installed by searching the search path
  - `whereis` is independent of the shell's search path and searches a broader range of system directories
- `locate` can find any file in the system (not limited to commands)
  - requires a database update and install

`sudo apt-get install software` will install the `software` using the canonical name

You can also instal via

- source code (download from Git or whereever the project is hosted)
- web script (`curl` usually)
