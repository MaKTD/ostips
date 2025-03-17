# Manual partitioning

### Navigating commands

```sh
# will list block devices 
blkid
# also list block devices
lsblk
# also list devices but output can be better
fdisk -l
# will not list what it do not understand
parted -l
```

### Partitining

#### cgdisk,cfdisk

* if you are using classic MBR partition table - use cfdisk
* if your are using GPT - use cgdisk

```sh
# will enter terminal gui 
cgdisk /dev/disk
cfdisk /dev/disk
```

After enter terminal gui you will see interface, it will allow you manage selected disk partitions, some tips:
* when you prompt to size of sector you can specify in megabytes - 500M, gigabytes - 1G
* you will be guided to this but when your are asked for GUID your can search for them with `L` key

#### fdisk,gdisk

* if you are using MBR - use fdisk
* if you are using GPT - use gdisk

This is terminal based but with prompts by default, 
so a little bit easier than parted if you go manual 

```
# select disk
gdisk /dev/disk
## then you will enter the gdisk shell
# type n to create new partition, then you will be promted and guided
# when you finished type w to write partitions
```



#### parted

This is command line approch, usefull for scripting or if you do not like gui like things

```sh
# Create a GPT partition table
parted /dev/disk -- mklabel gpt
# example of how to create root partition
parted /dev/sda -- mkpart root ext4 512MB -8GB
# example of how to create swap partition, but you can probably go with swap file
# so it is highly optional
parted /dev/sda -- mkpart swap linux-swap -8GB 100%

# example of boot partition
parted /dev/sda -- mkpart ESP fat32 1MB 512MB
parted /dev/sda -- set 3 esp on

# see nix os exampes is links for how to go with parted and mbr 
```

### Links
* [general info about partitioning](https://wiki.archlinux.org/title/Partitioning)
* [nix os great examples of how to go with parted](https://nixos.org/manual/nixos/stable/#sec-installation-manual-partitioning)
* [fdisk and parted guide](https://phoenixnap.com/kb/linux-create-partition)
