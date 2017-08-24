[TOC]

# Overview
Forencis 300, thử thách trong cuộc thi chung kết sinh viên với an toàn thông tin 2014 (20141122). File được cung cấp qua link: https://mega.co.nz/#!m0lCDboS!DklgsTq_NpRlPViTpAyV8mwb9E-p-cesQoYp04T47iU

# Solve
Đầu tiên, ta dùng lệnh `file` để xác định được kiểu file là 7-zip, giải nén ta được một file `pcapng` dung lượng khoảng hơn 200MB.

Tiếp tục dùng **WireShark** để mở file pcapng này lên, hơi bị lag một tí khi mở trên máy mình :v

Dùng HTTP export object thì ta được 4 file, trong đó cần để ý 3 file data d1, d2, d3. Thực tế thì tới đoạn này cùng ngồi bí lù chả biết nó là dạng gì mà làm tiếp :v cho đến khi ban tổ chức hint là zfs. Sau này xem lại thì thấy nếu xem head của file d1 thì có những keyword có thể dẫn đến file system zfs như pool, vdev,...

Sau một hồi search zfs và hì hục cài đặt cho trên con máy ảo ubuntu theo link: **http://zfsonlinux.org/generic-deb.html**; .......phù......cuối cùng cũng cài đặt hoàn thành. Tóm tắt các bước cài đặt như sau:

@todo install zfs

Bước đầu có thể xác định 3 file d1, d2, d3 là một storage pool. Theo manual của zfs thì import nó vào xem sao: `zpool import -d . attt`

List xem nó có cái gì: `zpool list`

Lục lọi trong thư mục `/attt/home/` thấy ngay file flag, mừng như mở cờ trong bụng tưởng là ăn ngon. Ai ngờ `cat /attt/home/flag|gunzip` thì được `SVATTT_FAKE_FLAG_01000` vỡ mộng :(

Ok vậy là flag đã được dấu trong cả đống snapshot `zfs list -t snapshot`. Ngồi viết cái bash script để rollback lại từng snapshot và tìm flag thực sự.

	#!/bin/bash
	for i in `zfs list -t snapshot -o name|tac`; do
	  if [ "$i" != "NAME" ]; then
	    #echo $i
	    zfs rollback -r $i
	    fake=`cat /attt/home/flag|gunzip|cut -d'_' -f 2`
	    #echo $fake
	    if [ $fake != "FAKE" ]; then
	      echo `cat /attt/home/flag|gunzip`
	      echo $i
	      exit 0
	    else
	      echo "wrong: $i"
	    fi
	  fi
	done

Boom!!!

Flag: `SVATTT_<3_ZFS_IS_FUN!!`