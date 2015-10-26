[TOC]

# Overview
[Vagrant](https://www.vagrantup.com/) is computer software for creating and configuring **virtual development environment**. It can be seen as **a wrapper** around virtualization software such as VirtualBox, VMWare and around configuration management software such as Ansible, Chef, Salt or Puppet.

## What is Vagrant?
Provides easy to configure, reproducible, and portable work virtual environment built on top of virtual machine engine such as VirtualBox, VMWare, AWS, Open Stack, etc.

## Why Vagrant?
- Isolate dependencies and their configuration, consistent environment, without lose any of the tools you're used to working.(editors, browsers, debuggers, etc.) Running code in the same environment, Say goodbye to "works on my machine" bugs.
- Quickly spin up new developers with a powerful, custom stack.
- Share your environment with your team.
- Maintain multiple environments
- Emulate a production environment

>Have you ever heard the following? "Welcome to the team! Here's a list of 15 applications to install, the instructions are in the team room, somewhere. See you in a week!" Or: "What do you mean it broke production, it runs fine on my machine?" Or: "Why is this working on her machine and his machine, but not my machine?"

# Installation
[VirtualBox download](https://www.virtualbox.org/)
[Vagrant download](http://www.vagrantup.com/downloads)

## [Config VAGRANT_HOME](https://harvsworld.com/2014/07/change-vagrant_home-directory-windows/)
Environment variable VAGRANT_HOME will specify directory Vagrant will store user data, contain boxes, plugins, configuration...

On Windows use: `SETX VAGRANT_HOME="Path\To\Vagrant"`

On Linux add line to `.bash_profile`: `export VAGRANT_HOME="X:\PATH\TO\VAGRANT"`

## Some places Vagrant store data
- **VAGRANT_HOME**: store base boxes, add boxes from command `vagrang box add`
- **Project directory**: store private_key, Vagrantfile, provisioning file, some configuration file
- **VirtualBox home**: store virtual machine run on VirtualBox


# Configuration
## how to change Vagrant’s default ssh port redirect
`config.vm.network :forwarded_port, guest: 22, host: 2224, id: 'ssh', auto_correct: true`

# Getting started
## Common Command Line
**Note** change directory to directory contain Vagrantfile before run commands

`vagrant init` : initialize a new vagrant box in the current directory
`vagrant up` : start an existing vagrant environment (box) and provision in
`vagrant ssh` : ssh into a running vagrant box
`vagrant halt` : stop a running vagrant box (shut down the computer)
`vagrant suspend`: hibernate machine running
`vagrant resume` : resume machine hibernated
`vagrant destroy` : completely destroy a vagrant box (delete all the things)

## Term
`Vagrant box` : an instance of *a VirtualBox VM that has been provisioned and started using Vagrant*.
`base box` : a stored VirtualBox machine packaged into a single file. Think of this as the template for your Vagrant box.
`provisioning` : the configuration step that comes after the Vagrant box loads.
`Vagrantfile` : a single file that defines what a particular Vagrant box is, including the base box, network settings, and provisioning.

## Providers
- VirtualBox
- VMWare
- AWS

## Provisioner configure the VM
- [Puppet](http://puppetlabs.com/)
- [Chef](https://www.chef.io/)
- [Ansible](http://www.ansible.com/home)
- Shell script

# Command-Line Interface
`vagrant -h`: show help for Vagrant CLI

`vagrant list-commands`: list all commands of Vagrant CLI

## init
`vagrant init [box-name] [box-url]`: initializes the current directory to be a Vagrant environment by creating an initial Vagrantfile if one doesn't already exist.
- `--force` overwrite any existing Vagrantfile.
- `--minimal` a minimal Vagrantfile will be created. This Vagrantfile does not contain the instructional comments that the normal Vagrantfile contains.
- `--output FILE` will output the Vagrantfile to the given file. `--output -` will be sent to stdout.

## package
`vagrant package`: this packages a currently running VirtualBox environment into a re-usable box. This command cannot be used with any other provider, they must be made by hand.

`vagrant package --base NAME`: instead of packaging a VirtualBox machine that Vagrant manages, this will package a VirtualBox machine that VirtualBox manages. `NAME` should be the name or UUID of the machine from the VirtualBox GUI.

`vagrant package --output NAME`: the resulting package will be saved as `NAME`. By default, it will be saved as `package.box`.

`vagrant package --include x,y,z` additional files will be packaged with the box. These can be used by a packaged Vagrantfile to perform additional tasks.

`vagrant package --vagrantfile FILE` packages a Vagrantfile with the box, that is loaded as part of the Vagrantfile load order when the resulting box is used.

## up
`vagrant up`: creates and configures guest machines according to your Vagrantfile. Start guest machine.

`vagrant up --provider x`: bring the machine up with the given provider. By default this is `virtualbox`

`vagrant up --provision`: force the provisioners run again

`vagrant up --provision-with shell,puppet,z`: this will only run the given provisioners.

## halt
`vagrant halt`: shuts down the running machine Vagrant. Vagrant will first attempt to gracefully shut down the machine by running the guest OS shutdown mechanism. If this fails, or if the `--force` flag is specified, Vagrant will effectively just shut off power to the machine.

## destroy
`vagrant destroy`: stops the running machine and destroys all resources that were created during the machine creation process. `-f` don't ask for confirmation before destroying.


## status
`vagrant status`: show the state of the machines Vagrant is managing.

## global-status
`vagrant global-status`: show the state of all active Vagrant environments on the system for the currently logged in user. Maybe status not true because cache to prune the invalid entries, run global status with the `--prune` flag.

## box
`vagrant box add <base_box_name> <url>` or `vagrant box add <base_box_name>` (this will use name on Atlas base box list): this command will download base box and keep on local boxes list. It will use to build Vagrant box when use `vagrant init && vagrant up` after that.

## reload
`vagrant reload` : run this after make any modifications to the Vagrantfile.

`vagrant reload --provision`: halt and up and apply new provisioning.

`vagrant reload --provision-with puppet,shell`

## provision
`vagrant provision` : run this after make any modifications in provisioning scripts like shell script or Puppet script, etc.

`vagrant provision --provision-with shell` : only the shell provisioner will be run.

## ssh
`vagrant ssh`: SSH into a running Vagrant machine and give you access to a shell.

`vagrant ssh -c "cat /etc/issue"`: run command after option `-c` through SSH prints out the stdout and stderr, and exits.

`vagrant ssh-config`: show valid configuration for an SSH config file to SSH into the running Vagrant machine.



## version
`vagrant version`

# Vagrantfile

# Vagrant Share


# Creating a new base box
## Boxes list
[Atlas](https://atlas.hashicorp.com/boxes/search)
[Vagrantbox.es](http://www.vagrantbox.es/)

## Provisioning
[PuPHPet](https://puphpet.com/) : A simple GUI to set up virtual machines for Web development.

## Base from existing box
1. Start from an existing box
2. Install only the pieces you know you'll always need
3. Clean up
4. Export the .box file (vagrant package)
5. Upload to a web-accessible place
6. Add to Vagrant Cloud

## [From the scratch](http://thornelabs.net/2013/11/11/create-a-centos-6-vagrant-base-box-from-scratch-using-virtualbox.html)
The box only contain:
- Package manager
- SSH
- SSH user so Vagrant can connect
- Perhaps Chef, Puppet, etc.
- Each provider may require additional software: e.g, if you're making a base box for VirtualBox, you'll want to include the VirtualBox guest additions to shared folders work properly. Provider AWS not require it.

Set SELinux to disabled :

`sed -i -e 's/^SELINUX=.*/SELINUX=disabled/' /etc/selinux/config`

### Disk space
Should choose dynamically resizing drive with a large maximum size.

### Memory
User can modify the memory with the Vagrantfile, so don't user too much by default.

### Peripherals (hardware)
Disable any non-necessary hardware such as audio and USB controllers.

### Default user settings
You should create these as defaults if you intend to publicly distribute your box.

If you're creating a base box for private use, you should try not to follow these, as they open up your base box to security risks (known users, passwords, private keys, etc.).

#### "vagrant" user
By default, Vagrant expect a "vagrant" user to SSH into the machine as. This user should be setup with the [insecure keypair](https://github.com/mitchellh/vagrant/tree/master/keys). And set password of user "vagrant" is "vagrant".

Place public key into the `~/.ssh/authorized_keys` file for the "vagrant" user. Make sure that `~/.ssh` has `0700` permissions and the authorized keys file has `0600` permissions.

When Vagrant boots a box and detects the insecure keypair, it will automatically replace it with a randomly generated keypair for additional security while the box is running.

#### "root" password is "vagrant"

#### password-less sudo
`vagrant ALL=(ALL) NOPASSWD: ALL`

Remove line has `requiretty` to sudo work properly without a tty.

#### SSH Tweaks
Keep SSH speedy, set the `UseDNS` configuration to `no` in the SSH server configuration.

SSH configuration file: `/etc/sshd_config` (type command `find / -name sshd_config` to find this file)

#### Windows base box
https://docs.vagrantup.com/v2/boxes/base.html

### Other software
- Chef/Puppet
- VirtualBox guest

#### VirtualBox Guest Additions
```bash
sudo yum groupinstall "Development Tools"
sudo yum install kernel-devel
```

Go to guest VirtualBox GUI, select Devices > Install Guest Additions CD Images...

```bash
sudo mkdir /media/cdrom/
sudo mount /dev/cdrom /media/cdrom/
sudo ./VBoxLinuxAdditions.run
```

### Packaging the box
Packaging the box into a `box` file.

Clean up yum:

`yum clean all`

Clean up the tmp directory:

`rm -rf /tmp/*`

Clean up the last logged in users logs:

`rm -f /var/log/wtmp /var/log/btmp`

Clean up history:

`history -c`

Shutdown the virtual machine:

`shutdown -h now`

`vagrant package --base <name_of_virtual_machine_in_virtualbox>` : file package.box should be in your working directory.

Contents of box file:
- Vagrantfile
- box-disk1.vmdk
- box.ovf
- metadata.json

### Distributing the box
[HashiCorp's Atlas](https://atlas.hashicorp.com/) : public or private boxes.

## VirtualBox provider base box
### Virtual machine
Hard requirements:
- The first network interface (adapter 1) must be a NAT adapter. Vagrant users this to connect the first time.
- The MAC address of the first network interface (the NAT adapter) should be noted, since you'll need to put it in a Vagrantfile later as the value for `config.vm.base_mac`. To get this value, use the VirtualBox GUI.

### Additional software
VirtualBox guest additions

Check version: `VBoxControl --version`
`VBoxService --version`

### Packaging the box
`vagrant package --base <name_of_virtual_machine_in_virtualbox>` : file package.box should be in your working directory.

Contents of box file:
- Vagrantfile
- box-disk1.vmdk
- box.ovf
- metadata.json


# Provisioning
## Basic Usage
First, every provisioner is configured within your Vagrantfile using the `config.vm.provision`.

	Vagrant.configure("2") do |config|
		# ... other configuration

		config.vm.provision "shell" do |s|
			s.inline = "echo hello"
		end
	end

Running provisioners: `vagrant up`, `vagrant provision` and `vagrant reload --provision`. Add flag `--no-provision` can be passed to `up` and `reload` if you don't want to run provisioner.

### Run once or always
By default, provisioners are run once, during the first `vagrant up` since the last `vagrant destroy`, unless the `--provision` flag is set.

Optionally, you can configure provisioners to run on every `up` or `reload`. They'll only be not run if the `--no-provision` flag is explicitly specified. To do this set the `run` option to `always` as shown below:

	Vagrant.configure("2") do |config|
	  config.vm.provision "shell", inline: "echo hello",
	    run: "always"
	end

If you're using the block format, you must specify it outside of the block, as shown below:

	Vagrant.configure("2") do |config|
	  config.vm.provision "shell", run: "always" do |s|
	    s.inline = "echo hello"
	  end
	end

## Multiple provisioners

	Vagrant.configure("2") do |config|
		config.vm.provision "shell", inline: "echo foo"

		config.vm.define "web" do |web|
			web.vm.provision "shell", inline: "echo bar"
		end

		config.vm.provision "shell", inline: "echo baz"
	end

## File
Provision name: `file`

The file provisioner allows you to upload a file from the host machine to the guest machine.

	Vagrant.configure("2") do |config|
		# ... other configuration

		config.vm.provision "file", source: "~/.gitconfig", destination: ".gitconfig"
	end

Above provisioning will replicate local .gitconfig to the vagrant user's home directory on the guest machine so you won't have to run `git config --global` every time you provision a new VM.

## Shell
Provision name: `shell`

Allows you to upload and execute a script within the guest machine.

	Vagrant.configure("2") do |config|
		config.vm.provision "shell",
			inline: "echo Hello, World"
	end

	Vagrant.configure("2") do |config|
		config.vm.provision "shell", path: "script.sh"
	end

## Puppet Apply - Masterless
Puppet must install on guest machine (box) before to use it.

Provision name: `puppet`

### Bare minimum
If directory tree looks like below:

	$ tree
	.
	|-- Vagrantfile
	|-- manifests
	|   |-- default.pp

you can get started with Puppet with just one line in your Vagrantfile:

	Vagrant.configure("2") do |config|
		config.vm.provision "puppet"
	end

### Custom manifest settings
You can override both the directory where Puppet looks for manifests with `manifests_path`, and the manifest file used as the entry-point with `manifest_file`. The path can be relative or absolute. If it is relative, it is relative to the project root.

	Vagrant.configure("2") do |config|
		config.vm.provision "puppet" do |puppet|
			puppet.manifests_path = "my_manifests"
			puppet.manifest_file = "default.pp"
		end
	end

To specify a remote manifests path, use the following syntax:

	Vagrant.configure("2") do |config|
		config.vm.provision "puppet" do |puppet|
			puppet.manifests_path = ["vm", "/path/to/manifests"]
			puppet.manifest_file = "default.pp"
		end
	end

### Modules
Vagrant also supports provisioning with [Puppet modules](http://docs.puppetlabs.com/guides/modules.html). This is done by specifying a path to a modules folder where modules are located. The manifest file is still used as default.

	Vagrant.configure("2") do |config|
		config.vm.provision "puppet" do |puppet|
			puppet.module_path = "modules"
		end
	end

### Custom facts
Custom facts to be exposed by [Facter](http://puppetlabs.com/puppet/related-projects/facter/) can be specified as well:

	Vagrant.configure("2") do |config|
		config.vm.provision "puppet" do |puppet|
			puppet.facter = {
				"vagrant" => "1"
			}
		end
	end

Now, the `$vagrant` variable in your Puppet manifests will equal "1".

### Configuring hiera
[Hiera](http://docs.puppetlabs.com/hiera/1/) configuration is also supported. `hiera_config_path` specifies the path to the Hiera configuration file stored on the host. If the `:datadir` setting in the Hiera configuration file is a relative path, `working_directory` should be used to specify the directory in the guest that path is relative to.

	Vagrant.configure("2") do |config|
		config.vm.provision "puppet" do |puppet|
			puppet.hiera_config_path = "hiera.yaml"
			puppet.working_directory = "/tmp/vagrant-puppet"
		end
	end

`hiera_config_path` can be relative or absolute. If it is relative, it is relative to the project root. `working_directory` is an absolute path within the guest.

### Options
Puppet supports a lot of command-line flags. Basically any setting can be overridden on the command line. To give you the most power and flexibility possible with Puppet, Vagrant allows you to specify custom command line flags to use:

	Vagrant.configure("2") do |config|
		config.vm.provision "puppet" do |puppet|
			puppet.options = "--verbose --debug"
		end
	end


# Providers
## VirtualBox
### Configuration

	config.vm.provider "virtualbox" do |v|
		v.name = "my_vm"
		v.gui = true
		v.cpus = 2
		v.memory = 1024
		v.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
	end

# Work flow
1. cd to project directory
2. vagrant init <base_box>
3. vagrant up (this will run provisioning process from Vagrantfile and Puppet/Chef script)
4. open project on IDE at host machine to develop project
5. test on localhost web page
6. ssh to Vagrant box to tuning thing or solve problems


# Synced Folders


# Multi-Machine


# Plugins
https://github.com/mitchellh/vagrant/wiki/Available-Vagrant-Plugins

https://vagrant-lists.github.io/#plugins


# Environmental Variables


# Troubleshoot
## Debugging

## Vagrant stuck at SSH retrying connect
Debug it by add these line into Vagrantfile and rerun `vagrant up`:

	config.vm.provider :virtualbox do |vb|
		vb.gui = true
	end

Maybe you do not enable virtual machine option on BIOS.

## Vagrant command line stuck
Focus to command line windows and click Enter some times.

## Cannot mount shared folder
Maybe kernel-devel of guest OS box is wrong with kernel-devel of Guest Additions. Reinstall VirtualBox Guest Additions, and install right kernel-devel version. When reinstall VirtualBox Guest Additions it will show error and show right kernel-devel need install.

## Different content of asset files between browser and editor
The server serving the static files is using the "sendfile()" syscall, which is broken with the VirtualBox file system. You need to disable sendfile() usage in your server. For Apache:

Open httpd.conf and edit line: `EnableSendfile off`

# Tutorial (Build Web development environment)
## PHP + nginx


## Create New Base-Box
### 1.1 Steps
- Enable **BIOS processor virtual**.
- Download & Install **VirtualBox and Vagrant**.
- Create **new virtual box machine**.(disable all monitor and usb device.)
- Setup centos on created virtual machine.

### 1.2 Create new virtual box machine
#### Settings Virtual Box
Download the CentOS CentOS-7.0-1406-x86_64-DVD.iso from server 214

Open VirtualBox and click New.

Give the virtual machine a Name: CentOS-7.0.

From the Type dropdown menu choose Linux.

From the Version dropdown menu choose Red Hat (64 bit).

Under Memory size, leave RAM at 512 MB (Vagrant can change this on-the-fly later).

Under Hard drive, select Create a virtual hard drive now, and click Create.

Under File location, leave the default name.

Under File size, change the size to 40.00 GB.

Under Hard drive file type, select VDI (VirtualBox Disk Image).

Under Storage on physical hard drive, select Dynamically allocated, and click Create.

The virtual machine definition has now been created. Click the virtual machine name and click Settings.

Go to the Storage tab, click Empty just under Controller: IDE, then on the right hand side of the window click the CD icon, and select Choose a virtual CD/DVD disk file….

Navigate to where the CentOS-7.0-1406-x86_64-DVD.iso was downloaded, select it, and click Open.

Go to the Audio tab and uncheck Enable Audio.

Go to the Ports tab, then go to the USB subtab, and uncheck Enable USB Controller.

Go to the System tab, then check **CD/DVD** in **boot order list box**, then move **CD/DVD to first**.

Click Ok to close the Settings menu.

#### Installation
Finally, start up the virtual machine to begin installation. Select version minimal to install, set root password is 'vagrant', create new user 'vagrant' with password is 'vagrant' add vagrant to 'wheel' group (admin group - have sudo privileges).

By default Centos 6 new installation will not have network access , which means you need to configure ip address to the network interfaces by yourself.

    /etc/sysconfig/network-scripts/ifcfg-eth0: to

    DEVICE=eth0
    BOOTPROTO=dhcp
    ONBOOT=yes

### 1.3 Create vagrant box

#### Enable openssh

	# yum install openssh-server

	# systemctl enable sshd.service / chkconfig sshd on

#### Install GUEST TOOLS for mount folder
Update kernel:

    # yum update
	# yum install kernel-devel bzip2 gcc
    # yum groupinstall "Development Tools"
    # reboot

Virtual BOX:

    Devices -> Insert Install Guide Image

Install guest tool:

	# mount /dev/cdrom /mnt
	# cd /mnt
	# ./VBoxLinuxAdditions.run

- **Note**: If any error, see it and install more application.

Check

    VBoxControl --version
    VBoxService --version

#### Setup the vagrant user enable use sudo without prompt password.

    # useradd vagrant
    # passwd vagrant
	# visudo

- Enter & Save below line

		vagrant ALL=(ALL) NOPASSWD:ALL

- Setup the vagrant user enable ssh without password.

		mkdir .ssh
		curl -k https://raw.githubusercontent.com/mitchellh/vagrant/master/keys/vagrant.pub > .ssh/authorized_keys
		chmod 0700 .ssh
		chmod 0600 .ssh/authorized_keys

- Disable root tty. It allows ssh to send remote commands using sudo.

		sed -i 's/^\(Defaults.*requiretty\)/#\1/' /etc/sudoers

- If command above is wrong on your machine, don't worry maybe some mad. Just open `/etc/sudoers` file and replace line **Defaults requiretty** by **Defaults !requiretty**

#### Disable SELinux
Set SELinux to disabled :

`sed -i -e 's/^SELINUX=.*/SELINUX=disabled/' /etc/selinux/config`

#### Clean up Before generate box

	yum clean all
	rm -rf /tmp/*
	rm -f /var/log/wtmp /var/log/btmp
	history -c
	shutdown -h now

#### Generate box
    Open command line at folder of host machine where you want to fork box.
    Run

    vagrant package --base <name_virtual_machine>

### 1.4 Start Vagrant Machine
Open command line at folder where you contain the box.

Add Box

	vagrant box add <name_box> <name_base_box>.box

Init

	vagrant init <name_box>

Start

	vagrant up
