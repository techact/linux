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
rsync -avu -e "scp -i /path/to/key.pem -o StrictHostKeyChecking=no" source_file root@hostname:/destination/path/
```sh
With ubuntu user
```sh
rsync -avu -e "scp -i /path/to/key.pem -o StrictHostKeyChecking=no" --rsync-path="sudo rsync" source_file ubuntu@hostname:/destination/path/
```
Remote ssh commands
```sh
ssh -i /path/to/key.pem root@hostname 'uptime'

ssh -i /path/to/key.pem root@hostname "free -m; df -h"
```
```
