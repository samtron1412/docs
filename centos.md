[TOC]

# Overview
## Resources
- All [archive](http://vault.centos.org/): find iso file use to install CentOS in folder `version/isos/arch/`
- [RHEL Life Cycle](https://access.redhat.com/support/policy/updates/errata#Life_Cycle_Dates)

# Centos 7
- [Change logs](http://www.interworx.com/community/centos-7-released-heres-whats-new/)
    + Support for Linux Containers: Docker
    + XFS as the default Filesystem
    + Switch to Systemd
    + Only have x86_64 version

## Initial Settings
### Add an user
    useradd <username>
    passwd <username>

Add user to a group: `gpasswd -a <user> <group>`

By default, on CentOS 7, users who belong to the "**wheel**" group are allowed to use the sudo command.


### Firewall
Decide which ports and services to open:
- SSH: port 22
- Web: port 80, 443
- Send Mail: 25(SMTP), 465(secure SMTP)
- Receive Mail: 110(POP3), 995(secure POP3), 143(IMAP), 993(IMAP over SSL)

#### [CentOS 7]((https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Security_Guide/sec-Using_Firewalls.html))

Check service running: `service firewalld status`

List of the exceptions that will be implemented: `firewall-cmd --permanent --list-all`

To find out all the settings of a zone: `firewall-cmd --zone=public --list-all`

Reload the firewall with out interrupting user connections, with out losing state information: `firewall-cmd --reload`

Reload the firewall and interrupt user connections, to discard state information: `firewall-cmd --complete-reload`

To see any additional services: `firewall-cmd --get-services`

Add a service: `firewall-cmd --permanent --add-service=ssh`

Remove a service `firewall-cmd --permanent --remove-service=ssh`

Add port: `firewall-cmd --permanent --add-port=4444/tcp`

#### [CentOS 6](https://www.digitalocean.com/community/tutorials/how-to-setup-a-basic-ip-tables-configuration-on-centos-6)
[Tutorial](http://www.cyberciti.biz/tips/linux-iptables-examples.html)

##### Block the most common attacks
- We start with empty configuration: `iptables -F`
- First, we start with blocking null packets: `iptables -A INPUT -p tcp --tcp-flags ALL NONE -j DROP`. put off the usual network scanning bots
- The next pattern to reject is a syn-flood attack: `iptables -A INPUT -p tcp ! --syn -m state --state NEW -j DROP`. Syn-flood attack means that the attackers open a new connection, but do not state what they want (ie. SYN, ACK, whatever). They just want to take up our servers' resources. We won't accept such packages.
- Now we move on to one more common pattern: XMAS packets, also a recon packet: `iptables -A INPUT -p tcp --tcp-flags ALL ALL -j DROP`

##### Open up ports for selected services
- The first such thing is a localhost interface: `iptables -A INPUT -i lo -j ACCEPT`
- Now we can allow web server traffic:
        iptables -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT
        iptables -A INPUT -p tcp -m tcp --dport 443 -j ACCEPT
- Now, let's allow users use our SMTP servers:
        iptables -A INPUT -p tcp -m tcp --dport 25 -j ACCEPT
        iptables -A INPUT -p tcp -m tcp --dport 465 -j ACCEPT
- We now proceed to allow the users read email on their server:
        iptables -A INPUT -p tcp -m tcp --dport 110 -j ACCEPT
        iptables -A INPUT -p tcp -m tcp --dport 995 -j ACCEPT
- Now we also need to allow IMAP mail protocol:
        iptables -A INPUT -p tcp -m tcp --dport 143 -j ACCEPT
        iptables -A INPUT -p tcp -m tcp --dport 993 -j ACCEPT

##### Limiting SSH accesse
- normal: `iptables -A INPUT -p tcp -m tcp --dport 22 -j ACCEPT`
- limit: `iptables -A INPUT -p tcp -s YOUR_IP_ADDRESS -m tcp --dport 22 -j ACCEPT`. Replace **YOUR_IP_ADDRESS** with the actuall IP, of course.

Right now, we need to add one more rule that will allow us to use outgoing connections (ie. ping from VPS or run software updates);

    iptables -I INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

It will allow any established outgoing connections to receive replies from the VPS on the other side of that connection. When we have it all set up, we will block everything else, and allow all outgoing connections.

    iptables -P OUTPUT ACCEPT
    iptables -P INPUT DROP

##### Save the configuration
- we can list the rules to see if anything is missing: `iptables -L -n`
- Now we can finally save our firewall configuration: `iptables-save | sudo tee /etc/sysconfig/iptables`
- Just to make sure everything works, we can restart the firewall: `service iptables restart`

### SELinux (Security-Enhanced Linux)
If you'd like to disable SELinux: `vi /etc/selinux/config` and change `SELINUX=disabled`
Save and quit.

### Change hostname
Centos 7:
`hostnamectl status`: Show info of hostname

`hostnamectl --static|--transient|--pretty`: show each kind of hostname. *static* is hostname of kernel save permanently, *transient* temporary use in DHCP, *pretty* free-form of hostname.

`hostnamectl [--static|--transient|--pretty] set-hostname <hostname>`: change hostname.

### Services
Start, stop, restart, view status of a service:

`service <service_name> start|stop|restart|status`

`systemctl start|stop|restart|status <service_name>`

`chkconfig <service_name> on|off`: auto start service when booting.

### Configure timezones
Check current timezone: `timedatectl`

Set timezone: `timedatectl set-timezone Asia/Ho_Chi_Minh`

Synchronization with NTP:
- Install ntp: `yum install ntp`
- Start and enable ntpd service: `systemctl start ntpd $$ systemctl enable ntpd`

### Create a Swap file
Adding "swap" to a Linux server allows the system to move the less frequently accessed information of a running program from RAM to a location on disk. Accessing data stored on disk is much slower than accessing RAM, but having swap available can often be the difference between your application staying alive and crashing. This is especially useful if you plan to host any databases on your system.

Advice about the best size for a swap space varies significantly depending on the source consulted. Generally, an amount equal to or double the amount of RAM on your system is a good starting point.

Allocate the space you want to use for your swap file using the fallocate utility. For example, if we need a 4 Gigabyte file, we can create a swap file located at /swapfile by typing:

    sudo fallocate -l 4G /swapfile

After creating the file, we need to restrict access to the file so that other users or processes cannot see what is written there:

    sudo chmod 600 /swapfile

We now have a file with the correct permissions. To tell our system to format the file for swap, we can type:

    sudo mkswap /swapfile

Now, tell the system it can use the swap file by typing:

    sudo swapon /swapfile

Our system is using the swap file for this session, but we need to modify a system file so that our server will do this automatically at boot. You can do this by typing:

    sudo sh -c 'echo "/swapfile none swap sw 0 0" >> /etc/fstab'

With this addition, your system should use your swap file automatically at each boot.


## Create SSL Certificates
    cd /etc/pki/tls/certs
    make server.key
    ...
    openssl rsa -in server.key -out server.key
    ...
    make server.csr
    ...
    openssl x509 -in server.csr -out server.crt -req -signkey server.key -days 3650
    chmod 400 server.*




## Yum, update and install packages
`yum install <package>`

`yum remove <package>`

### Undo a yum command (example undo all install package and dependencies)
`yum history list <package name>`

Get ID of history

`yum history undo <ID>`


### List all packages is installed
`yum list installed`

### Update
`yum update`: update to latest version of package but not delete obsoletes packages.

`yum upgrade`: same update but delete obsoletes packages.

### Repository
List all repository: `yum repolist`







### Open a port
List all open ports for a zone: `firewall-cmd --zone=dmz --list-ports`

```shell
$ sudo firewall-cmd --zone=public --add-port=80/tcp --permanent
$ sudo firewall-cmd --reload

sudo firewall-cmd --permanent --zone=public --add-service=http
sudo firewall-cmd --permanent --zone=public --add-service=https
sudo firewall-cmd --reload
```


## RPM, packages manager
### Install packages
`rpm -ivh <packages>`

### Upgrade packages
`rpm -Uvh <packages>`

### Remove packages
`rpm -e <part of name package>`



# Centos 6
## [Network](http://www.krizna.com/centos/how-to-setup-network-in-centos-6/)
By default Centos 6 new installation will not have network access , which means you need to configure ip address to the network interfaces by yourself.

    /etc/sysconfig/network-scripts/ifcfg-eth0: to

    DEVICE=eth0
    BOOTPROTO=dhcp
    ONBOOT=yes

## Search package in specific repository
`yum --disablerepo="*" --enablerepo="epel" list available|grep "php"`

## Package info
`yum info <package>`



# php
configuration file: `/etc/php.ini`

extension configuration: `/etc/php.d/*` : contain *.ini file configure extension will load.

## Bootloader
### CentOS 7
Grub2: modify timeout at `/etc/default/grub` edit this and run command `grub2-mkconfig -o /boot/grub2/grub.cfg` to generate new configuration file.

Modify files at `/etc/grub.d/*` to tuning option boot. After edit run command to update configuration file.

### CentOS 6
Modify at `/etc/grub.conf`

# Web development
## nginx
Configuration files: `/etc/nginx/*`
Default document root: `/usr/share/nginx/*`
Log files: `/var/log/nginx/*`

## [tomcat](http://www.davidghedini.com/pg/entry/install_tomcat_6_on_centos)

[archive download](http://archive.apache.org/dist/tomcat)


# Tips and Tricks
## Change ls output color
Copy file `/etc/DIR_COLORS` to home directory of user. Change value of `DIR`

Yellow

	DIR 00;33
