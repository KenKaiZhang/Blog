# 4 Process Control

A **process** has:

- memory pages: stores any information needed by process
  - can be anywhere and tracked by page tables
- data structures and holds:
  - process address space map
  - current process status
  - process priority
  - resources
  - files and network ports opened
  - signal mask
  - owner

**PID** is the unique identifier associated to each process

A new process is created by cloning the itself and then assigning a task to that process

- original = "parent"
- copy = "child"

**UID** and **EUID** identifies the creator of a process

**GID** and **EGID** identifies the group that owns the process

The EUID and the EGID usually determines the permissions a process has and GID and UID are only importatn when a process creates new files

**`fork`**: a system call that creates a copy of the original process

- unique PID
- unique accounting information

The parent will store the PID of the new child which can be determined by a returned value (0 will indicate child)

A process must get acknowledgement from parent before killing themselves (**`wait`**)

- parents will receive an exit code or indication of why it was killed mainly for error handling, resource cleanup, synchronization, and monitoring tasks

If a child becomes an orphan, then its signals are sent to **init** or **systemd** (they act as their parent)

**Signals**: process-level interupt requests mainly used for process to process communication

One of two things can happen when a signal is received:

1. handler routine is called if one was given
2. default action is taken if none was provided

**MUST KNOW SIGNALS**

- HUP (Hangup)
- INT (Interrupt)
- QUIT (Quit)
- KILL (Kill)
- BUS (Bus Error)
- SEGV (Segmentation Fault)
- TERM (Software Termination)
- STOP (Stop)
- TSTP (Keyboard Stop)
- CONT (Continue After Stop)
- WINCH (Window Change)
- USR1 (User-defined #1)

**`kill`**: signal used to send a signal to a process

- No signal provided defaults to TERM signal
- `kill -9 pid` will kill a process (guarantee with the -9 since that indicates a KILL not TERM)

## Processes and Threads

Process states are inherited by all its threads

Threads within a process can continue execution while one is stuck in a "sleep" state

- a process "sleeps" when all its threads sleeps

**`ps`**: the main tool for monitoring processes

- `ps aux` will show all processes running on system at time of calling
  - a = show all processes
  - u = user oriented output format
  - x = show even process with no control terminal

```
ps Output Explaination

USER - username of the process's owner

PID - Process ID

%CPU - percentage of the CPU process is using

%MEM - percentage of the memory process is using

VSZ - virtual size of the process

RSS - resident set size

TTY - control terminal ID

STAT - current process status
    R = Runnable    D = In uninterruptible sleep
    S = Sleep (< 20s)   T = Traced or stopped
    Z = Zombie

TIME - CPU time consumed

COMMAND - Command name and arguments
```

**`top`** will give you a live view of all the processes and their resource usage

### Niceness

Niceness is basically how much priority a process has over CPU resource

- a numerical "hint" over exact value
- -20 to +19 is the usual range

Children usually inherits parent's niceness

**`nice`** command can be used to custom set the niceness of a process and reset using **`renice`**

- `sudo renice -5 8829` will set nicessness of process 8829 by -5
- `sudo renice 5 username` will set username's processs' niceness by +5

---

Everything is stored within the **`/proc`** directory and the is created on the fly as they are read

**`strace`** command can be used to revewal track actions of a process

- show you the name of every system call made by the process
- decodes all the arguments and shows the result code

**Runaway** processes are those that soak up significantly more of the system's resources than their usual role or behavior should allowed to be

- utilize all the commands on this page to determine a possible issue

## Cron

**`cron`** is the traditional tool for running commands on a predetermined schedule

Starts when the system boots and runs as long as the system is up

Reads from configuration files (**cron tabs**) containing lists of command lines and times at which they should be invoked

You should not change cron tabs directly but use the **`crontab`** command so cron knows when a change has been made

The cron format `minute hour dayofmonth month week command` where:

- minute is 0 -> 59
- hour is 0 -> 23
- day is 1 -> 31
- month is 1 -> 12
- week is 0 -> 6 (0 is Sunday)
- - indicates all

`45 10 * * 1-5` indicates 10:45 AM Monday through Friday

`crontab filename` will make `filename` as the crontab and replace any previous versions of it

`/etc/cron.allow` and `/etc/cron.deny` determines who can submit crom files

## Systemd Timers

Since `systemd` looks to replace all Linux subsystems, it has its own "cron"

Contains 2 files:

- timer unit that describes the schedule and the unit to activate
- service unit that specifies the details of what to run

`systemd` timers can be described in absolute calender terms ("Wednesday at 10:00 am")
