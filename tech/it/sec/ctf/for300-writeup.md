First, 


# Install zfs in 64 bit
$ git clone https://github.com/zfsonlinux/spl.git
$ git clone https://github.com/zfsonlinux/zfs.git

$ apt-get install build-essential gawk alien fakeroot linux-headers-$(uname -r) zlib1g-dev uuid-dev libblkid-dev libselinux-dev parted lsscsi wget autogen automake libtool

$ cd spl
$ ./autogen.sh
$ ./configure
$ make deb-utils deb-kmod
$ ls *.deb|xargs dpkg -i

$ cd ../zfs
$ ./autogen.sh
$ ./configure
$ make deb-utils deb-kmod
$ ls *.deb|xargs dpkg -i

$ reboot

# zfs
zpool import -d . attt


===

Get file [here](https://mega.co.nz/#!m0lCDboS!DklgsTq_NpRlPViTpAyV8mwb9E-p-cesQoYp04T47iU"]https://mega.co.nz/#!m0lCDboS!DklgsTq_NpRlPViTpAyV8mwb9E-p-cesQoYp04T47iU)

Đầu tiên, xác định được kiểu file là 7-zip, giải nén ta được một file pcapng dung lượng khoảng hơn 200MB.

Tiếp tục dùng WireShark để mở file pcapng này lên, hơi bị lag một tí khi mở trên máy mình :p

Dùng HTTP export object thì ta được 4 file, trong đó cần để ý 3 file data d1, d2, d3. Thực tế thì tới đoạn này cùng ngồi bí lù chả biết nó là dạng gì mà làm tiếp :rolleyes: cho đến khi ban tổ chức hint là [B]zfs[/B]. Sau này (sau khi thi xong :o) xem lại thì thấy nếu xem head của file d1 thì có những keyword có thể dẫn đến file system zfs như [B]pool, vdev,…[/B]

Sau một hồi search zfs và hì hục cài đặt cho trên con máy ảo ubuntu theo link: [URL="http://zfsonlinux.org/generic-deb.html"]http://zfsonlinux.org/generic-deb.html[/URL]; .......phù......cuối cùng cũng cài đặt hoàn thành. Tóm tắt các bước cài đặt như sau:

[QUOTE]
$ apt-get install build-essential gawk alien fakeroot linux-headers-$(uname -r) zlib1g-dev uuid-dev libblkid-dev libselinux-dev parted lsscsi wget autogen automake libtool

$ git clone [url]https://github.com/zfsonlinux/spl.git[/url]
$ git clone [url]https://github.com/zfsonlinux/zfs.git[/url]

$ apt-get install build-essential gawk alien fakeroot linux-headers-$(uname -r) zlib1g-dev uuid-dev libblkid-dev libselinux-dev parted lsscsi wget autogen automake libtool

$ cd spl
$ ./autogen.sh
$ ./configure
$ make deb-utils deb-kmod
$ ls *.deb|xargs dpkg -i

$ cd ../zfs
$ ./autogen.sh
$ ./configure
$ make deb-utils deb-kmod
$ ls *.deb|xargs dpkg -i

$ reboot
[/QUOTE]

Bước đầu có thể xác định 3 file d1, d2, d3 là một storage pool. Import nó vào xem sao: [QUOTE]zpool import -d . attt[/QUOTE]

List xem nó có cái gì: [B]zpool list[/B]

Lục lọi trong thư mục /attt/home/ thấy ngay file flag, mừng như mở cờ trong bụng tưởng là ăn ngon. Ai ngờ cat [B]/attt/home/flag|gunzip[/B] thì được [B]SVATTT_FAKE_FLAG_01000[/B] vỡ mộng :mad:

Ok vậy là flag đã được dấu trong cả đống snapshot: [QUOTE]snapshot zfs list -t snapshot[/QUOTE] Ngồi viết cái bash script để rollback lại từng snapshot và tìm flag thực sự.

[QUOTE]#!/bin/bash
bla bla bla ...[/QUOTE]

==
Boom!!!

Flag: [B]SVATTT_<3_ZFS_IS_FUN!![/B]

===

Get file [here](https://mega.co.nz/#!m0lCDboS!DklgsTq_NpRlPViTpAyV8mwb9E-p-cesQoYp04T47iU"]https://mega.co.nz/#!m0lCDboS!DklgsTq_NpRlPViTpAyV8mwb9E-p-cesQoYp04T47iU)

First, we detect file type is **7-zip**, extract this file we get a `pcapng` file with size about 200 MB.

Use **WireShark** to open pcapng file, a little slow when load this file :3

With **HTTP export object** we have 4 files, you look at 3 data files **d1, d2, d3**. At this time, I really don't know what else to do next :rolleyes: until the organizers hint **zfs**. After contest (:o) when review this challenge, I see if view head of **d1** data file then have keywords maybe lead to file system **zfs** such as **pool, vdev, ...**

After a moment search zfs and install it on Ubuntu virtual machine follow this [link](http://zfsonlinux.org/generic-deb.html"]http://zfsonlinux.org/generic-deb.html); I can summary process installation like this:

```bash
$ apt-get install build-essential gawk alien fakeroot linux-headers-$(uname -r) zlib1g-dev uuid-dev libblkid-dev libselinux-dev parted lsscsi wget autogen automake libtool

$ git clone [url]https://github.com/zfsonlinux/spl.git[/url]
$ git clone [url]https://github.com/zfsonlinux/zfs.git[/url]

$ apt-get install build-essential gawk alien fakeroot linux-headers-$(uname -r) zlib1g-dev uuid-dev libblkid-dev libselinux-dev parted lsscsi wget autogen automake libtool

$ cd spl
$ ./autogen.sh
$ ./configure
$ make deb-utils deb-kmod
$ ls *.deb|xargs dpkg -i

$ cd ../zfs
$ ./autogen.sh
$ ./configure
$ make deb-utils deb-kmod
$ ls *.deb|xargs dpkg -i

$ reboot
```

First step we know 3 data files **d1, d2, d3** is a storage pool. Import this pool by command: `zpool import -d . attt`

List content of this pool: `zpool list`

Find in `/attt/home` folder we can see flag file, but when we run `cat /attt/home/flag|gunzip` then it show `SVATT_FAKE_FLAG_01000`

Ok so, flag is hide in stack of **snapshot**: `snapshot zfs list -t snapshot`. Write a bash script to rollback each snapshot to find real flag.

```bash
#!/bin/bash
bla bla bla ...
```

==
Boom!!!

**Flag**: `SVATTT_<3_ZFS_IS_FUN!!`
