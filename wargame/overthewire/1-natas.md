[TOC]

# Overview
Natas teaches the basics of **server side web-security**.

Each level of natas consists of its own website located at `http://natasX.natas.labs.overthewire.org`, where X is the level number. There is no SSH login. To access a level, enter the username for that level (e.g. natas0 for level 0) and its password.

Each level has access to the password of the next level. Your job is to somehow obtain that next password and level up. All passwords are also stored in `/etc/natas_webpass/`. E.g. the password for natas5 is stored in the file `/etc/natas_webpass/natas5` and only readable by **natas4** and **natas5**.

Start here:

	Username: natas0
	Password: natas0
	URL:      http://natas0.natas.labs.overthewire.org

View source

Password: `gtVrDuiDfck831PqWsLEZy5gyDz1clto`

# Level 0 - Level 1
	Username: natas1
	URL:      http://natas1.natas.labs.overthewire.org

## Solution
View source (Ctrl + U in Chrome)

## Result
Password: `ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi`

# Level 1 - Level 2
	Username: natas2
	URL:      http://natas2.natas.labs.overthewire.org

## Solution
View source and attention at pixel image. Go to `http://natas2.natas.labs.overthewire.org/files/` we see `users.txt` file have natas3 password.

## Result
Password: `sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14`

# Level 2 - Level 3
	Username: natas3
	URL:      http://natas3.natas.labs.overthewire.org

## Solution
View source, hint is `Not even Google will find it...`. We check `robots.txt` file at url `http://natas3.natas.labs.overthewire.org/robots.txt` and we see a `/s3cr3t/` directory. Go there and get `users.txt` file to get password.

## Result
Password: `Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ`

# Level 3 - Level 4
	Username: natas4
	URL:      http://natas4.natas.labs.overthewire.org

## Solution
