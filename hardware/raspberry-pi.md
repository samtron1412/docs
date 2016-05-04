[TOC]

# Overview
- [Wikipedia](https://en.wikipedia.org/wiki/Raspberry_Pi)

The Raspberry Pi is a series of credit card-sized sing-board computers was developed in the United Kingdom by the Raspberry Pi Foundation with the intent to promote the teaching of basic computer science in schools and developing countries.

# [Set up](https://www.raspberrypi.org/documentation/setup/)
## SD card
The `dd` command is the Linux block copy command. It reads from the `if=` file, in the first case a block of zeros, and writes to the `of=` file, in the first case the file named `test.tmp` in your **HOME** directory (the `~/` means your HOME directory). The `bs=` gives the size of the data, and the `count=` gives the number of times this is repeated. `sync` ensures that the filesystem cache is flushed to have more realistic data. Please run it multiple times, one sample is not scientific enough.

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

# [Linux](https://www.raspberrypi.org/documentation/linux/)
