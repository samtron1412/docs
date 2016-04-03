[TOC]

# bash
GNU Bourne-Again SHell

`bash -c <string>` : execute command from string.

# echo - prints arguments separated by a space and terminated by a newline
>You should avoid it.

Two main branches of Unix: AT&T's System V and BSD. One of their differences was the behavior of `echo`. Built into all modern shells, `echo` prints its arguments with a single space between them to the standard output stream, followed by a newline:

	$ echo The   quick  brown   fox
	The quick brown fox

The default newline can be suppressed in one of two ways, depending on the shell:

	$ echo -n No newline
	No newline$ echo "No newline\c"
	No newline$



## Check exit status code

	run command
	echo $?



# man - display information about a command
# cd - change directories
# ls - list the contents of a directory
`ls -d */` : list all subdirectories in the current directory

ll – list at long mode

List files sorted by the time they were last modified:
`ls -lt`

List files human readable
`ls -lh`

List files order by size
`ls -lS` and with human readable `ls -lhS`

# pwd - show the path to the current directory
# cp - copy a file to another file or directory

# scp – secure copy , remote file copy

# mv - move or rename a file
# rm - remove a file
# mkdir - create a directory
# chmod - change the permissions on a file
# less - view the contents of a file
# nano - file editor

# netstat
`netstat -tunap | grep :80` : find what process use 80 port. (-t: tcp, -u: udp, -n: numeric ip instead hostname, -a: all, -p: program/process id)

# grep - search for a pattern in a file or files

# date - display the current date and time
# passwd - Change your login password
# du - display the space size used for a directory
- Show size of current directory: `du -sh` - s: summary, h: human readable

# df - finding the disk free space / disk usage
`df -h`

# links - text based web browser - hay
# w - See who else is logged in
    - tty – native terminal of host
    - pty/pts – remote terminal, ie# Ssh, xterm…

# grep
Recursively grep through directory for string in file: `grep -r -i "phrase" directory/`


# [sed](http://www.thegeekstuff.com/2009/11/unix-sed-tutorial-append-insert-replace-and-count-file-lines/)
**sed** is a stream editor. A stream editor is used to perform basic text transformations on an input stream (a file or input from a pipeline). While in some ways similar to an editor which permits scripted edits (such as ed), sed works by making only one pass over the input(s), and is consequently more efficient. But it is sed's ability to filter text in a pipeline which particularly distinguishes it from other types of editors.

Append a line at the end of the file: `sed '$ a\sentence' filepath`


# find
Lệnh trên tìm tất cả các file có tên là “music” trong toàn bộ hệ thống
`find / –name music`

Tìm các file trong thư mục /home có owned là joe
`find /home -user joe`

Tìm các file trong thư mục /usr kết có tên kết thúc là “stat”
`find /usr -name *stat`

Tìm các file trong thư mục /var/spool đã được hiệu chỉnh trong vòng >60 ngày trước
`find /var/spool –mtime +60`

Tìm các file đã được hiệu chỉnh trong vòng 24h trở lại đây trong thư mục home
`find $HOME –mtime 0`

Tìm các file có tên “core” trong thư mục /tmp và xóa chúng đi
`find /tmp –name core –type f –print | xargs /bin/rm –f`

Tìm các file được chmod theo thông số nào đó
`find # –perm –664`

Tìm các file được cho phép đọc bởi tất cả mọi người nhưng không cho phép thực thi
`find # –perm –444 ! –perm /111`

# unordered
1.  clear: làm sạch cửa sổ dòng lệnh
2.  ls tenthumuc:      Liệt kê nội dung bên trong một thư mục
3.  cat tentaptin:      Hiển thị nội dung của một tập tin lên cửa sổ dòng lệnh
4.  rm tentaptin:      Xóa một tập tin
5.  cp taptinnguon taptindich: Sao chép một tập tin
6.  passwd: Đổi mật khẩu
7.  motd:      Thông điệp của ngày
8.  finger tentruycap:      Chương trình tìm kiếm thông tin người dùng
9.  startx: Khởi động X Window System server
10. less tentaptin hoặcr more tentaptin: Hiển thị nội dung một tập tin trong cửa sổ dòng lệnh một trang mỗi lần
11. info:      Hiển thị thông tin và tài liệu trên shell, các tiện ích và chương trình.
12. lpr tentaptin:      Gửi tập tin tới máy tin
13. grep chuoi tentaptin: tìm kiếm chuỗi trong tập tin
14. head tentaptin:      Hiển thị 10 dòng đầu tiên của tập tin
15. tail tentaptin:      Hiển thị 10 dòng cuối cùng của tập tin
16. mv tentaptincu      tentaptinmoi: Di chuyển hoặc đổi tên tập tin
17. file tentaptin:      Hiển thị thông tin về nội dung của tập tin
19. date:      Hiển thị ngày và giờ hiện tại
20. cal:      Hiển thị lịch
21. gzip tentaptin:      Nén một tập tin
22. gunzip tentaptin:      Giải nén một tập tin
23. which lenh:      Hiển thị đường dẫn tới lệnh
24. whereis lenh:      Hiển thị đường tới nơi chứa lệnh
25. who: Hiển thị các người dùng đã đang nhập
26. finger tentruycap@maychu:      Thu thập thông tin chi tiết về người dùng hiện đang dùng hệ thống
27. w: Hiễn thị người dùng đã đăng nhập với các tiến trình sử dụng
28. mesg y/n: Đặt tùy chọn để các người dùng khác viết thông điệp cho bạn
29. write nguoidung:      Gửi tin nhắn cho người dùng khác
30. talk nguoidung:      Cho phép 2 người chat với nhau
31. chmod quyen      tentaptin: Thay đổi quyền truy cập tập tin
32. mkdir tenthumuc:      Tạo một thư mục
33. rmdir tenthumuc:      Xóa một thư mục rỗng
34. ln existingfile      new-link: Tạo một đường dẫn tới một tập tin (liên kết cứng)
35. df: Hiển thị tất cả các mount của hệ thống
36. top:      Hiển thị danh sách các tiến trình đang chạy
37. tty:      Hiển thị tên của cửa sổ dòng lệnh mà trên đó lệnh được dùng
38. kill PID hoặc số %job: Ngừng một tiến trình bằng số PID (Process      Identification Number) hoặc số công việc
39. jobs:      Hiển thị một danh sách các công việc hiện tại
40. netstat:      Hiển thị các kết nối mạng
41. traceroute maychu:      In gói định tuyến tới máy chủ
42. nslookup:      Truy vấn máy chủ tên miền
43. hostname:      Hiển thị tên định danh của hệ thống
44. rlogin maychu:      Tiện ích để kết nối với một hệ thống ở xa
45. telnet maychu:      Tiện ích để kết nối tới một hệ thống ở xa (tương tự như rlogin nhưng tương tác tốt hơn)
46. rcp taptin      maytuxa: Được dùng để sao chép từ một máy tính ở xa
47. ftp: Tiện ích để truyền tập tin giữa các hệ thống trên một mạng
48. rsh lenh:      Tiện ích để chạy một lệnh trên một hệ thống ở xa mà không cần đăng nhập
49. ping maychu:      Tiện ích để kiểm tra kết nối tới một hệ thống ở xa
50. lcd duongdanthumuc:      Thay đổi thư mục máy cục bộ khi đã đăng nhập ở trên máy ở xa

# [useradd](http://www.tecmint.com/add-users-in-linux/)
## synopsis
`useradd [options] <username>`
`useradd -D <username>`
`useradd -D [options] <username>`

## description
create a new user or update default new user information

When invoked without the **-D** option, the useradd command creates a new user account using the values specified on the command plus the default values. And with **-D** option, values only on the command.

## options
`-d, --home-dir <HOME_DIR>`

    The new user will be created using HOME_DIR as the value for the user's login directory.

`-g, --gid <GROUP>`

    The group name or number of the user's initial login group. The group name must exist. A group number must refer to an already existing group.

# userdel
## synopsis
`userdel [options] <username>`

## description
delete a user account and related files

## options
`-f, --force`

    Remove user though user still logged in.

`-r, --remove`

    Remove home directory of user


# groupadd
Create a new group

## synopsis
`groupadd [options] group`

# groupdel
delete a group

`groupdel [options] <GROUP>`


# change color of shell
- https://wiki.archlinux.org/index.php/Color_Bash_Prompt
- http://askubuntu.com/questions/466198/how-do-i-change-the-color-for-directories-with-ls-in-the-console





# tail
real time log file view: `tail -f ca <file_path>`

# chkconfig
## Linux Runlevels explained

| Run level | Mode          | Action                   |
| -   | -             | -                        |
| 0   | Halt          | Shuts down system                    |
| 1   | Single-User Mode    | Does not configure network interfaces, start daemons, or allow non-root logins |
| 2   | Multi-User Mode     | Does not configure network intrefaces or start daemons.      |
| 3   | Multi-User Mode with Networking | Starts the system normally.                |
| 4   | Undefined           | Not used/User-definable              |
| 5   | X11           | as runlevel 3 + display manager            |
| 6   | Reboot        | Reboots the system                   |

The `chkconfig` tool is used in Red Hat based systems (like CentOS) to control what services are started at which runlevels. Running the command `chkconfig –list` will display a list of services whether they are enabled or disabled for each runlevel.

`chkconfig --level 234 tomcat on`


# unset
Remove a variable environment: `unset PATH`
`unset HOME`

# mount
- Listing currently mounted file systems: `mount`
- Listing currently mounted file system type specific: `mount -t <type>`
	+ `mount -t ext3`
- Mounting a file system: `mount [option...] <device> <directory>`
	+ `mount /dev/sdc1 /media/flashdisk`
	+ `mount -t vfat /dev/sdc1 /media/flashdisk`
- Unmounting a file system: `umount <directory/device>`
	+ Check whether file system is in use by any process: `fuser -m <directory>`
	+ Unmouting: `umount /media/cdrom`

# type - displays information about a command

# source a.k.a `.` (dot) - executes a script in the current shell environment

# printf - prints the arguments as specified by a format string
`$ printf '%s\n' "Hello World!"`

# chattr - change file attributes on a Linux file system
