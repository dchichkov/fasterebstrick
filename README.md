Faster EBS trick
================

Mixing in ephemeral storage on top of persistant. Or how to unload these unnesesary EBS storage requests onto local storage (or RAM).


Dependencies
============

Ubuntu 11.10+


Usage
=====

Overlay your $BASEDIR directory (located on EBS volume) with /mnt/basedir located on your local hard drive. 
For $BASEDIR This increases available space, performance and also reduces the number of paid requests to EBS. Read requests for old files would still go to your $BASEDIR, but new and modified files would use /mnt/basedir. 
Note that /mnt uses ephemeral storage, and can not survive instance termination.

       sudo mkdir /mnt/basedir
       sudo chown admin:admin /mnt/basedir
       sudo mount -t overlayfs -o lowerdir=$BASEDIR,upperdir=/mnt/basedir overlayfs $BASEDIR

Alternatively - use /var/run (or /run, or /dev/shm depending on your system) instead of /mnt. 
This will overlay your EBS with a RAM disk.
