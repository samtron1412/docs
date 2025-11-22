# Overview

# Core components and concepts

## Introduction

Container Engine: The software that manages containers, responsible for running and orchestrating them. Examples include Docker and containerd.
Container Image: A lightweight, standalone, executable package that includes everything needed to run a piece of software: the code, a runtime, libraries, environment variables, and configuration files.
Container: A runnable instance of a container image. It is a live, running process with its own isolated filesystem, processes, and network space.
Isolation: Containers achieve isolation by using the host operating system's kernel features, such as namespaces (to isolate processes, network, etc.) and cgroups (to limit resource usage). This is a key difference from virtual machines, which have their own full operating systems.
Orchestration: The automation of the deployment, scaling, and management of containerized applications. Tools like Kubernetes and Docker Swarm handle tasks like load balancing, scaling, and self-healing for clusters of containers.
Key benefits and principles
Environment Consistency: Containers ensure that an application runs the same way regardless of where it's deployed—from a developer's laptop to a testing server to a production environment.
Dependency Management: By bundling an application with its dependencies, containers eliminate the "it works on my machine" problem, as all necessary libraries and configurations are included in the image.
Portability: Containers are lightweight and portable, making it easy to move an application across different infrastructures, such as from on-premises servers to the cloud.
Ephemeral Nature: Containers are often designed to be disposable. Instead of updating a running container, a new image is built, and the container is replaced.
Volumes: For persistent data, containers rely on volumes, which are managed separately from the container's filesystem. This allows data to persist even if the container is destroyed and recreate

## Containerization vs Virtualization

- LXC vs Docker vs VM
    + https://www.reddit.com/r/Proxmox/comments/15ni84i/when_do_you_use_docker_vs_lxc_vs_a_vm/

## Container Runtime / Engine

- https://kubernetes.io/docs/setup/production-environment/container-runtimes/
- Container Runtime Interface
    + https://kubernetes.io/docs/concepts/containers/cri/
- https://www.reddit.com/r/kubernetes/comments/9y89wu/a_comparison_of_container_runtimes/

Container runtimes are software components responsible for running and managing containers. They can be broadly categorized into three types:
1. Low-level runtimes:
These runtimes directly interact with the operating system kernel to create and manage container processes. They are typically OCI (Open Container Initiative) compliant.
runC: The most widely used OCI-compliant runtime, originally developed by Docker and donated to the OCI.
crun: A fast and lightweight OCI-compliant runtime focused on efficiency.
runhcs: A fork of runC used by Microsoft for running Windows containers.
2. High-level runtimes:
These runtimes provide a higher-level interface for managing containers, often building upon low-level runtimes. They handle tasks like image management, networking, and storage.
containerd: A core component of Docker and a widely adopted high-level runtime, known for its stability and OCI compliance.
CRI-O: A lightweight runtime specifically designed for Kubernetes, focusing on the Container Runtime Interface (CRI).
Docker (dockerd): The daemon that manages the entire Docker platform, including container lifecycle, image management, and orchestration.
3. Sandboxed and virtualized runtimes:
These runtimes offer enhanced isolation and security by running containers within a lightweight virtual machine or a secure sandbox.
Kata Containers: An OCI-compliant runtime that provides VM-level isolation for containers, leveraging hardware virtualization.
gVisor (runsc): An OCI-compliant runtime from Google that provides a secure sandbox for containers, offering a faster startup time than full VMs.
Other notable container runtimes and related tools:
Podman: A daemonless container engine that allows running and managing OCI containers.
Nvidia runtime: A specialized runtime designed to enable GPU access for containers.
Systemd-nspawn: A lightweight container solution provided by systemd.


# Open Container Initiative (OCI)

- OCI in containerization refers to the Open Container Initiative, a project that creates open industry standards for container formats and runtimes. These standards ensure that containers are interoperable and can be built, distributed, and run consistently across different platforms, tools, and cloud providers.

Key components of OCI
Image Specification: Defines the standard for what a container image looks like, including its manifest, configuration, and filesystem layers. This allows any OCI-compliant runtime to use an image from any OCI-compliant registry.
Runtime Specification: Specifies how to create and run a container from an unpacked bundle. It defines the low-level configuration and lifecycle of a container process.
Distribution Specification: Defines a standard API protocol for distributing container images, covering how to push and pull images from registries.
Why OCI is important
Interoperability: OCI standards ensure that an image built with one tool (like Docker or Podman) can be run by any other OCI-compliant runtime.
Portability: OCI containers are not locked into a specific technology provider or cloud service, making applications highly portable across different environments.
Ecosystem stability: The OCI was founded by major industry players like Docker and CoreOS to avoid fragmentation and ensure a stable, shared standard for the growing container ecosystem
