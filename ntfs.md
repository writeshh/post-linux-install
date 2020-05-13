# Introduction

These instructions cover configuring a NTFS disk containing Steam games, that was previously used in a Windows environment, to work with Proton on Linux. This allows a user to use the same files to play games on both Windows and Linux without needing to reinstall games for each operating system.

# Tested On

- Ubuntu 18.10
- Ubuntu 19.04
- Pop!_OS 18.10
- Pop!_OS 19.04

# Configuring and Automounting the NTFS Partition

## Create a Mount Point

Create a mount point for the NTFS game disk:
```
$ sudo mkdir /media/gamedisk
```

Find the User ID, Group ID, attached disk partition, and the UUID using the following commands:

**User ID**
```
$ id -u
```
**Group ID**
```
$ id -g
```

By default, both should be `1000`

**Attached Disk Partition**
```
$ sudo fdisk -l
```
It should be labeled similar to `/dev/sda2` 

*The trailing letter and number (a2) will depend on how many disks are attached.*

**UUID**
```
$ sudo blkid
```

Find the line where the first column matches the label of the `fdisk` command. 

For example, `/dev/sda2` would match this line:
```
...
/dev/sda2: UUID="38CE9483CE943AD8" TYPE="ntfs" 
...
```
Copy the UUID.

## Editing fstab
Edit the *fstab* file to mount the partition:
```
$ sudo nano /etc/fstab
```
At the bottom of the file, add the following line (changing UUID, uid, and gid where needed):
```
UUID=38CE9483CE943AD8 /media/gamedisk ntfs uid=1000,gid=1000,rw,user,exec,umask=000 0 0
```
*On Ubuntu, as long as `ntfs-3g` is installed using `ntfs` as the filesystem type will work*

Reboot the computer for the changes to take effect:
```
$ sudo reboot
```

## Preventing NTFS Read Errors
**THERE HAS BEEN A REPORT THAT THIS MAY CAUSE DATA LOSS**

Due to the nature of NTFS, creating files/folders with characters Windows cannot read will cause disk errors (leading to games that don't launch), the most common issue is a `;` character in filenames that Proton creates on the NTFS disk.

Fixing this is pretty simple. Create a symlink from the `/compatdata` folder on Linux to the mounted NTFS disk.

Creating the symlink:

```
$ ln -s ~/.steam/steam/steamapps/compatdata /media/gamedisk/Steam/steamapps/
```

*If the `/compatdata` folder already exists on the mounted disk BEFORE the syslink, DELETE IT!*
