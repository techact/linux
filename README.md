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

## Mysql changing data dir from /var/lib/mysql to /data/lib/mysql

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
### For openjdk 7
```
echo "export JAVA_HOME="/usr/lib/jvm/java-7-openjdk-amd64/"" >> ~/.bashrc
source ~/.bashrc

echo $JAVA_HOME
/usr/lib/jvm/java-7-openjdk-amd64/
```
###  For printing descending order from a file
```
1. tac file.txt
2. vi file.txt => :g/^/m0
3. cat file.txt | awk '{print NR" "$0}' | sort -k1 -n -r | sed 's/^[^ ]* //g'
4. awk '{a[i++]=$0} END {for (j=i-1; j>=0;) print a[j--] }' file.txt

sed '1!G;h;$!d' file.txt
cat file.txt  | awk '{print NR" "$0}' | sort -nr

http://www.pement.org/awk/awk1line.txt
http://backreference.org/2010/12/19/print-lines-in-reverse-order/
```

### Host Notifications

| Syntax |	Definition | 
| ------------- | ------------- |
| D | Down |
| U | Up |
| R | Recovery |
| F | Flapping |
| S | Scheduled Downtime |

### Service Notifications

| Syntax |	Definition | 
| ------------- | ------------- |
| W | Warning |
| U | Unknown |
| C | Critical |
| F | Flapping |
| S | Scheduled Downtime |
| R | Recovery |
| N | Null |

### Exit codes
A nrpe script or program must generate an exit code (return code) and description.

### nrpe Exit codes (return codes) 
* 0 - Service is OK.
* 1 - Service has a WARNING.
* 2 - Service is in a CRITICAL status.
* 3 - Service status is UNKNOWN.

| Attempt | #1 | #2 |
| :---: | :---: | :---: |
| Seconds | 301 | 283 |

### SSH Tunneling - Port Forwarding (From Local to EC2)

ssh -L local_port_to_access:127.0.0.1:remote_port -i path_to_ssh_private_key username@ipaddress

```
ssh -L 8081:127.0.0.1:80 -i ec2.pem ubuntu@ec2-ip-address
```

Now you can access EC2 web server in your local system using the following url 
```
http://127.0.0.1:8081/
```

### Remote Port Forwarding

ssh -R remote_port:127.0.0.1:local_port_to_listening -i path_to_ssh_private_key ubuntu@ec2-ip-address

```
ssh -R 8081:127.0.0.1:80 -i ec2.pem ubuntu@ec2-ip-address
```
Now you can access your local system in EC2 servr using the following url

```
curl http://127.0.0.1:8081
```
