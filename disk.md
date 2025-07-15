# Commands to setup a disk

## How to wipe a disk
```bash
   sudo wipefs -a /dev/yourdisk
```
## How to partition a disk
```bash
   sudo fdisk /dev/yourdisk
```
## How to create a file system
```bash
   sudo fdisk /dev/yourdisk
```
## How to format your file system (applicable to partitions)
```bash
   sudo mkfs.ntfs /dev/yourpartition
```


