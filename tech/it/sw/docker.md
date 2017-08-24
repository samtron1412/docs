[TOC]

# [Overview](https://www.docker.com/)
[Docker misconceptions](https://devopsu.com/blog/docker-misconceptions/)

[Docker provider](https://www.vagrantup.com/blog/feature-preview-vagrant-1-6-docker-dev-environments.html)

Docker is an open-source project that automates **the deployment of applications inside software containers**, by providing an additional layer of abstraction and automation of [operating-system-level virtualization](https://en.wikipedia.org/wiki/Operating-system-level_virtualization) on Linux.

Docker uses **resource isolation** features of the Linux kernel such as [cgroups](https://en.wikipedia.org/wiki/Cgroups) and **kernel namespaces** to allow independent "containers" to run within a single Linux instance, avoiding the overhead of starting an maintaining virtual machines.

The Linux kernel's support for namespaces mostly isolates an application's view of the operating environment, including process trees, network, user IDs and mounted file systems, while the kernel's cgroups provide resource isolation, including the CPU, memory, block I/O and network.

Since version 0.9, Docker includes the **libcontainer** library as its own way to directly use virtualization facilities provided by the Linux kernel, in addition to using abstracted virtualization interfaces via [libvirt](https://en.wikipedia.org/wiki/Libvirt), [LXC](https://en.wikipedia.org/wiki/LXC) (Linux Containers) and [systemd-nspawn](https://en.wikipedia.org/wiki/Systemd-nspawn).

>Docker is a tool that can package an **application and its dependencies** in a **virtual container** that can run on any Linux server.

# History
**Solomon Hykes** started Docker as an internal project within dotCloud. Docker represents an evolution of dotCloud's proprietary technology.

Docker was released as open source in March 2013. On March 13, 2014, with the release of version 0.9, Docker dropped LXC as the default execution environment and replaced it with its own libcontainer library written in **Go** language.

# Docker internal
Docker implements a **high-level API** to provide lightweight containers that run processes in isolation. Building on top of facilities provided by the Linux kernel (primarily **cgroups** and **namespaces**).

A Docker container, as opposed to a traditional virtual machine, does not require or include a separate operating system. Instead, it relies on the **kernel's functionality** and uses **resource isolation** (CPU, memory, block I/O, network, etc.) and **separate namespaces** to isolate the application's view of the operating system.

Docker accesses the Linux kernel's virtualization features either directly through the provided **libcontainer** library or indirectly via **libvirt**, **LXC** or **systemd-nspawn**.

By using containers, resources can be isolated, services restricted, and processes provisioned to have an almost completely private view of the operating system with their own process ID space, file system structure, and network interfaces. Multiple containers share the same kernel, but each container can be constrained to only use a defined amount of resources such as CPU, memory and I/O.

## How is this different from Virtual Machines?
### Virtual Machines Architecture

![Virtual Machines Architecture](../graphic/docker/virtual-machine-arch.png)

### Docker Engine

![Docker Engine](../graphic/docker/docker-engine.png)

## Operating-system-level virtualization
Operating-system-level virtualization is a server virtualization method where the kernel of an operating system allows for multiple isolated user space instances, instead of just one. Such instances (often called containers, virtualization engines, virtual private servers, or jails) may look and feel like a real server from the point of view of its owners and users.

### Uses
Commonly used in virtual hosting environments.

Separating several applications to separate containers for improved security, hardware independence, and added resource management features.

### Overhead
Operating-system-level virtualization usually imposes little to no overhead, because programs in virtual partitions use the operating system's normal system call interface and do not need to be subjected to emulation or be run in an intermediate virtual machine, as is the case with whole-system virtualizers (such as **VMWare**, [QEMU](https://en.wikipedia.org/wiki/QEMU) or [Hyper-V](https://en.wikipedia.org/wiki/Hyper-V)) and paravitualizers (such as [Xen](https://en.wikipedia.org/wiki/Xen) or [UML](https://en.wikipedia.org/wiki/User-mode_Linux))

### Flexibility
Operating-system-level virtualization is not as flexibility as other virtualization approaches since it cannot host a guest operating system different from the host one, or a different guest kernel. For example, with Linux, different distributions are fine, but other operating systems such as Windows cannot be hosted.


## Docker Engine
The Docker Engine consists of two parts: a **daemon**, a **server process** that manages all the containers; a **client**, which acts as a remote control for the daemon.

You can think of **containers as a process in a box**. The box contains everything the process might need, so it has the filesystem, system libraries, shell and such, but by default none of these are running. You `start` a container by running a process in it.


# Basic
- [Docker cheatsheet and best practices](http://zeroturnaround.com/rebellabs/docker-commands-and-best-practices-cheat-sheet/)

![Docker cheat sheet](../graphic/docker/docker-cheat-sheet-rebellabs.png)

`# docker`: show help for docker commands

`# docker version`: show version of docker client and server

`# docker search <string>`: search container image from Docker Hub Registry

`# docker pull <username>/<container>`: download container image (it will download multiple layers for docker)

`# docker run <username>/<container> echo "hello world"`: run process `echo "hello world"` in container

`# docker run learn/tutorial apt-get install -y ping`: install package `ping` in container but not yet saved

`# docker commit [-author=""] [-m="message commit"] <container id> <new repository name>`: save change of container to new repository (container id get from command `# docker ps -l`)

`# `
`# docker ps`: list container running

`# docker exec -it <id process> bash` : spawn new bash shell for container with ID

`# docker exec -it <name container> bash`: spawn new bash shell for container with name

`# docker stop container <container>`

# Tutorial
## [Docker LAMP](https://www.linode.com/docs/applications/containers/how-to-install-docker-and-deploy-a-lamp-stack/)
- [Another LAMP](https://github.com/tutumcloud/lamp)

## [Docker training](http://www.meetup.com/peoplespace/events/229722697/)
- [Slide](http://cdn.michelleliu.io/training/dockerintro.pdf)
- [Exercise](https://github.com/anonmily/docker-up-and-running)
- [Blog](http://michelleliu.io/devops/a-crash-course-in-docker)

## [Docker birthday 3](https://github.com/docker/docker-birthday-3)
