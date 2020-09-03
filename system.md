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
