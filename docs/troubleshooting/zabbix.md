This servers a my notes for troubleshooting anything related to Zabbix

Problem: Error: “Unable to correct problems, you have held broken packages” while running script to install Zabbix
The installation I was trying had dependencies on other packages that I didn’t have (and was unable to get). These do NOT come with Ubuntu
Solution: Install Debian instead of Ubuntu
The easiest solution was to start over on Debian (which is specifically made to work out of the box with Zabbix) 


Problem: “System Locale = Fail” on Zabbix Pre-requisite check 
 Checking “locale” everything was set to “=C” and was showing LC errors at the top
Troubleshooting steps:
Check status Zabbix components that I installed
Sudo systemctl status zabbix-server (active)
Systemctl status zabbix-agent (active)
Systemcstl status apache2 (active)
Systemctl status php-fpm (not found)
Check if php-fpm is installed
Dpkg -l | grep php | grep | fpm
If it returns blank, it is not installed
Enable and start php-fpm service
Systemctl start php8.2-fpm
Check with systemctl status 
Active
Check if en_US.UTF-8 is generated on my system
Locale -a
Shows that en_US.UTF-8 is missing
Generate the missing file
Locale-gen en_US.UTF-8
Still couldn’t get the locale to show this, it was all set to =C
To get by this, nano /etc/default/locale
Manually enter LANG=”en_US.UTF-8”
Manually enter LC_ALL=”en_US.UTF-8”
This got all but one of the locale to = en_US
Dpkg-reconfigure locales
Selecting en_US.UTF from installer dialog  got it to fully install finally
Solution: en_US.UTF-8 had to be installed and set as the default locale instead of the =C
I tried generating the en_US, which worked bit even when I set the locale to it manually by editing the text file it didn’t work. Turns out it wasn't truly fully installed



Problem: Unable to determine current Zabbix database version: the table “dbversion” was not found
No schema file was found where it usually should be
Manually download scheme and import it into the database
Troubleshooting Steps:
Download Zabbix scheme files
wget https://cdn.zabbix.com/zabbix/sources/stable/7.0/zabbix-7.0.3.tar.gz
tar -xvzf zabbix-7.0.3.tar.gz
cd zabbix-7.0.3/database/mysql
Update to version 7 and create new Zabbix database and import the schema

Problem: Zabbix dashboard shows Zabbix Server is not running, even tho zabbix-server showed active
Solution: editing the Zabbix server config file
The config file /etc/zabbix/zabbix_server.conf had the password commented out
The fix was to remove the # before the line DBPassword=mypassword
This way it was no longer written out

