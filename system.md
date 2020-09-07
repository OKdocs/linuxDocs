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
