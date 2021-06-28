# EC2-EBS-commands

## Instance 1
```
lsblk ## used to list all block devices attached to EC2 instance.
sudo file -s /dev/xvdf ## to list any file system available on EC2 instance, if response of this command is "data" then there is no file system available. We need to create one if needed.
sudo mkfs -t xfs /dev/xvdf  ## this will create "xfs" type file system on this EBS volume
sudo file -s /dev/xvdf ## This command returns "xfs", if there is file system on EBS else "data" same as above.
sudo mkdir /ebstest ## create directory
sudo mount /dev/xvdf /ebstest ## mount file system to this newly created directory
df -k ## this command list all the file system mounted on the instance
cd /ebstest
sudo nano amazingtestfile.txt
add a message in this text file
save and exit
ls -la
```
## Reboot Instance 1

sudo reboot

## Instance 1 After Reboot
- below commands mount our file system automatically while we launch instance 

df -k
sudo blkid ## this command provides Unique ID for all the EBS volumes attached to instance
sudo nano /etc/fstab
  ADD LINE 
  UUID=YOURUUIDHEREREPLACEME  /ebstest  xfs  defaults,nofail
sudo mount -a
cd /ebstest
ls -la

## Instance 2

lsblk 
sudo file -s /dev/xvdf
sudo mkdir /ebstest
sudo mount /dev/xvdf /ebstest
cd /ebstest
ls -la

## Instance 3

lsblk 
sudo file -s /dev/xvdf
sudo mkdir /ebstest
sudo mount /dev/xvdf /ebstest
cd /ebstest
ls -la

## InstanceStoreTest

lsblk
sudo file -s /dev/nvme1n1 
sudo mkfs -t xfs /dev/nvme1n1
sudo file -s /dev/nvme1n1
sudo mkdir /instancestore
sudo mount /dev/nvme1n1 /instancestore
cd /instancestore
sudo touch instancestore.txt

## InstancStoreTest - After Restart

df -k
its not there
but we can mount it
sudo mount /dev/nvme1n1 /instancestore
cd /instancestore
ls -la

## InstanceStoreTest - After Stop/Start

sudo file -s /dev/nvme1n1
