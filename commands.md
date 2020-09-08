# linux commands

## general structure
### shortcuts
  ```!``` last command  
  ```!$``` or ```ESC + .``` last argument  
  ```tab``` autocomplete  
  ```!number``` function number n from history
  ```!string``` previous used function with string name
  shortcut | description
  ---|---
  ^a| jump to beginning of command line
  ^e| jump to end of command line
  ^u| clear from the curser to the beginning of the command line
  ^k| clear from the curser to the end of the command line
  ^left| jump to beginning of previous word on command line
  ^right| jump to the end of the next word on command line
  ^r | search command history
### language specific syntacs
```$(command)``` can be used to replace the command with its output   
example:
  ```sh
  echo The time is $(date +%k:%M)
  ```
  The time is 12:45 (or whatever time is right now)
  ```sh
  a=b
  echo $a
  ```
  prints "b". $a is the variable set before to b
  
  ``` "string $host"``` will  express variable substitution
  ``` 'string $host'``` will suppress variable substitution
## system
  ```sh 
  date
  ```
  display or set system time
  ```sh
  history
  ```
  display command history
  ```sh
  echo
  ```
  display line of text; similar to print string to console in python/go/js etc
  ```sh
  ps
  ```
  dispaly processes ```-u``` user association (who is running the process) ```-a``` all processes
  ## user
  ```sh
  whoami
  ```
  displays user name of logged in user
  ```sh
  id
  ```
  get basic information about user

  ```sh
  su
  ```
  switch user ```su [option] [username]``` ```-c command``` option executes single command as other user ```-``` to switch to root, not always possible for security reasons, if not use ```sudo su```
  
  ### super user permissions
  ```sh 
  su [-]
  ```
  switch to super user account, only works if super user has password
  ```sh
  sudo su[-]
  ```
  switch to super user using user password
  ```sh
  sudo command
  ```
  execute command as super user
  ```sh 
  visudo
  ```
  use vim as super user to edit special files
  
  ### creating and managing users
  ```sh
  useradd username
  ```
  create new user, many options ```-c``` GECOS ```-g``` primary group ```-d``` home directory
  ```sh
  userdel username
  ```
  removes user (removes entry from */etc/passwd*) with ```-r``` also home directory
  ```sh
  passwd
  ``` 
  change user password
  ```sh 
  usermod [options] username
  ```
  modify user account ```-G``` remove user from all groups and add to those stated ```-aG``` append stated groups to groups the user is in. Usually use ```-aG```.
  
## groups

```sh
groupadd [options] groupname
```
create a new group ```-g``` specify GID ```-r``` system group
```sh 
groupmod [options] groupname
```
modify group ```-n newname oldname``` change name
```sh
groupdel [options] groupname
```
delete group

## permissions
  owner group all
  ```
  -rw-r--r-- size owner group ...
  ```
  directories
  ```
  drwxrwxrwx numberOfFiles owner group ...
  ```
  pemission | files | directory
  ---|---|---|
  r | contents of file can be read | contents of directory (file names) can be read (ls command)
  w | contents of file can be changed | new files can be created and all files (independent of file permissions) can be deleted
  x | files can be executed as commands | contents can be accessed (also cd is possible)
  
  ### setting permissions
  
  ```
  chmod [options] file
  ```

 
 #### symbolic method keywords
 ```sh
 chomod WhoWhatWhich file|directory
 ```
 *who*  u==user g==group o==other a==all
 *what* +,-,= (add, remove, set)
 *which* r,w,x (read, write, execute)
 
 #### numeric method
 
```sh
chmod ### file|directory
```
UserGroupOther = [0-7][0-7][0-7]

code|permission|binary
  ---|---|---
  0|none|000
  1|execute|001
  2|write|010
  3|write & execute|011
  4|read|100
  5|read & execute |101
  6|read & write | 110
  7| all|111
  
  ### setting special permissions
  
  u+s == **setuid**  
  g+s == **setgid** 
  o+t == **sticky**  
  
  special permission | effect on files | efect on directories
  --- | --- | ---
  u+s | executes as user that owns, not logged in user | no effect
  g+s | executes as the group that owns | new created files have group owner set to directory group owner
  o+t | no effect | users with write permissions can only remove files they own
  
  #### special permissions numeric method
  
  setuid = 4 setgit =2 sticky = 1
  ```sh
  chmod [0-7][0-7][0-7]0 directory/file
  ```
  ### setting permissions for files created in the future
  
  ```sh
  umask
  ```
  masks permissions for files created, read ```man umask``` well descibed there
 
 ## change ownership
 
 ```sh
 chown [options][owner] file
 ```
 set permissions ```-R``` set recursively for whole directory tree
 
 ```sh
 chown user:group file
 chown :group file
 ```
 chown can also ge used to set user:group ownership or just :group ownership
 
## remote login

##### login with password
```sh
  ssh remoteuser@remotehost
  ```
  
##### login with private key
```sh
  ssh -i "private.key" remoteuser@remotehost
  ```
  private key must be only readable by owner
  
  ```
  chmod 600 file
  ```
     
## files
```sh
  file [filepath]
  ```
  scans beginning of file and returns it'stype
  ```sh
  head [-n number of lines]
  ```
  displayes first lines of file
  ```sh
  tail [-n number of lines]
  ```
  displayes last lines of file
  ```sh
  wc [-lwc] filepath
  ```
  counts lines, words or characters in file
  
  ## file operations
  ```sh
  cp file1 file2/dir
  cp file1 file2 file3 dir
  ```
  copy file ```-r``` cp recursivly (directory with content)
  ```sh
  mv file1 file2/dir
  mv file1 file2 file3 dir
  ```
  move file, file to file = rename
  ```sh
  rm file1
  rm -f file1 file2 file3
  rm -r dir
  ```
  remove file, non-empty directories need ```-r``` to remove files inside recursivly
  ```sh
  mkdir 
  ```
  make directory ```-p``` make whole path of directories
  
  ## navigating paths
  ### current work directory
  ```sh
  pwd
  ```
  print working directory - full path
  ```sh
  ls [options]
  ```
  list directory content
  ```-l``` list long format ```-h``` human readable sizes ```-a``` or ```-A``` print invisible files ```-s``` size (unnecessary with ```-l```) ```-R``` also all content in subdirectories (use with care, might be millions if called on ```/```)
  
  ```sh
  cd [relative/absolute path]
  ``` 
  go to directory ```~``` home directory ```-``` previous directory ```..``` one level up in hierarchy ```cd``` == ```cd ~```
  
  ```sh 
  touch [option]... [file]...
  ```
  update access and modification time to current time, if filename does not exist, create empty file
  
  ### globbing
  
  pattern | matches
  ---|---
  ___*___ | any string of zero or more characters
  ? | any single character
  ~ |current user's home directory
  ~username | user username's home directory
  ~+ | current working directory
  ~- | previous working directory
  [abc...] | any one character in the enclosed class
  [!abc...] or [^abc...] | any one character not in the enclosed class
  [[:alpha:]] | alphabetic character
  [[:upper:]] | upper-case character
  [[:lower:]] | lower-case character
  [[:alnum:]] | alphabetic character or digit
  [[:punct:]] | anything but space or alphanumeric
  [[:digit:]] | digit 0-9
  [[:space:]] | space \t \n \r \f
  
  
  
