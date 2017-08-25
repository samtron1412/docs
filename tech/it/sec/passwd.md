[TOC]

**passwd** is a tool on most Unix and Unix-like operating systems used to change a user's password.

# Password file (/etc/passwd)
The **/etc/passwd** file is a text-based database of *information about users* that may log in to the system or other operating system user identities that own running processes.

The **/etc/passwd** file typically has file system permissions that allow it to be *readable by all users of the system* (world-readable), although it may only be *modified by the superuser* or by using a few special purpose privileged commands.

The **/etc/passwd** file is a text file with one record per line, each describing a user account. Each record consists of *seven fields separated by colons*. The ordering of the records within the file is generally unimportant.

	jsmith:x:1001:1000:Joe Smith,Room 1007,(234)555-8910,(234)555-0044,email:/home/jsmith:/bin/sh

1. **Username**: It is used when user logs in. It should be between 1 and 32 characters in length.
2. **Password**: An `x` character indicates that encrypted password is stored in **/etc/shadow** file.
3. **User ID (UID)**: Each user must be assigned a user ID (UID). UID 0 (zero) is reserved for root and UIDs 1-99 are reserved for other predefined accounts. Further UID 100-999 are reserved by system for administrative and system accounts**/groups**.
4. **Group ID (GID)**: The primary group ID (stored in /etc/group file)
5. **User ID Info**: The comment field. It allow you to add extra information about the users such as user's full name, phone number etc. This field use by finger command.
6. **Home directory**: The absolute path to the directory the user will be in when they log in. If this directory does not exists then users directory becomes /
7. **Command/shell**: The absolute path of a command or shell (/bin/bash). Typically, this is a shell. Please note that it does not have to be a shell.

# Shadow file (/etc/shadow)
**/etc/shadow** is used to increase the security level of passwords by restricting all but highly privileged users' access to hashed password data. Typically, that data is kept in files owned by and accessible only by the **super user**.

	glider:$1$hk7KLlVV$7SbPQwAAp0k5zf1TdrNiS/:16280:0:99999:7:::
	root:!:16280:0:99999:7:::
	postgres:*:16284:0:99999:7:::

1. **User name** : It is your login name
2. **Password**: It your encrypted password. The password should be minimum 6-8 characters long including special characters/digits.
	- "**$id$salt$hashed**", the printable form of a password hash as produced by [crypt](http://en.wikipedia.org/wiki/Crypt_(C)) (C), where "**$id**" is the algorithm used. (On GNU/Linux, "**$1$**" stands for MD5, "**$2a$**" is Blowfish, "**$2y$**" is Blowfish (correct handling of 8-bit chars), "**$5$**" is SHA-256 and "**$6$**" is SHA-512, [crypt(3) manpage](http://man7.org/linux/man-pages/man3/crypt.3.html)).
	- Empty string - No password, the account has no password.
	- "**!**" - the account is *password Locked*, user will be unable to log-in via password authentication but other methods (e.g. ssh key) may be still allowed)
	- `"*LK*"` or `"*"` - the *account is Locked*, user will be unable to log-in via password authentication but other methods (e.g. ssh key) may be still allowed)
	- "**!!**" - the password has never been set.
3. Last password change (**lastchanged**): The date of the last password change, expressed as the number of days since Jan 1, 1970.
	- The value 0 has a special meaning, which is that the user should change her pasword the next time she will log in the system.
	- An empty field means that password aging features are disabled.
4. **Minimum password age**: The minimum number of days required between password changes i.e. the number of days left before the user is allowed to change his/her password. An empty field and value 0 mean that there are no minimum password age.
5. **Maximum password age**: The maximum number of days the password is valid (after that user is forced to change his/her password). An empty field means that there are no maximum password age, no password warning period, and no password inactivity period.
6. **password warning period** : The number of days before password is to expire that user is warned that his/her password must be changed
7. **Inactive** : The number of days after password expires that account is disabled
8. **Expire** : days since Jan 1, 1970 that account is disabled i.e. an absolute date specifying when the login may no longer be used


Get more info about password aging for aspecific user:

	# chage -l <username>

# Use
A *normal user* may only change the password for his/her own account, the *super user* (or root) may change the password for any account. The *administrator* of a group may change the password for the group. passwd *also changes account information*, such as the full name of the user, *user's login shell*, or *password expiry date* and interval.

## Change root's password
must login as root:

	$ su -l
	or
	$ sudo -s
	# passwd

## Set or change your password
	$ passwd

output

	Changing password for vivek
	(current) UNIX password:
	Enter new UNIX password:
	Retype new UNIX password:
	passwd: password updated successfully

## Change password for other user account
must login as root:

	# passwd vivek

output

	Enter new UNIX password:
	Retype new UNIX password:
	passwd: password updated successfully

## Change group password
must login as root

	# passwd -g sales

The current group password is not prompted for. The `-r` option is used with the `-g` option to remove the current password from the named group. This allows group access to *all members*. The `-R` option is used with the `-g` option to restrict the named group for *all users*.

