[TOC]

# Overview

- [Docker misconceptions](https://devopsu.com/blog/docker-misconceptions/)

Docker is an open-source project that automates **the deployment of
applications inside software containers**, by providing an additional
layer of abstraction
    - Deploys applications in a sandbox (containers) to run on the host
    operating system e.g. Linux.

Docker uses **resource isolation** features of the Linux kernel such as
[cgroups](https://en.wikipedia.org/wiki/Cgroups) and **kernel
namespaces** to allow independent "containers" to run within a single
Linux instance, avoiding the overhead of starting an maintaining virtual
machines.

The Linux kernel's support for namespaces mostly isolates an
application's view of the operating environment, including process
trees, network, user IDs and mounted file systems, while the kernel's
cgroups provide resource isolation, including the CPU, memory, block I/O
and network.

Since version 0.9, Docker includes the **libcontainer** library as its
own way to directly use virtualization facilities provided by the Linux
kernel, in addition to using abstracted virtualization interfaces via
[libvirt](https://en.wikipedia.org/wiki/Libvirt),
[LXC](https://en.wikipedia.org/wiki/LXC) (Linux Containers) and
[systemd-nspawn](https://en.wikipedia.org/wiki/Systemd-nspawn).

>Docker is a tool that can package an **application and its
>dependencies** in a **virtual container** that can run on any Linux
>server.

## History

**Solomon Hykes** started Docker as an internal project within dotCloud.
Docker represents an evolution of dotCloud's proprietary technology.

Docker was released as open source in March 2013. On March 13, 2014,
with the release of version 0.9, Docker dropped LXC as the default
execution environment and replaced it with its own libcontainer library
written in **Go** language.

# Versions

## Bundle

- https://docs.docker.com/docker-for-mac/docker-toolbox/
- Docker Desktop (newer version)
    + `docker` and `docker-compose`
    + only one virtual machine
    + there are STABLE and EDGE versions
- Docker Toolbox
    + `docker-machine` => can create multiple virtual machine, routing,
    etc.
    + older than Desktop version

## Specific Tools an Their Functions

- `docker`: Docker Engine
    + builds images and creates containers
- `docker-compose`
    + manages multiple containers
    + creates a network to allow containers communicate
- `docker-machine`
    + creates multiple virtual machines => swarms (multiple containers
    can run on one virtual machine)
- Docker Hub
    + a registry stores all the Docker images
    + similar like GitHub for Docker images
- Kubernetes
    + an operating system of machines (virtual/real)
    + manages and schedules containers on machines

# Tutorials

## Use Cases of Docker

- Trying out new technologies and don't want to mess up your environment
- Working or sharing with other people
    + It also includes the situation in which you move to a new machine,
    and you don't want to reinstall all development tools again.

## General Steps

0. `mkdir apps`
1. `cd apps`
2. `mkdir <container1_name>`
    + e.g., `mkdir website`
3. `mkdir <container2_name>`
    + e.g., `mkdir database`
4. Creating a `Dockerfile` for each container
    + Writing a blueprint for your environment
    + If you don't want to modify the base image from Docker Hub, you
    can use `docker-compose.yml` without `Dockerfile`, but if you want
    to modify something in the base image, you should use `Dockerfile`
    to do that.
5. `vim docker-compose.yml`
    + Specifying configurations for the container: build, command,
    environment, ports, working_dir, depends_on, volumes, etc.
    + Coordinating containers if you have more than one container
6. Using `docker-compose` to manage the services/containers
    + Start all services and detach from the terminal; services run in
    background: `docker-compose start`
    + Stop all services: `docker-compose stop`
    + Launch a specific service: `docker-compose up <service_name>`
    + Restart a single service: `docker-compose restart <name>`
    + Log a service: `docker-compose logs -f <name>`
    + SSH to a service container: `docker-compose exec <name> bash`
7. (Optional) Write a shell script if the command to run
   `docker-compose` is long to type


- `Dockerfile` example

```Dockerfile
FROM ruby:2.3.3
RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs
RUN mkdir /app
WORKDIR /app
```

- `docker-compose.yml` example

```yaml
version: '3'

services:
  njs1:
    build: ./njs1
    command: sh -c "npm install && npm start"
    environment:
      - NODE_ENV=development
      - PORT=7000
    ports:
      - '7000:7000'
    working_dir: /root/njs1
    volumes:
      - ./njs1:/root/njs1:cached # <--- This will map ./njs1 to /root/njs1 inside the container.

  njs2:
    image: node:12.3-alpine
    command: sh -c "npm install && npm start"
    environment:
      - NODE_ENV=development
      - PORT=8000
    ports:
      - '8000:8000'
    working_dir: /root/njs2
    volumes:
      - ./njs2:/root/njs2:cached # <--- This will map ./njs2 to /root/njs2 inside the container.

  py1:
    image: python:3-stretch
    command: sh -c "pip install -r requirements.txt && python -m server"
    environment:
      - PORT=9000
      - FLASK_ENV=development
    ports:
      - '9000:9000'
    working_dir: /root/py1
    volumes:
      - ./py1:/root/py1:cached # <--- This will map ./py1 to /root/py1 inside the container.

  go1:
    image: golang:1.12-alpine
    command: sh -c "go run ."
    environment:
      - PORT=5000
    ports:
      - '5000:5000'
    working_dir: /root/go1
    volumes:
      - ./go1:/root/go1:cached # <--- This will map ./py1 to /root/py1 inside the container.
```

Links
- https://blog.atulr.com/docker-local-environment/
- https://www.netguru.com/codestories/efficient-way-to-use-docker-in-development

# Networking

TODO

# File System Sharing

TODO

# Develop with Docker

## Best Practices

### How to keep images small?

- Start with an appropriate base image. For instance, if you need a JDK,
  consider basing your image on the official `openjdk` image, rather
  than starting with a generic `ubuntu` image and installing `openjdk`
  as part of the Dockerfile.
- Use multistage builds. For instance, you can use the `maven` image to
  build your Java application, then reset to the `tomcat` image and copy
  the Java artifacts into the correct location to deploy your app, all
  in the same Dockerfile. This means that your final image doesn’t
  include all of the libraries and dependencies pulled in by the build,
  but only the artifacts and the environment needed to run them.
    + If you need to use a version of Docker that does not include
    multistage builds, try to reduce the number of layers in your image
    by minimizing the number of separate `RUN` commands in your
    Dockerfile. You can do this by consolidating multiple commands into
    a single `RUN` line and using your shell’s mechanisms to combine them
    together. Consider the following two fragments. The first creates
    two layers in the image, while the second only creates one.

```docker
RUN apt-get -y update
RUN apt-get install -y python
===
RUN apt-get -y update && apt-get install -y python
```

- If you have multiple images with a lot in common, consider creating
  your own base image with the shared components, and basing your unique
  images on that. Docker only needs to load the common layers once, and
  they are cached. This means that your derivative images use memory on
  the Docker host more efficiently and load more quickly.
    + https://docs.docker.com/develop/develop-images/baseimages/
- To keep your production image lean but allow for debugging, consider
  using the production image as the base image for the debug
  image. Additional testing or debugging tooling can be added on top of
  the production image.
- When building images, always tag them with useful tags which codify
  version information, intended destination (`prod` or` test`, for
  instance), stability, or other information that is useful when
  deploying the application in different environments. Do not rely on
  the automatically-created `latest` tag.

### How to persist application data? How to store information?

- Using volumes or bind mounts. **Avoid** storing in the container.
    + volumes: https://docs.docker.com/storage/volumes/
    + bind mounts: https://docs.docker.com/storage/bind-mounts/
- Manage sensitive data with Docker secrets
    + https://docs.docker.com/engine/swarm/secrets/
- Store configuration data using Docker Configs
    + https://docs.docker.com/engine/swarm/configs/

### Use Continuous Integration/Continuous Deployment

TODO

### Differences in Development and Production Environments

| Development                                                        | Production                                                                                                                                                                                                                                       |
|--------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Use bind mounts to give your container access to your source code. | Use volumes to store container data.                                                                                                                                                                                                             |
| Use Docker Desktop for Mac or Docker Desktop for Windows.          | Use Docker Engine, if possible with userns mapping for greater isolation of Docker processes from host processes.                                                                                                                                |
| Don’t worry about time drift.                                      | Always run an NTP client on the Docker host and within each container process and sync them all to the same NTP server. If you use swarm services, also ensure that each Docker node syncs its clocks to the same time source as the containers. |

## Build Images

- Docker builds images automatically by reading instrutions from a
  `Dockerfile`.
- A Docker image consists of read-only layers each of which represents a
  Dockerfile instruction.
    + The layers are stacked and each one is a delta of the changes from
    the previous layer.

```docker
FROM ubuntu:18.04
COPY . /app
RUN make /app
CMD python /app/app.py
```

- When you run an image and generate a container, you add a new WRITABLE
  layer (the “container layer”) on top of the underlying layers. All
  changes made to the running container, such as writing new files,
  modifying existing files, and deleting files, are written to this thin
  writable container layer.

### Build Context

- `docker build`: when enter this command
    + the current directory = build context
    + `Dockerfile` in the current directory is used

### Multi-stage builds

- https://docs.docker.com/develop/develop-images/multistage-build/

## Manage Images

- Docker Hub
    + `docker login`
    + `docker search`
    + `docker pull`
    + `docker push`

# Docker internal

Docker implements a **high-level API** to provide lightweight containers
that run processes in isolation. Building on top of facilities provided
by the Linux kernel (primarily **cgroups** and **namespaces**).

A Docker container, as opposed to a traditional virtual machine, does
not require or include a separate operating system. Instead, it relies
on the **kernel's functionality** and uses **resource isolation** (CPU,
memory, block I/O, network, etc.) and **separate namespaces** to isolate
the application's view of the operating system.

Docker accesses the Linux kernel's virtualization features either
directly through the provided **libcontainer** library or indirectly via
**libvirt**, **LXC** or **systemd-nspawn**.

By using containers, resources can be isolated, services restricted, and
processes provisioned to have an almost completely private view of the
operating system with their own process ID space, file system structure,
and network interfaces. Multiple containers share the same kernel, but
each container can be constrained to only use a defined amount of
resources such as CPU, memory and I/O.

## How is this different from Virtual Machines?

### Virtual Machines Architecture

![Virtual Machines Architecture](../graphic/docker/virtual-machine-arch.png)

### Docker Engine

![Docker Engine](../graphic/docker/docker-engine.png)

## Operating-system-level virtualization

Operating-system-level virtualization is a server virtualization method
where the kernel of an operating system allows for multiple isolated
user space instances, instead of just one. Such instances (often called
containers, virtualization engines, virtual private servers, or jails)
may look and feel like a real server from the point of view of its
owners and users.

### Uses

Commonly used in virtual hosting environments.

Separating several applications to separate containers for improved
security, hardware independence, and added resource management features.

### Overhead

Operating-system-level virtualization usually imposes little to no
overhead, because programs in virtual partitions use the operating
system's normal system call interface and do not need to be subjected to
emulation or be run in an intermediate virtual machine, as is the case
with whole-system virtualizers (such as **VMWare**,
[QEMU](https://en.wikipedia.org/wiki/QEMU) or
[Hyper-V](https://en.wikipedia.org/wiki/Hyper-V)) and paravitualizers
(such as [Xen](https://en.wikipedia.org/wiki/Xen) or
[UML](https://en.wikipedia.org/wiki/User-mode_Linux))

### Flexibility

Operating-system-level virtualization is not as flexibility as other
virtualization approaches since it cannot host a guest operating system
different from the host one, or a different guest kernel. For example,
with Linux, different distributions are fine, but other operating
systems such as Windows cannot be hosted.


## Docker Engine (docker command)

The Docker Engine consists of two parts: a **daemon**, a **server
process** that manages all the containers; a **client**, which acts as a
remote control for the daemon.

You can think of **containers as a process in a box**. The box contains
everything the process might need, so it has the filesystem, system
libraries, shell and such, but by default none of these are running. You
`start` a container by running a process in it.


# Docker Engine Basic (docker command)

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


# Docker Machine (docker-machine command)

- `$ docker-machine create --driver virtualbox default`: create a new virtual machine
- `$ eval $(docker-machine env default)`: connect the shell to the virtual machine
- `$ docker-machine start default`: start the virtual machine
- `$ docker-machine stop default`: stop the virtual machine

# Docker Compose (docker-compose command)

## Create docker-compose.yml

```yaml
version: '3.4'
services:
  dev:
    image: ethanlee/cs61c-env
    security_opt:
      - seccomp:unconfined
    volumes:
      - .:/cs61c
```

## Usage

- `docker-compose run dev bash`: run this command at the directory
  contains the docker-compose.yml to run a bash shell.



# Tips and Tricks

## Running GUI apps in Docker containers

- https://medium.com/@dimitris.kapanidis/running-gui-apps-in-docker-containers-3bd25efa862a
- Install an X Server
    + Mac OS: XQuartz (brew cask install XQuartz)
- Allow remote connections to the X server
- Disable access control of the X server
    + `xhost + <local_ip>`
- Export DISPLAY environment variable
    + `export DISPLAY=<local_ip>:0`
- Run the image
    + `docker run --rm -i -e DISPLAY=<local_ip>:0 sontran/firefox`
    + You can build the image by yourself. Install an application on an
    OS such as ubuntu or alpine.

## Add a new volume in existing containers

- https://stackoverflow.com/questions/28302178/how-can-i-add-a-volume-to-an-existing-docker-container

```bash
$ docker ps  -a
CONTAINER ID        IMAGE                 COMMAND                  CREATED              STATUS                          PORTS               NAMES
    5a8f89adeead        ubuntu:14.04          "/bin/bash"              About a minute ago   Exited (0) About a minute ago                       agitated_newton

$ docker commit 5a8f89adeead newimagename

$ docker run -ti -v "$PWD/dir1":/dir1 -v "$PWD/dir2":/dir2 newimagename /bin/bash
```


## Pair programming with Docker, SSH and TMUX

- Create an container supports ssh and tmux for pair programming.


