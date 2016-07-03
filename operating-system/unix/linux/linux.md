[TOC]


`tty` stands for *teletype* - is a terminal used a line printer for ouput and a keyboard for input.
`pdy` stands for *pseudo-terminal* - it's is a software implementation that appears to the attached program like a terminal, but instead of communicating directly with a "real" terminal, it transfers the input and output to another program. For example, when you ssh into a machine and run `ls`, the `ls` command is sending its output to a pseudo-terminal, the other side of which is attached to the SSH daemon.

# Overview
Linux is a **Unix-like** and mostly **POSIX-compliant** computer operating system (OS) assembled under the model of **free and open-source** software development and distribution. Linux kernel is licensed under GPL version 2.

- [Linux Standard Base](http://www.linuxfoundation.org/collaborate/workgroups/lsb/group)
  + [Wikipedia](https://en.wikipedia.org/wiki/Linux_Standard_Base)

## [Filesystem Hierarchy Standard](http://refspecs.linuxfoundation.org/fhs.shtml)
The FHS defines the **directory structure** and **directory contents** in Unix and Unix-like operating systems, maintained by the Linux Foundation.
- `/bin` : All the executable binary programs (file) required during booting, repairing, files required to run into single-user-mode, and other important, basic commands viz., cat, du, df, tar, rpm, wc, history, etc.
- `/boot` : Holds important files during boot-up process, including Linux Kernel.
- `/dev` : Contains device files for all the hardware devices on the machine e.g., cdrom, cpu, etc
- `/etc` : Contains Application’s configuration files, startup, shutdown, start, stop script for every individual program.
- `/home` : Home directory of the users. Every time a new user is created, a directory in the name of user is created within home directory which contains other -directories like Desktop, Downloads, Documents, etc.
- `/lib` : The Lib directory contains kernel modules and shared library images required to boot the system and run commands in root file system.
- `/lost`+found : This Directory is installed during installation of Linux, useful for recovering files which may be broken due to unexpected shut-down.
- `/media` : Temporary mount directory is created for removable devices viz., media/cdrom.
- `/mnt` : Temporary mount directory for mounting file system.
- `/opt` : Optional is abbreviated as opt. Contains third party application software. Viz., Java, etc.
- `/proc` : A virtual and pseudo file-system which contains information about running process with a particular Process-id aka pid.
- `/root` : This is the home directory of root user and should never be confused with ‘/‘
- `/run` : This directory is the only clean solution for early-runtime-dir problem.
- `/sbin` : Contains binary executable programs, required by System Administrator, for Maintenance. Viz., iptables, fdisk, ifconfig, swapon, reboot, etc.
- `/srv` : Service is abbreviated as ‘srv‘. This directory contains server specific and service related files.
- `/sys` : Modern Linux distributions include a /sys directory as a virtual filesystem, which stores and allows modification of the devices connected to the system.
- `/tmp` :System’s Temporary Directory, Accessible by users and root. Stores temporary files for user and system, till next boot.
- `/usr` : Contains executable binaries, documentation, source code, libraries for second level program.
- `/var` : Stands for variable. The contents of this file is expected to grow. This directory contains log, lock, spool, mail and temp files.

## Exploring Important file, their location and their Usability
Linux is a complex system which requires a more complex and efficient way to start, stop, maintain and reboot a system unlike Windows. There is a well defined configuration files, binaries, man pages, info files, etc. for every process in Linux.

- `/boot/vmlinuz` : The Linux Kernel file.
- `/dev/hda` : Device file for the first IDE HDD (Hard Disk Drive)
- `/dev/hdc` : Device file for the IDE Cdrom, commonly
- `/dev/null` : A pseudo device, that don’t exist. Sometime garbage output is redirected to /dev/null, so that it gets lost, forever.
- `/etc/bashrc` : Contains system defaults and aliases used by bash shell.
- `/etc/crontab` : A shell script to run specified commands on a predefined time Interval.
- `/etc/exports` : Information of the file system available on network.
- `/etc/fstab` : Information of Disk Drive and their mount point.
- `/etc/group` : Information of Security Group.
- `/etc/grub`.conf : grub bootloader configuration file.
- `/etc/init`.d : Service startup Script.
- `/etc/lilo`.conf : lilo bootloader configuration file.
- `/etc/hosts` : Information of Ip addresses and corresponding host names.
- `/etc/hosts`.allow : List of hosts allowed to access services on the local machine.
- `/etc/host`.deny : List of hosts denied to access services on the local machine.
- `/etc/inittab` : INIT process and their interaction at various run level.
- `/etc/issue` : Allows to edit the pre-login message.
- `/etc/modules`.conf : Configuration files for system modules.
- `/etc/motd` : motd stands for Message Of The Day, The Message users gets upon login.
- `/etc/mtab` : Currently mounted blocks information.
- `/etc/passwd` : Contains password of system users in a shadow file, a security implementation.
- `/etc/printcap` : Printer Information
- `/etc/profile` : Bash shell defaults
- `/etc/profile`.d : Application script, executed after login.
- `/etc/rc`.d : Information about run level specific script.
- `/etc/rc`.d/init.d : Run Level Initialisation Script.
- `/etc/resolv`.conf : Domain Name Servers (DNS) being used by System.
- `/etc/securetty` : Terminal List, where root login is possible.
- `/etc/skel` : Script that populates new user home directory.
- `/etc/termcap` : An ASCII file that defines the behaviour of Terminal, console and printers.
- `/etc/X11` : Configuration files of X-window System.
- `/usr/bin` : Normal user executable commands.
- `/usr/bin`/X11 : Binaries of X windows System.
- `/usr/include` : Contains include files used by ‘c‘ program.
- `/usr/share` : Shared directories of man files, info files, etc.
- `/usr/lib` : Library files which are required during program compilation.
- `/usr/sbin` : Commands for Super User, for System Administration.
- `/proc/cpuinfo` : CPU Information
- `/proc/filesystems` : File-system Information being used currently.
- `/proc/interrupts` : Information about the current interrupts being utilised currently.
- `/proc/ioports` : Contains all the Input/Output addresses used by devices on the server.
- `/proc/meminfo` : Memory Usages Information.
- `/proc/modules` : Currently using kernel module.
- `/proc/mount` : Mounted File-system Information.
- `/proc/stat` : Detailed Statistics of the current System.
- `/proc/swaps` : Swap File Information.
- `/version :` Linux Version Information.
- `/var/log/lastlog` : log of last boot process.
- `/var/log/messages` : log of messages produced by syslog daemon at boot.
- `/var/log/wtmp` : list login time and duration of each user on the system currently.


## Resources
- [The Linux Documentation Project](http://tldp.org/)
  + [Works](http://tldp.org/docs.html)
  + [HOWTOs](http://tldp.org/HOWTO/HOWTO-INDEX/index.html)
  + [Guides](http://tldp.org/guides.html)
  + [Man pages](http://tldp.org/manpages/man.html)



# Design
![layer](linux/layer.png)

- [Kernel](https://en.wikipedia.org/wiki/Kernel_(operating_system))
- [Linux kernel design patterns](https://lwn.net/Articles/336224/)
- [Anatomy of the Linux kernel](http://www.ibm.com/developerworks/library/l-linux-kernel/)
- [Tour of the Linux kernel source](http://www.tldp.org/LDP/khg/HyperNews/get/tour/tour.html)
- [The art of Linux kernel design](http://www.amazon.com/The-Linux-Kernel-Design-Implementation/dp/1466518030)

# Uses
![stack](linux/Free_and_open-source-software_display_servers_and_UI_toolkits.svg)

# Knowledge
## init process
Dịch vụ đơn lẻ quan trọng nhất trong hệ thống Unix/Linux là init. Nó được khởi động như là tiến trình đầu tiên trong mọi hệ thống Unix/Linux. Đây là tiến trình dùng để khởi động (boot) hệ thống. Nó sẽ kiểm tra và mount filesystems vào hệ thống, khởi động các daemon.
Nó cung cấp các khái niệm như single user mode (chế độ hoạt động như hệ người dùng đơn lẻ), multiuser mode (chế độ đa người dùng). Một số tài liệu còn gọi là run level (cấp độ hoạt động).
Khi hệ thống kết thúc hoạt động (shutdown), init sẽ dọn dẹp (dừng mọi triến trình đang hoạt động, umount filesystems, v.v...).

* init 0: Shutdown hệ thống (halt).
* init 1: Admin single user mode: chỉ có root account có thể login ở mode này.
* init 2: Multi user mode, không có hỗ trợ Network File System (NFS).

* init 3: Multi user, có hỗ trợ NFS: cho phép chia sẻ hệ thống file với các hệ thống khác trong mạng.
* int 4: Không dùng.
* int 5: Multi user, hỗ trợ graphic mode (X11)
* init 6: reboot (tái khởi động) hệ thống. Lưu ý: không được thiết lập mặc định (default) ở chế độ này.
* s (hoặc S): Single user, sử dụng hệ thống như hệ thống cá nhân riêng biệt.
(Tại một thời điểm chỉ có một và chỉ một user có quyền đăng nhập hệ thống).

# Linux Background Job
A task can usually be started and run as a background task by putting a `&` at the end of the command line.

If a task was started and is running in the foreground, it is still possible to move it to the background without cancelling it. To move a task from the foreground to the background perform the following steps:

CTRL-Z (That is, while holding the CTRL key down, tap the 'z' key) This will suspend the current foreground job (task).
Enter the job control command 'bg'
Tap the 'Enter' key
The job is now running in the background.

Useful commands to see which jobs are still running is the 'jobs' or the 'ps ua' commands. If the 'jobs' command is used, a background jobs can be brought to the foreground with the command fg n where n is the job (not the PID) number.


# Logical Volume Management (LVM)
Logical Volume Management (LVM) is a disk management option that every major Linux distribution includes.

## What is LVM?
LVM allows for a layer of abstraction between your operating system and the disks/partitions it uses.

In traditional disk management your operating system looks for what disks are available (/dev/sda, /dev/sdb, etc.) and then looks at what partitions are available on those disks (/dev/sda1, /dev/sda2, etc.).

With LVM, disks and partitions can be abstracted to contain multiple disks and partitions into one device. Your operating systems will never know the difference because LVM will only show the OS the **volume groups (disks)** and **logical volumes (partitions)** that you have set up.

## Common uses
Because volume groups and logical volumes aren't physically tied to a hard drive, it makes it easy to dynamically resize and create new disks and partitions. In addition, LVM can give you features that your file system is not capable of doing. For example, Ext3 does not have support for live snapshots, but if you're using LVM you have the ability to take a snapshot of your logical volumes without unmounting the disk.

- Managing large hard disk farms by allowing disks to be added and replaced without downtime or service disruption, in combination with hot swapping (term used to describe the functions of replacing computer system components without shutting down the system).
- Allows file systems to be easily resized later as needed.
- Performing consistent backups by taking snapshots of the logical volumes.
- Creating single logical volumes of multiple physical volumes or entire hard disks (like to RAID 0), allowing for dynamic volume resizing.

## Anatomy of LVM

```
    hda1   hdc1      (PV:s on partitions or whole disks)
       \   /
        \ /
       diskvg        (VG)
       /  |  \
      /   |   \
  usrlv rootlv varlv (LV:s)
    |      |     |
 ext2  reiserfs  xfs (filesystems)
```

LVM internal organization

![lvm internal](linux/lvm_internal.gif)

- **Volume group (VG)**: is the highest level abstraction used within the LVM. It gathers together a collection of Logical Volumes and Physical Volumes into one administrative unit.
- **Physical Volume (PV):** is typically a hard disk, though it may well just be a device that 'looks' like a hard disk (eg. a software raid device)
- **Logical Volume (LV):** equivalent of a disk partition in a non-LVM system. The LV is visible as a standard block device; as such the LV can contain a file system (eg. /home).
- **Physical Extent (PE):** each physical volume is divided chunks of data, known as physical extents, these extents have the same size as the logical extents for the volume group.
- **Logical Extent (LE):** each logical volume is split into chunks of data, known as logical extents. The extent size is the same for all logical volumes in the volume group.

Mapping logical extents to physical extents. Each PV consists of a number of fixed-size physical extents (PEs); similarly, each LV consists of a number of fixed-size logical extents (LEs). (LEs and PEs are always the same size, the default in LVM 2 is 4 MB.)

![lvm mapping](linux/lvm_mapping.gif)

Linear mapping

![lvm linear mapping](linux/linear_mapping.gif)

Striped mapping

![lvm striped mapping](linux/striped_mapping.gif)


## LVM command line tool
- Physical Volume = pv
  + The physical volume commands are for adding or removing hard drives in volume groups.
- Volume Group = vg
  + The volume group commands are for changing what abstracted set of physical partitions are presented to your operating system in logical volumes.
- Logical Volume = lv
  + Logical volume commands will present the volume groups as partitions so that your operating system can use the designated space.

![lvm-cheatsheet](linux/lvm-cheatsheet.png)

### View current LVM information
`pvdisplay`, `vgdisplay`, `lvdisplay`

# [Loop device](https://en.wikipedia.org/wiki/Loop_device)
- [Ubuntu question](http://askubuntu.com/questions/247625/what-is-the-loopback-device-and-how-do-i-use-it)

# Tips and Tricks
## User's bin
User's `bin` directory is a way to customize how the binary will run. Creating `~/bin` directory and create `shell script files` same name with the binary, set executable attribute for these files, change `$PATH=~/bin:$PATH`.

```chromium
#!/bin/sh -e
# Avoid flash storing cookies and crap.
# (Unfortunatly, some may depend on it, so I can't just link to /dev/null.
# Clear on boot.)
rm -rf ~/.macromedia

# Enable privoxy.
#http_proxy=http://localhost:8118
#https_proxy=$http_proxy
#export http_proxy
#export https_proxy

# While I like C collating at the shell, in some programs I prefer US collating
# for bookmarks..
LC_COLLATE=en_US.UTF-8
PATH=/usr/bin:/bin:/sbin:/usr/sbin:/usr/local/bin
exec chromium --proxy-auto-detect  --disable-remote-fonts "$@"
```

## Optimize Linux
- [cache problem](https://rudd-o.com/linux-and-free-software/tales-from-responsivenessland-why-linux-feels-slow-and-how-to-fix-that)

## Search terminal history commands
`Ctrl+R` and type something you remember about command.

## chmod to only the directories or to only the files
`find . -type d -exec chmod 775 {} \;`: chmod 775 to only the directories

`find . -type f -exec chmod 664 {} \;`: chmod 664 to only the files

## Check runtime of a command
`time <command>`: when finish command it will print runtime of command

## [Check hardware](http://www.binarytides.com/linux-commands-hardware-info/)
## du - display the space size used for a directory
- Show size of current directory: `du -sh` - s: summary, h: human readable

## df - finding the disk free space / disk usage
`df -h`

## [User management](https://wiki.archlinux.org/index.php/Users_and_groups#User_management)
- List users currently logged on the system: `who`
- To add a new user:
  + `# useradd -m -g [initial_group] -G [additional_groups] -s [login_shell] [username]`
  + `# useradd -m -G wheel -s /bin/bash archie`
  + The login shell must be one of those listed in `/etc/sheels `
  + `adduser` is a perl script alternative for `useradd` built in.
- To add a user to other groups:
  + `# usermod -aG additional_groups username`
  + **Warning**: If the `-a` option is omitted in the *usermod* command above, the user is removed from all groups not listed in *additional_groups* (i.e. the user will be member only of those groups listed in *additional_groups*).
- To specify the user's password: `# password username`
- To delete user: `# userdel -r username`
  + `-r` mean user's home directory and mail spool should also be deleted.

## [Group management](https://wiki.archlinux.org/index.php/Users_and_groups#Group_management)
- `/etc/group` is the file that defines the groups on the system.
- Display group membership: `$ groups [username]`
  + If user is omitted, the current user's group names are displayed.
- Detail information: `$ id [user]`
- To list all groups on the system: `$ cat /etc/group`
- Create new group: `# groupadd [group]`
- Modify an existing group with `groupmod`
- To delete existing groups: `# groupdel [group]`

### Group list
#### User groups
| Group  | Affected files                                   | Purpose                                                                                                                                                                                                                                                                                         |
| -      | -                                                | -                                                                                                                                                                                                                                                                                               |
| games  | /var/games                                       | Access to some game software                                                                                                                                                                                                                                                                    |
| rfkill | /dev/rfkill                                      | Right to control wireless devices power state                                                                                                                                                                                                                                                   |
| users  | /dev/ttyS[0-9], /dev/tts/[0-9], /dev/ttyACM[0-9] | Serial and USB devices such as modems, handhelds, RS-232/serial ports.                                                                                                                                                                                                                          |
| wheel  |                                                  | Administration group, commonly used to give access to the **sudo** and **su** utilities (neither uses it by default, configurable in /etc/pam.d/su and /etc/pam.d/su-l). It can also be used to gain full read access to [journal](https://wiki.archlinux.org/index.php/Systemd#Journal) files. |

#### System groups
The following groups are used for system purposes and are not likely to be used by novice Arch users.

| Group           | Affected files                         | Purpose                                                                                                                                                                             |
| -               | -                                      | -                                                                                                                                                                                   |
| bin             | none                                   | Historical                                                                                                                                                                          |
| daemon          |                                        |                                                                                                                                                                                     |
| dbus            |                                        | used internally by dbus                                                                                                                                                             |
| ftp             | /srv/ftp                               | used by FTP servers like Proftpd                                                                                                                                                    |
| fuse            |                                        | Used by fuse to allow used mounts                                                                                                                                                   |
| http            |                                        |                                                                                                                                                                                     |
| kmem            | /dev/port, /dev/mem, /dev/kmem         |                                                                                                                                                                                     |
| mail            | /usr/bin/mail                          |                                                                                                                                                                                     |
| mem             |                                        |                                                                                                                                                                                     |
| nobody          |                                        | Unprivileged group                                                                                                                                                                  |
| polkitd         |                                        | polkit group                                                                                                                                                                        |
| proc            | /proc/pid/                             | A group authorixed to learn processs information otherwise prohibited by hidepid= mount option of the proc filesystem. The group must be explicitly set with the gid= mount option. |
| root            | /*                                     | Complete system administration and control                                                                                                                                          |
| smmsp           |                                        | sendmail group                                                                                                                                                                      |
| systemd-journal | /var/log/journal/*                     | Provides access to the complete systemd logs. Otherwise, only user generated messages are displayed.                                                                                |
| tty             | /dev/tty, /dev/vcc, /dev/vc, /dev/ptmx | Eg. to access /dev/ACMx                                                                                                                                                             |

#### Software groups
These groups are used by certain non-essential software. Sometimes they are used just internally, in these cases you should not add your user into these groups. See the main page for the software for details.

| Group         | Affected files            | Purpose                                                                    |
| -             | -                         | -                                                                          |
| adbusers      | devides nodes under /dev/ | Right to access Android Debugging Bridge                                   |
| avahi         |                           |                                                                            |
| bumblebee     | /run/bumblebee.socket     | Right to launch applications with Bumblebee to utilize NVIDIA Optimus GPUs |
| cdemu         | /dev/vhba_ctl             | Right to use cdemu                                                         |
| ntp           | /var/lib/ntp/*            | NTPd group                                                                 |
| networkmanage |                           |                                                                            |
| vmware        |                           | Right to use VMware software                                               |
| wireshark     |                           | Right to capture packets with Wireshark                                    |





## check distribution of Linux
`dmesg | head -10`

`cat /proc/version`

`cat /etc/issue`

shell script:

```bash
#!/bin/sh
# Detects which OS and if it is Linux then it will detect which Linux Distribution.

OS=`uname -s`
REV=`uname -r`
MACH=`uname -m`

GetVersionFromFile()
{
  VERSION=`cat $1 | tr "\n" ' ' | sed s/.*VERSION.*=\ // `
}

if [ "${OS}" = "SunOS" ] ; then
  OS=Solaris
  ARCH=`uname -p`
  OSSTR="${OS} ${REV}(${ARCH} `uname -v`)"
elif [ "${OS}" = "AIX" ] ; then
  OSSTR="${OS} `oslevel` (`oslevel -r`)"
elif [ "${OS}" = "Linux" ] ; then
  KERNEL=`uname -r`
  if [ -f /etc/redhat-release ] ; then
    DIST='RedHat'
    PSUEDONAME=`cat /etc/redhat-release | sed s/.*\(// | sed s/\)//`
    REV=`cat /etc/redhat-release | sed s/.*release\ // | sed s/\ .*//`
  elif [ -f /etc/SuSE-release ] ; then
    DIST=`cat /etc/SuSE-release | tr "\n" ' '| sed s/VERSION.*//`
    REV=`cat /etc/SuSE-release | tr "\n" ' ' | sed s/.*=\ //`
  elif [ -f /etc/mandrake-release ] ; then
    DIST='Mandrake'
    PSUEDONAME=`cat /etc/mandrake-release | sed s/.*\(// | sed s/\)//`
    REV=`cat /etc/mandrake-release | sed s/.*release\ // | sed s/\ .*//`
  elif [ -f /etc/debian_version ] ; then
    DIST="Debian `cat /etc/debian_version`"
    REV=""

  fi
  if [ -f /etc/UnitedLinux-release ] ; then
    DIST="${DIST}[`cat /etc/UnitedLinux-release | tr "\n" ' ' | sed s/VERSION.*//`]"
  fi

  OSSTR="${OS} ${DIST} ${REV}(${PSUEDONAME} ${KERNEL} ${MACH})"

fi

echo ${OSSTR}
```

## Package manager: ./configure && make install, rpm, dpkg, yum, apt-get
These tools all install software into your system, but are working on different levels.

Installing distributor-provided package (eg. by `yum`) means installing precompiled, almost-ready-to-use binary version of application, whereas installation by source means building application from source, which involves compiling program source code into binary code.

Most notable differences are:

1. Building from source provides more **flexibility** - often applications can be **configured to be built with different features**. For example, you can decide whether you want to build Apache with support for SSL and whether you want to include support for PHP scripting and so on. On the other hand, binary packages are sometimes split into several packages, for example Apache modules (such as mod_php) can be installed as separate modules.

2. Installing from source is usually much more time consuming while installing binary package involves mainly copying files and running installation scripts.

3. Most often, latest versions of applications are provided in source form only - there is time gap before application is packaged and made available in repositories. On the other hand, application installed from repository will be automatically updated by package manager, while applications installed from source will have to be updated manually.

4. Installing binary packages need only package manager, whareas installing from source required working toolchain, mostly `make`, compilers (eg. `gcc`) and development version of third-party libraries.

5. Package manager handles dependencies for you. For example, Apache needs `libapr`, Apache Portable Runtime. When you install Apache using package manager, it installs libapr automatically for you. When you build from source, you have to install libapr first.

**./configure && make install**

Running ./configure && make install builds and installs the libraries or executables directly from the source code.

The make install step basically just copies the final files into your system. Many sources come with a special make uninstall rule to remove them again, but this is not guaranteed and of course only works as long as you have the configured sources around. Also, this does not take care of required dependencies.

Often there is only the source code available for a certain package, so this is the only way to go. Also, ./configure usually accepts lots of options allowing you to tailor your package.

Not being able to find out what software installed which file, and the lack of a reliable way to remove them from the system are major shortcomings of this approach.

**RPM (Redhat Package Manager)**

rpm installs already configured and compiled software in your system and it also comes with a uninstall to get rid of it again. The packages have to be created by somebody. This person already decided on what features to include and how to best integrate the package into your system layout. It also comes with a list of dependencies.

Since rpms are used for many distributions there, you will often want to make sure that this rpm was written for your distribution so that install paths, dependencies and other housekeeping things integrate well.

On Debian systems, the equivalent package format is .deb and the installation and database is handled by the **dpkg** tool.

**Yum**

yum is an additional wrapper around rpm. It keeps its own database of rpm files available for your distribution, generally in online repositories. For the stable versions of most distributions all packages inside that database will play well with each other. This database can be searched (e.g. with yum search some_name).

It will also automatically resolve dependencies for you. Packages (and with some extra help their dependencies) can be easily uninstalled as well.

On Debian systems, the equivalent repository and dependency-resolution tools are provided by Apt (**apt-get** and **aptitude**).

So to sum it up: if you just want some software try yum first. If it is not available there, you can try to find an existing rpm package. If there is none or you have some special requirements, build from source.


## Append to file by command line
### Use redirection symbol : `>>`

`echo <sth> >> abc.txt`

`echo "`date` text here" >> filename`

### Use `tee` command:

`echo "text here `date`"|tee -a filename`

### Use `sed`







## Count file numbers
Pass stdin to `wc -l` command.

`find . -type f|wc -l`

## Find all files follow extension
`find $directory -type f -name "*.ext"`

## 9 dangerous commands
1. Delete Recursively: `rm -rf /`
2. Format Hard Drive: `mkfs.ext4 /dev/hda`
3. Overwrite Hard Drive: `command > /dev/hda`
4. Wipe Hard Drive: `dd if=/dev/zero of=/dev/hda`
5. Implode Hard Drive: `mv / /dev/null`
6. Cause Kernel Panic:
dd if=/dev/random of=/dev/port
echo 1 > /proc/sys/kernel/panic
cat /dev/port
cat /dev/zero > /dev/mem
7. Fork Bomb: `:(){:|:&};:`
8. Execute Remote Script: `wget http://an-untrusted-url -O- | sh`
9. Disable Root Command Rights: `rm -f /usr/bin/sudo;rm -f /bin/su`

## Find process use port
`sudo lsof -i tcp:80`

`sudo netstat -nlp|grep 80`

`netstat -tunap | grep :80` : find what process use 80 port. (-t: tcp, -u: udp, -n: numeric ip instead hostname, -a: all, -p: program/process id)

## Audio muted
`alsamixer` and unmute
