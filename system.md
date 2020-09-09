# linux 

## distributions

+ RHEL (Red Hat Enterprise Linux)
+ CentOS (free RHEL clone)
+ Fedora (upstream experimental branch)

## filesystem

location | purpose
---|---
/usr | installed software, shared libraries 
/usr/bin | user commands
/usr/sbin | system admin commands
/usr/local | locally customized software
/etc | configuration files specific to the system
/var | variable data specific to this system that should persist between boots
/run | runtime data for processes started since the last boot
/home | home directories where regular users store their personal data and configuration files
/root | home directory for the administrative superuser, root
/temp | space for temporary files, auto delete after 10 days
/boot | files needed for boot process
/dev | contains special device files which are used by the system to access hardware

## user

```$``` superuser

```#``` regular user

/etc/passwd
```username:password:UID:GID:GECOS:/home/dir:shell```

item | description
---|---
username | mapping of UID to a name for benefit of human users
password | vestigial datafield, always ___x___
UID | user ID
GID | group ID
GECOS | real name or software name (z.B Postgres Administrator)
/home/dir | path to user's home directory
shell | the shell he is using

## groups

/etc/group
```groupname:password:GID:list of users
```

## processes
consists of *process* and *environment*

**process**
+ and address space of allocated memory
+ security properties including ownership credentials and privileges
+ one or more execution threads of program code
+ process state
**environmen**
+ local and global variables
+ current scheduling context
+ allocated system resources (file descriptors, network ports)

parent processes **fork** child processes which can inherit process and environment

### process states
<table>
  <tr>
    <th>name</th>
    <th>flag</th>
    <th>kernel-defined state name description</th>
  </tr>
  <tr>
    <td>RUNNING</td>
    <td> <b>R</b> </td>
    <td>TASK_RUNNING: executing on CPU or waiting to run</td>
  </tr>
   <tr>
    <td rowspan=4>SLEEPING</td>
     <td><b>S</b></td>
    <td>TASK_INTERRUPTIBLE: waiting for condition: when event or signal satisfies the condition, process return to RUNNING</td>
  </tr>
   <tr>
    <td><b>D</b></td>
    <td>TASK_UNINTERRUPTIBLE: sleeping and not responding to signals, if killed, may cause unpredictable device state</td>
  </tr>
  <tr>
    <td><b>I</b></td>
    <td>TASK_UNINTERRUPTABLE | TASK_NOLOAD: idle threads that do not require any load / don't use any resources. Just ignore processes marked as <b>I</b>
   <tr>
    <td><b>K</b></td>
    <td>TASK_KILLABLE: sleeping and not waiting for signal but if killed everything is going to be alright</td>
  </tr>
   <tr>
    <td rowspan=2>STOPPED</td>
    <td><b>T</b></td>
    <td>TASK_STOPPED: Stopped by user or other process. Can return to RUNNING by another signal</td>
  </tr>
   <tr>
    <td><b>T</b></td>
    <td>TASK_TRACED: temporarily stopped for debugging</td>
  </tr>
   <tr>
    <td rowspan=2>ZOMBIE</td>
    <td><b>Z</b></td>
    <td>EXIT_ZOMBIE: exit signal from child process to parent, all but PID are released</td>
  </tr>
   <tr>
    <td><b>X</b></td>
    <td>EXIT_DEAD: after parent process reaps remaining child process structure, process is released completely. Will never be observed in process-listing utilities </td>
</table>
  
Jobs (process pipelines started from prompt) can run in the *foreground* or in the *background*, only one job per console can run in the *foreground* taking control over it's input. Both *foreground* and *background* can write to the terminal, but only the *foreground* can read inputs.

Processes started from the system and not from the shell prompt, like *system deamons*, aren't members of a job and cannot be brought to the *foreground*.

Processes can be started in the *background* by adding an ampersand (**&**) to the end of the command line.
```sh
command [options] [target] &
```
### process control

#### fundamental process management signals

short names (**HUP**) add **SIG** to become proper name (**SIGHUP**)

signal number | short name | definition | purpose
--- | --- | --- | ---
1 | **HUP** | Hangup | report termination of controlling process or request process reinitialization without termination
2 | **INT** | Keyboard interrupt | program termination, can be blocked or handled (**ctrl** + **c**)
3 | **QUIT** | Keyboard quit | same as **SIGINT** but also produces process dump 
4 | **KILL** | Kill, unblockable | abrupt program termination, unblockable; always fatal
15 | **TERM** | Terminate | program termination, can be blocked and handled and allows self-cleanup. Nearly identical to **SIGINT**
18 | **CONT** | Continue | resume stopped process
19 | **STOP** | Stop, unblockable | suspends the process, cannot be blocked or handled
20 | **TSTP** | Keyboard stop | suspends the process, can be blocked and handled (**ctrl** + **z**)

