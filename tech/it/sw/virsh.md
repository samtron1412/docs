[TOC]

# Overview

# Troubleshooting
When your virtual machine running but cannot connect by SSH or cannot start or something like that. Best way to troubleshoot is install **virt-manager** or **vncviewer** on Linux and [UltraVNC](http://www.uvnc.com/downloads.html) on Windows to connect to virtual machine. After that you can troubleshoot problem from this.

Or you can use `virt-rescue` to read image of virtual machine, mount this disk and trobleshoot problems.

- First, you dump information of virtual machine by command: `virsh dumpxml <machine name> > abc.xml`
- Read abc.xml file to determine image place. It some thing like that:  `<source file='/var/kvm/images/motosearch_fazer.img'/>`
- Stop virtual machine: virsh destroy <machine name>
- Use virt-rescue with command: we have two way to use
	+ `virt-rescue -a <path to img file>`
	+ `virt-rescue -d <machine name>`
​- When you go to interactive mode of virt-rescue, use command `lvs` to list all partition of image. It some thing like this:

		LV      VG       Attr      LSize  Pool Origin Data%  Move Log Cpy%Sync Convert
		  lv_root vg_thanh -wi-a---- 27.98g
		  lv_swap vg_thanh -wi-a----  1.53g

- We will see VG is `vg_thanh` and LV have `lv_root`. We will mount `/dev/vg_thanh/lv_root` to `/sysroot` : `mount /dev/vg_thanh/lv_root /sysroot`

After that we chroot to /sysroot: `chroot /sysroot`

Now we can modify content of image. When done you type exit two type to exit virt-rescue.

## Backup virtual machine and restore
- Backup
	+ `virsh save <machine name> <file name>`
	+ `virsh save motosearch_fazer motosearch_fazer_backup`

- Restore
	+ `virsh restore <filename>`
	+ `virsh restore motosearch_fazer_backup`