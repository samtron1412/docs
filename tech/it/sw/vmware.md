[TOC]

# Troubleshooting


## After each update **linux header** then reinstall **vmware tools**

**error ubuntu**, maybe access Terminal before login shell: `CTRL + ALT + F1`

### 1. Install VMwareTools

- `sudo apt-get update`
- `sudo apt-get upgrade`
- `sudo apt-get install linux-headers-$(uname -r)`
- VM->Reinstall VMwaretool
- `cp /media/<cdrom>/VMwaretool.tar.gz <new folder>`
- `tar -xf VMwaretool.tar.gz`
- `cd WMwareTool_folder -> sudo ./wmware_install.pl`

### 2. Share folder: should create a seperate share folder to share file with guest to safe

- See in `/mnt/hgfs` to find share folder
- If not see any folder ==> rerun `vmware-config-tools.pl` (terminal -> `$ sudo vmware-config-tools.pl`)
- Để chung mọi share thư mục trong cùng một chỗ
	`sudo mount -t vmhgfs .host:/ <path_to_mount_folder_at_guest_machine>`
	hoặc có thể config từng thư mục share vào các thư mục cụ thể khác nhau
	`sudo mount -t vmhgfs .host:/<name_of_share_folder_at_host_machine_not_guest_machine> <path_to_mount_folder_at_guest_machine>`
	gỡ ra
	`sudo umount -t vmhgfs .host:/`
- edit `/etc/fstab` file, add at the end of file:
	`host:/ <path_to_mount_folder_at_guest_machine> vmhgfs defaults 0 0`

### 3. If above method cannot install vmware tools, you should use **vmware tools patches master** to install.
