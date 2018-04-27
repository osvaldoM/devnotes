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
