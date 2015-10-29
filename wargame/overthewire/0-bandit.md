[TOC]

# Overview
The bandit wargame is aimed at absolute beginners.

The level0 is home page for this wargame. And the page `Level X -> Level Y` contain information on how to start level Y from level X.

# Level 0
Connect to the host `bandit.labs.overthewire.org`by
- Username: `bandit0`
- Password: `bandit0`

## Solution
`ssh bandit0@bandit.labs.overthewire.org` and type your password

# Level 0 - Level 1
The password use to log in to bandit1 level store at **readme** file at level0 folder.

## Solution
`cat readme` to show this password and use it to log in to bandit1.

## Result
- Password: `boJ9jbbUNNfktd78OOpsqOltutMc3MY1`

# Level 1 - Level 2
The password for the next level is stored in a file called `-` located in the home directory.

- **Hint**: Google search for 'dashed filename'.
	+ [Special character in bash shell](http://tldp.org/LDP/abs/html/special-chars.html)

## Solution
Prefix filename with the path like this `./-`

## Result
- Password: `CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9`

# Level 2 - Level 3
The password for the next level is stored in a file called spaces in this filename located in the home directory

## Result
- Password: `UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK`

# Level 3 - Level 4
The password for the next level is stored in a hidden file in the **inhere** directory.

## Result
- Password: `pIwrPrtPN36QITSp3EQaw936yaFoFgAB`

# Level 4 - Level 5
The password for the next level is stored in the only **human-readable file** in the inhere directory. Tip: if your terminal is messed up, try the "reset" command.

## Solution
Use find command to find human-readable file.

`find . -type f -exec bash -c 'file -b {} | grep text &>/dev/null' \; -print`

This command will find all file in this directory, each file it will run command `bash -c 'file -b {} | grep text &>/dev/null'` (`\;` is end of command and we need escape it).
- Command `file b {}` have `{}` is a path name holder, it will replace path file to there when it execute.
- `grep text &>/dev/null` it grep text string in output of file command and redirect stderr and stdout to `/dev/null`.
- Last action is `-print`: if true, print whole path file.

## Result
- Password: `koReBOKuIDDepwhWk7jZC0RTdopnAYKh`

# Level 5 - Level 6
The password for the next level is stored in a file somewhere under the **inhere** directory and has all of the following properties:
- human-readable
- 1033 bytes in size
- not executable

## Solution
`find . -type f -exec bash -c 'file -b {} | grep text &>/dev/null' \; -size 1033c ! -executable -print`

## Result
-Password: `DXjZPULLxYr17uwoI01bNLQbtFemEgo7`

# Level 6 - Level 7
The password for the next level is stored **somewhere on the server** and has all of the following properties:
- owned by user **bandit7**
- owned by group **bandit6**
- 33 bytes in size

## Solution
`find / -type f -group bandit6 -user bandit7 -size 33c 2>/dev/null`

- `2>/dev/null`: use to hide the stderr

## Result
- Password: `HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs`

# Level 7 - Level 8
The password for the next level is stored in the file **data.txt** next to the word **millionth**

## Solution
`grep millionth data.txt`

## Result
- Password: `cvX2JJa4CFALtqS87jk27qwqGhBM9plV`

# Level 8 - Level 9
The password for the next level is stored in the file **data.txt** and is the only line of text that occurs only once

## Solution
`sort data.txt | uniq -cu`

## Result
- Password: `UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR`

# Level 9 - Level 10
The password for the next level is stored in the file **data.txt** in one of the few **human-readable** strings, beginning with several **'='** characters.

## Solution
`grep -o --text '==[[:print:]]*' data.txt`

## Result
- Password: `truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk`

# Level 10 - Level 11
The password for the next level is stored in the file data.txt, which contains base64 encoded data

## Solution
`cat data.txt | base64 --decode`

## Result
- Password: `IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR`

# Level 11 - Level 12
The password for the next level is stored in the file **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

## Solution
	$ alpha=abcdefghijklmnopqrstuvwxyz
	$ beta=ABCDEFGHIJKLMNOPQRSTUVWXYZ
	$ rot=13
	$ sed "y/${alpha}${beta}/${alpha:$rot}${alpha::$rot}${beta:$rot}${beta::$rot}/" <<< 'Gur cnffjbeq vf 5Gr8L4qetPEsPk8htqjhRK8XSP6x2RHh'

## Result
- Password: `5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu`

# Level 12 - Level 13
The password for the next level is stored in the file **data.txt**, which is a *hexdump* of a file that has been **repeatedly compressed**. For this level it may be useful to create a directory under `/tmp` in which you can work using `mkdir`. For example: `mkdir /tmp/myname123`. Then copy the data file using cp, and rename it using `mv` (read the manpages!)

## Solution
	xxd -r data.txt foobar.bin
	zcat foobar.bin | bzcat | zcat | tar xO | tar xO | bzcat | tar xO | zcat

## Result
- Password: `8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL`

# Level 13 - Level 14
The password for the next level is stored in **/etc/bandit_pass/bandit14** and can only be read by user **bandit14**. For this level, you don't get the next password, but you get a **private SSH key** that can be used to log into the next level. **Note: localhost** is a hostname that refers to the machine you are working on.

## Solution
Log in to bandit13 user and run this command:

`ssh -i /home/bandit13/sshkey.private bandit14@localhost`

Key-based authentication uses two keys, one "public" key that anyone is allowed to see, and another "private" key that only the owner is allowed to see. To securely communicate using key-based authentication, one needs to create a key pair, securely store the **private key on the computer one wants to log in from**, and store the **public key on the computer one wants to log in to**.

## Result
- Password: `4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e`
- Private SSH key

```
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAxkkOE83W2cOT7IWhFc9aPaaQmQDdgzuXCv+ppZHa++buSkN+
gg0tcr7Fw8NLGa5+Uzec2rEg0WmeevB13AIoYp0MZyETq46t+jk9puNwZwIt9XgB
ZufGtZEwWbFWw/vVLNwOXBe4UWStGRWzgPpEeSv5Tb1VjLZIBdGphTIK22Amz6Zb
ThMsiMnyJafEwJ/T8PQO3myS91vUHEuoOMAzoUID4kN0MEZ3+XahyK0HJVq68KsV
ObefXG1vvA3GAJ29kxJaqvRfgYnqZryWN7w3CHjNU4c/2Jkp+n8L0SnxaNA+WYA7
jiPyTF0is8uzMlYQ4l1Lzh/8/MpvhCQF8r22dwIDAQABAoIBAQC6dWBjhyEOzjeA
J3j/RWmap9M5zfJ/wb2bfidNpwbB8rsJ4sZIDZQ7XuIh4LfygoAQSS+bBw3RXvzE
pvJt3SmU8hIDuLsCjL1VnBY5pY7Bju8g8aR/3FyjyNAqx/TLfzlLYfOu7i9Jet67
xAh0tONG/u8FB5I3LAI2Vp6OviwvdWeC4nOxCthldpuPKNLA8rmMMVRTKQ+7T2VS
nXmwYckKUcUgzoVSpiNZaS0zUDypdpy2+tRH3MQa5kqN1YKjvF8RC47woOYCktsD
o3FFpGNFec9Taa3Msy+DfQQhHKZFKIL3bJDONtmrVvtYK40/yeU4aZ/HA2DQzwhe
ol1AfiEhAoGBAOnVjosBkm7sblK+n4IEwPxs8sOmhPnTDUy5WGrpSCrXOmsVIBUf
laL3ZGLx3xCIwtCnEucB9DvN2HZkupc/h6hTKUYLqXuyLD8njTrbRhLgbC9QrKrS
M1F2fSTxVqPtZDlDMwjNR04xHA/fKh8bXXyTMqOHNJTHHNhbh3McdURjAoGBANkU
1hqfnw7+aXncJ9bjysr1ZWbqOE5Nd8AFgfwaKuGTTVX2NsUQnCMWdOp+wFak40JH
PKWkJNdBG+ex0H9JNQsTK3X5PBMAS8AfX0GrKeuwKWA6erytVTqjOfLYcdp5+z9s
8DtVCxDuVsM+i4X8UqIGOlvGbtKEVokHPFXP1q/dAoGAcHg5YX7WEehCgCYTzpO+
xysX8ScM2qS6xuZ3MqUWAxUWkh7NGZvhe0sGy9iOdANzwKw7mUUFViaCMR/t54W1
GC83sOs3D7n5Mj8x3NdO8xFit7dT9a245TvaoYQ7KgmqpSg/ScKCw4c3eiLava+J
3btnJeSIU+8ZXq9XjPRpKwUCgYA7z6LiOQKxNeXH3qHXcnHok855maUj5fJNpPbY
iDkyZ8ySF8GlcFsky8Yw6fWCqfG3zDrohJ5l9JmEsBh7SadkwsZhvecQcS9t4vby
9/8X4jS0P8ibfcKS4nBP+dT81kkkg5Z5MohXBORA7VWx+ACohcDEkprsQ+w32xeD
qT1EvQKBgQDKm8ws2ByvSUVs9GjTilCajFqLJ0eVYzRPaY6f++Gv/UVfAPV4c+S0
kAWpXbv5tbkkzbS0eaLPTKgLzavXtQoTtKwrjpolHKIHUz6Wu+n4abfAIRFubOdN
/+aLoRQ0yBDRbdXMsZN/jvY44eM+xRLdRVyMmdPtP8belRi2E2aEzA==
-----END RSA PRIVATE KEY-----
```

# Level 14 - Level 15
The password for the next level can be retrieved by submitting the password of the current level to **port 30000 on localhost**.

## Solution
`echo 4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e | nc localhost 30000`

## Result
- Password: `BfMYroe26WYalil77FoDi9qh59eK5xNr`

# Level 15 - Level 16
The password for the next level can be retrieved by submitting the password of the current level to **port 30001 on localhost using SSL encryption**.

Helpful note: Getting "HEARTBEATING" and "Read R BLOCK"? Use **-quiet** and read the "CONNECTED COMMANDS" section in the manpage. Next to 'R' and 'Q', the 'B' command also works in this version of that command...

## Solution
`echo BfMYroe26WYalil77FoDi9qh59eK5xNr | openssl s_client -connect localhost:30001 -quiet`

## Result
- Password: `cluFn7wTiGryunymYOu4RcffSxQluehd`

# Level 16 - Level 17
The password for the next level can be retrieved by submitting the password of the current level to **a port on localhost in the range 31000 to 32000**. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don't. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

## Solution
Run this command `nmap -sT localhost -p31000-32000` we get five open port (don't use any option for nmap because you don't have root permission. Try each port with below command.

`echo cluFn7wTiGryunymYOu4RcffSxQluehd | openssl s_client -connect localhost:31790 -quiet`

## Result
- Private key:

```
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----
```

# Level 17 - Level 18
There are 2 files in the home directory: **passwords.old** and **passwords.new**. The password for the next level is in **passwords.new** and is the only line that has been changed between **passwords.old** and **passwords.new**

**NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19**

## Solution
`diff passwords.old passwords.new`

## Result
- Password: `kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd`

# Level 18 - Level 19
The password for the next level is stored in a file **readme** in the home directory. Unfortunately, someone has modified **.bashrc** to log you out when you log in with SSH.

## Solution
`ssh -tv user@host cat readme`

## Result
- Password: `IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x`

# Level 19 - Level 20
To gain access to the next level, you should use the **setuid** binary in the home directory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (**/etc/bandit_pass**), after you have used to **setuid** binary.

## Solution
Use executable file `bandit20-do` to run command with bandit20's permissions. So we will use this file to cat password of next level at `/etc/bandit_pass/bandit20`

`./bandit20-do cat /etc/bandit_pass/bandit20`

## Result
- Password: `GbKksEFF4yrVs6il55v6gwY5aVje5f0j`

# Level 20 - Level 21
There is a **setuid** binary in the home directory that does the following: it makes a connection to localhost on the port you specify as a command line argument. It then reads a line of text from the connection and compares it to the password in the previous level (**bandit20**). If the password is correct, it will transmit the password for the next level (**bandit21**).

**NOTE**: To beat this level, you need to login twice: once to run the setuid command, and once to start a network daemon to which the setuid will connect.

**NOTE 2**: Try connecting to your own network daemon to see if it works as you think

## Solution
- Because the binary is makes a connection to localhost on the specific port, so we log in to bandit20 and use `nc` to listen on a specific port: `nc -l 4444`
- After that we log in another time to bandit20 to run the binary: `./suconnect 4444`
- Finally we sending previous password from `nc` listen terminal to `suconnect` terminal

## Result
- Password: `gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr`

# Level 21 - Level 22
A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in `/etc/cron.d/` for the configuration and see what command is being executed.

## Solution
- Look in `/etc/cron.d/` and cat the file `cronjob_bandit22` and we see it will run this file `/usr/bin/cronjob_bandit22.sh`.
- Run command `cat /usr/bin/cronjob_bandit22.sh` we get this

		#!/bin/bash
		chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
		cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv

- Cat the file `/tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv`


## Result
- Password: `Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI`

# Level 22 - Level 23
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in `/etc/cron.d/` for the configuration and see what command is being executed.

**NOTE**: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

## Solution
`/etc/cron.d/cronjob_bandit23`

	* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null

`/usr/bin/cronjob_bandit23.sh`

	#!/bin/bash

	myname=$(whoami)
	mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

	echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

	cat /etc/bandit_pass/$myname > /tmp/$mytarget

When we run `cronjob_bandit23.sh` it will get `myname=bandit22`, so we will run these command to get password for bandit23

	myname=bandit23
	mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)
	cat /tmp/$mytarget

## Result
- Password: `jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n`

# Level 23 - Level 24
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in `/etc/cron.d/` for the configuration and see what command is being executed.

**NOTE**: This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!

**NOTE 2**: Keep in mind that your shell script is removed once executed, so you may want to keep a copy around ...

## Solution
`/usr/bin/cronjob_bandit24.sh`

	#!/bin/bash

	myname=$(whoami)

	cd /var/spool/$myname
	echo "Executing and deleting all scripts in /var/spool/$myname:"
	for i in * .*;
	do
	    if [ "$i" != "." -a "$i" != ".." ];
	    then
	        echo "Handling $i"
	        timeout -s 9 60 "./$i"
	        rm -f "./$i"
	    fi
	done

We create a new shell script and put it on `/var/spool/bandit24` directory. This shell script will be cat the password of bandit24 and write to file at `/tmp/` directory.

	#!/bin/bash
	cat /etc/bandit_pass/bandit24 > /tmp/glider-password.txt

## Result
- Password: `UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ`

# Level 24 - Level 25
A daemon is listening on port **30002** and will give you the password for bandit25 if given the password for bandit24 and **a secret numeric 4-digit pincode**. There is no way to retrieve the pincode except by *going through all of the 10000 combinations, called brute-forcing*.

## Solution

	#!/bin/bash

	for i in {1..10000}; do
		echo "UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ $i" >> input
	done

	cat input | nc localhost 30002 >> result
	sort result | uniq -u

## Result
- Password: `uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG`

# Level 25 - Level 26
Logging in to bandit26 from bandit25 should be fairly easy. The shell for user bandit26 is not **/bin/bash**, but something else. Find out what it is, how it works and how to break out of it.

## Solution
View `/etc/passwd` we see the shell of bandit26 is `/usr/bin/showtext`

	#!/bin/sh

	more ~/text.txt
	exit 0

`more`



## Result
- Password: `5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z`

Congratulations on solving the last level of this game!

At this moment, there are no more levels to play in this game. However, we are constantly working
on new levels and will most likely expand this game with more levels soon.
Keep an eye out for an announcement on our usual communication channels!
In the meantime, you could play some of our other wargames.

If you have an idea for an awesome new level, please let us know!
