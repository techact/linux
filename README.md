# linux

## SSH

###### ssh with user name and password

ssh user@hostname
```
ssh root@xxx.xxx.xxx.xxx
```
###### Remote ssh commands (AWS EC2)
```
ssh -i /path/to/key.pem user@hostname
```
###### Remote scp

Copy file
```
scp -i /path/to/key.pem source_file user@hostname:/destination/path/
```
Copy directory
```
scp -i /path/to/key.pem -r soruce_directory user@hostname:/destination/directory/
```
###### Remote rsync

With root user
```
rsync -avu -e "scp -i /path/to/key.pem -o StrictHostKeyChecking=no" source_file root@hostname:/destination/path/
```
With ubuntu user
```
rsync -avu -e "scp -i /path/to/key.pem -o StrictHostKeyChecking=no" --rsync-path="sudo rsync" source_file ubuntu@hostname:/destination/path/
```
