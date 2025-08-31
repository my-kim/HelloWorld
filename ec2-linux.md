# EC2-Linux

\[ec2-user@ip-10-1-1-101 \~]$ lsblk

NAME MAJ:MIN RM SIZE RO TYPE MOUNTPOINT

xvda 202:0 0 10G 0 disk

└─xvda1 202:1 0 10G 0 part /

​

\[ec2-user@ip-10-1-1-101 \~]$ df -h

Filesystem Size Used Avail Use% Mounted on

devtmpfs 482M 0 482M 0% /dev

tmpfs 492M 0 492M 0% /dev/shm

tmpfs 492M 464K 492M 1% /run

tmpfs 492M 0 492M 0% /sys/fs/cgroup

/dev/xvda1 10G 1.7G 8.4G 17% /

tmpfs 99M 0 99M 0% /run/user/1000

tmpfs 99M 0 99M 0% /run/user/0

​
