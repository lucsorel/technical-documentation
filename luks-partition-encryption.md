This documentation is highly based on [Linux Hard Disk Encryption With LUKS](http://www.cyberciti.biz/hardware/howto-linux-hard-disk-encryption-with-luks-cryptsetup-command/) tutorial.

# Partition setup

This tutorial explains:
* how the logical partition bound to be crypted was created. It is `sda8` here, adapt it to your partition device
* how this partition can be mounted and unmounted. Its mount point here is `~/ciphered`, adapt it to your needs
* the mapper to the crypted partition is also called `ciphered`

## Creation of the partition to encrypt

I used `gparted` to reduce the size of an existing partition and create a new logical one (`sda8` in this tutorial).

## Crypt setup installation

```sh
sudo apt-get install cryptsetup
```
## List the partitions

To list the devices corresponding to your partitions:

 ```sh
 sudo fdisk -l
 ```
 
## Setting the encryption mechanism on the partition

```sh
# SKIP this step if you are creating a mapper to a partition which is already ciphered with LUKS (eg. after a reinstallation)
sudo cryptsetup -y -v luksFormat /dev/sda8
# -> YES (agree to encrypt and loose all the data on the partition)
# -> (type the de/en/cryption passphrase, don't forget it!)

# creates a mapper for /dev/sda8
sudo cryptsetup luksOpen /dev/sda8 ciphered
# -> (type your de/en/cryption passphrase)

# checks the mapper for /dev/sda8
ls -l /dev/mapper/ciphered

# checks the mapper status
sudo cryptsetup -v status ciphered

# LUKS headers of the partition
sudo cryptsetup luksDump /dev/sda8 > ciphered_luks_header.txt

# SKIP this step if you are creating a mapper to a partition which is already ciphered with LUKS
# overwrites the partition with 0s
sudo dd if=/dev/zero of=/dev/mapper/ciphered
# monitors the overwrite progress by running the following command in another terminal
sudo kill -USR1 $(pgrep ^dd)
# to repeat the monitoring every 60s: watch -n60 'sudo kill -USR1 $(pgrep ^dd)'

# SKIP this step if you are creating a mapper to a partition which is already ciphered with LUKS
# creates a filesystem
sudo mkfs.ext4 /dev/mapper/ciphered
```

## Bash scripts to mount and unmount the crypted partition
I have these scripts in my home directory.

* `mount-ciphered.sh`: script to mount the directory (NOTE: in the `chown` instruction, change `USER` by your Linux user name)

```sh
#! /bin/bash
CIPHERED_DIR="~/ciphered"
if [ -d "$CIPHERED_DIR" ]; then
  echo "$CIPHERED_DIR already exists"
else
  echo "creating $CIPHERED_DIR..."
  sudo mkdir -p $CIPHERED_DIR
  sudo chown $USER:$USER $CIPHERED_DIR
  echo "$CIPHERED_DIR created"
fi

sudo umount "$CIPHERED_DIR"
sudo cryptsetup luksOpen /dev/sda8 ciphered
sudo mount /dev/mapper/ciphered "$CIPHERED_DIR"
```

* `umount-ciphered.sh`: script to unmount the directory

```sh
#! /bin/bash
CIPHERED_DIR="~/ciphered"
sudo umount "$CIPHERED_DIR"
sudo cryptsetup luksClose ciphered
```
