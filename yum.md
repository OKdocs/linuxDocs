# red hat package manager

package file names: __name-version-release.architecture__
+ NAME one or more words describing the content
+ VERSION is the version number of the original software (2.4.6)
+ RELEASE release number
+ ARCH is the processor architecture the package was compiled to run on. "noarch" is not architecture-specific

```sh 
rpm
```
install, update, remove and query RPM packages, does not resolve dependencies

```sh
yum
```
install individual packages or *package collection* aka *package groups* and takes care of dependencies

**/etc/yum.conf** is main config file for **yum**
**/etc/yum.repos.d** additional repository configuration files
## commands
```sh
yum help
```
display useful info
```sh
yum history
```
summary of install and reove transactions 
```sh 
yum history undo NUMBER
```
reverse transaction, find it's number in history first
### single packages
```sh
yum list
```
displays installed and available packages
```sh
yum search KEYWORD
yum search all KEYWORD
```
lists packages by keywords found in name and summary field with ```all``` also in decription fields
```sh
yum info PACKAGENAME
```
gives information about a package, including disc space needed
```sh
yum provides PATHNAME
```
displays packages that match the pathname
```sh 
yum install PACKAGENAME 
```
obtains and installs package including dependencies
```sh 
yum update [PACKAGENAME]
```
update PACKAGENAME or all packages if no name given
```sh 
yum remove PACKAGENAME
```
removes and installed software package and all that depend on it. And depend on the dependencies. Can lead to unexpected removal of packages 
### package groups
```sh
yum group list
yum grouplist
```
show names of all installed and available groups
```sh
yum group info
yum groupinfo
```
displays info about group, including list of mandatory, default and optional packages, those can be marked as follows:
marker | meaning
--- | ---
__=__ | package is installed, was installed as part of the group
__+__ | package isn't installed, will be if the group is installed or updated
__-__ | package isn't installed, will not be if the group is installed or updated
_no marker_ | package is installed, but was not installed through the group
```sh
yum group install GROUPNAME
yum groupinstall GROUPNAME
```
install group
