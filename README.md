# linux

## SSH

###### ssh with user name and password

ssh user@hostname
```bash
ssh root@xxx.xxx.xxx.xxx
```
###### Remote ssh commands (AWS EC2)
```sh
ssh -i /path/to/key.pem user@hostname
```
###### Remote scp

Copy file
```sh
scp -i /path/to/key.pem source_file user@hostname:/destination/path/
```
Copy directory
```sh
scp -i /path/to/key.pem -r soruce_directory user@hostname:/destination/directory/
```
###### Remote rsync

With root user
```sh
rsync -avu -e "ssh -i /path/to/key.pem -o StrictHostKeyChecking=no" source_file root@hostname:/destination/path/
```
With ubuntu user
```sh
rsync -avu -e "ssh -i /path/to/key.pem -o StrictHostKeyChecking=no" --rsync-path="sudo rsync" source_file ubuntu@hostname:/destination/path/
```
Remote ssh commands
```sh
ssh -i /path/to/key.pem root@hostname 'uptime'
ssh -i /path/to/key.pem root@hostname "free -m; df -h"
```

## Mysql changing data dir from /var/log/mysql to /data/lib/mysql

### Ubuntu distribution

### 1. Install mysql if not install
```sh
apt-get install mysql-server
```
####### While installing set the root password (and remember).

### 2. Check the default data directory path using the below command
```sh
grep datadir /etc/mysql/my.cnf
```
##### Output
datadir		= /var/lib/mysql/

### 3. Stop MySQL using the following command:
```sh
sudo /etc/init.d/mysql stop
  [or]
service mysql stop
```
### 4. Copy the existing data directory (default located in /var/lib/mysql) using the following command:
```sh
cp -R -p /var/lib/mysql /data/lib/mysql
```
```sh
vi /etc/mysql/my.cnf
```
datadir = /var/lib/mysql
to
datadir = /data/lib/mysql
```sh
sudo vi /etc/apparmor.d/usr.sbin.mysqld

change from 
  /var/lib/mysql/ r,
  /var/lib/mysql/** rwk,
 
  to

  /data/lib/mysql/ r,
  /data/lib/mysql/** rwk,

```
Restart the AppArmor profiles with the command:
```sh
/etc/init.d/apparmor reload
/etc/init.d/mysql restart
```

### Install openjdk on ubuntu 14.04
```
sudo add-apt-repository ppa:openjdk-r/ppa
sudo apt-get update 
sudo apt-get install openjdk-8-jdk
sudo update-alternatives --config java
Type in a number to select a Java version.

set default java version
openjdk version "1.8.0_111"
OpenJDK Runtime Environment (build 1.8.0_111-8u111-b14-3~14.04.1-b14)
OpenJDK 64-Bit Server VM (build 25.111-b14, mixed mode)
```
