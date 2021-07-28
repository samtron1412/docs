[TOC]

# Overview
- [Wikipedia](https://en.wikipedia.org/wiki/Raspberry_Pi)

The Raspberry Pi is a series of credit card-sized sing-board computers was developed in the United Kingdom by the Raspberry Pi Foundation with the intent to promote the teaching of basic computer science in schools and developing countries.

# [Set up](https://www.raspberrypi.org/documentation/setup/)
## SD card
The `dd` command is the Linux block copy command. It reads from the `if=` file, in the first case a block of zeros, and writes to the `of=` file, in the first case the file named `test.tmp` in your **HOME** directory (the `~/` means your HOME directory, change this to the mount point of the card). The `bs=` gives the size of the data, and the `count=` gives the number of times this is repeated. `sync` ensures that the filesystem cache is flushed to have more realistic data. Please run it multiple times, one sample is not scientific enough.

Write speed

	sync; dd if=/dev/zero of=~/test.tmp bs=500K count=1024

Read speed

	sync; echo 3 | sudo tee /proc/sys/vm/drop_caches
	sync; time dd if=~/test.tmp of=/dev/null bs=500K count=1024

Delete the temporary file

	rm ~/test.tmp

# [Installation](https://www.raspberrypi.org/documentation/installation/)

# [Remote access](https://www.raspberrypi.org/documentation/remote-access/)

# [Usage](https://www.raspberrypi.org/documentation/usage/)

# [Configuration](https://www.raspberrypi.org/documentation/configuration/)

# [Hardware](https://www.raspberrypi.org/documentation/hardware/raspberrypi/README.md)

# [ArchLinux ARM](https://archlinuxarm.org/)
- [Arch Wiki](https://wiki.archlinux.org/index.php/Raspberry_Pi)
Replace sdX in the following instructions with the device name for the SD card as it appears on your computer.

## Installation
### Start fdisk to partition the SD card:

		# fdisk /dev/sdX

- At the fdisk prompt, delete old partitions and create a new one:
- Type o. This will clear out any partitions on the drive.
- Type p to list partitions. There should be no partitions left.
- Type n, then p for primary, 1 for the first partition on the drive, press ENTER to accept the default first sector, then type +100M for the last sector.
- Type t, then c to set the first partition to type W95 FAT32 (LBA).
- Type n, then p for primary, 2 for the second partition on the drive, and then press ENTER twice to accept the default first and last sector.
- Write the partition table and exit by typing w.

### Create and mount the FAT filesystem:
	# mkfs.vfat /dev/sdX1
	# mkdir boot
	# mount /dev/sdX1 boot

### Create and mount the ext4 filesystem:
	mkfs.ext4 /dev/sdX2
	mkdir root
	mount /dev/sdX2 root

### Download and extract the root filesystem (`as root, not via sudo`):
	wget http://os.archlinuxarm.org/os/ArchLinuxARM-rpi-2-latest.tar.gz
	bsdtar -xpf ArchLinuxARM-rpi-2-latest.tar.gz -C root
	sync

### Move boot files to the first partition:
	mv root/boot/* boot

### Unmount the two partitions:
	umount boot root

Insert the SD card into the Raspberry Pi, connect ethernet, and apply 5V power.
Use the serial console or SSH to the IP address given to the board by your router.
Login as the default user **pi** with the password **raspberry**.
The default root password is **root**.

# [Linux](https://www.raspberrypi.org/documentation/linux/)
