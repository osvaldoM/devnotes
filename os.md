[disable annoying unnable to mount device warning](https://askubuntu.com/a/191531)


### delete file based on extension

use it with precaution. Run first:

`find . -name "*.bak" -type f`

then

`find . -name "*.bak" -type f -delete`

### change php version 

** always make sure to have version 7.* of php installed, otherwise an error will be thrown due to the inexistence of the module **

`sudo a2enmod php7.x` followed by:

`systemctl  restart apache2`

 source [https://tecadmin.net/switch-between-multiple-php-version-on-ubuntu/](https://tecadmin.net/switch-between-multiple-php-version-on-ubuntu/)


### check for a package dependencies
    ldd path/to/file
missing dependencies should have a __not present__ tag appended to them

search for the package using apt-search for instance and install it
    
### fix things with shutter
[https://itsfoss.com/shutter-edit-button-disabled/](https://itsfoss.com/shutter-edit-button-disabled/)

## escape wildcards zsh
use backslash to escape wildcard

example `sudo apt-get --purge mysql-\*`

## fix annoying vlc: unnable to open the mrl.....

    sudo apt-get install browser-plugin-vlc
    
    
### install things from unmantained ubuntu releases
this is really usefull in situations where an upgrade to a newer version would not be easy to perform( for instance, if you are using a live ubuntu disc)

 - add old servers addresses to sources file
` 
deb http://old-releases.ubuntu.com/ubuntu/ zesty main restricted
deb http://old-releases.ubuntu.com/ubuntu/ zesty-updates main restrictesudo add-apt-repository ppa:yannubuntu/boot-repair[][d
deb http://old-releases.ubuntu.com/ubuntu/ zesty universe
deb http://old-releases.ubuntu.com/ubuntu/ zesty-updates universe
deb http://old-releases.ubuntu.com/ubuntu/ zesty multiverse
deb http://old-releases.ubuntu.com/ubuntu/ zesty-updates multiverse
deb http://old-releases.ubuntu.com/ubuntu/ zesty-backports main restricted universe multiverse
# deb http://security.ubuntu.com/ubuntu zesty-security main restricted
# deb http://security.ubuntu.com/ubuntu zesty-security universe
# deb http://security.ubuntu.com/ubuntu zesty-security multiverse
deb http://archive.canonical.com/ubuntu zesty partner
`
Things should work now, to install boot-repair, do as follows :
- `sudo add-apt-repository ppa:yannubuntu/boot-repair`
- from software download center , do as described in [this answer](https://askubuntu.com/questions/165255/unable-to-install-boot-repair)
- force download from unauthenticated sources `sudo apt-get update --allow-unauthenticated`
