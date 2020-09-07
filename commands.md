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
  passwd
  ``` 
  change user password
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

## permissions
  owner group all
  ```
  -rw-r--r-- number owner group ...
  ```
  directories
  ```
  drwxrwxrwx numberOfFiles owner group ...
  ```
  
  ##### setting permissions
  
  ```
  chmod [options] file
  ```
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
  
 0 none 
 1 execute permission
 2 write permission
 
 ## change ownership
 
 ```
 chown [options][owner] file
 ```
 
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
  
  
  
