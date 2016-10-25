# Mysql changing data dir from /var/log/mysql to /data/lib/mysql

### Ubuntu distribution

### 1. Install mysql if not install
'''
apt-get install mysql-server
'''
####### While installing set the root password (and remember).

### 2. Check the default data directory path using the below command
'''
grep datadir /etc/mysql/my.cnf
'''
##### Output
datadir		= /var/lib/mysql/

### 3. Stop MySQL using the following command:
'''
sudo /etc/init.d/mysql stop
  [or]
service mysql stop
'''
### 4. Copy the existing data directory (default located in /var/lib/mysql) using the following command:
'''
cp -R -p /var/lib/mysql /data/lib/mysql
'''
'''
vi /etc/mysql/my.cnf
'''
datadir = /var/lib/mysql
to
datadir = /data/lib/mysql
'''
sudo vi /etc/apparmor.d/usr.sbin.mysqld
change from 
'''
  /var/lib/mysql/ r,
  /var/lib/mysql/** rwk,
 
  to

  /data/lib/mysql/ r,
  /data/lib/mysql/** rwk,

'''
Restart the AppArmor profiles with the command:
'''
/etc/init.d/apparmor reload
/etc/init.d/mysql restart
'''
