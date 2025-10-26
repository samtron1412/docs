# Overview

Kubernetes (K8s) is an open-source system for automating deployment,
scaling, and management of containerized applications.
- It's similar an operating system of containers (instead of processes)

# Glossary

- https://kubernetes.io/docs/reference/glossary/?fundamental=true

```
Cluster
A cluster is the core of a Kubernetes environment and consists of a control plane and one or more worker nodes. It provides a unified computing environment that automates the deployment, scaling, and management of your applications.

    Control Plane: The "brain" of the cluster, which makes decisions about scheduling, detects and responds to cluster events, and manages the lifecycle of all Kubernetes objects.
    Nodes: The machines (physical or virtual) that run your applications. They are managed by the control plane and contain the necessary services to run pods.

Nodes
A node is a worker machine in a Kubernetes cluster. Each node has the following components:

    Kubelet: An agent that runs on each node to ensure the containers inside pods are running and healthy.
    Container Runtime: The software, such as containerd or Docker, that runs the containers.
    Kube-proxy: A network proxy that maintains network rules on nodes and facilitates communication between pods.

Pods
A pod is the smallest and most fundamental deployable unit in Kubernetes.

    Logical Host: A pod acts as an application-specific logical host for one or more containers that are tightly coupled and share resources.
    Shared Resources: The containers within a pod share a network namespace, a unique IP address, and storage volumes, enabling them to communicate with each other using localhost.
    Ephemeral: Pods are designed to be temporary. If a node fails, identical replacement pods are scheduled on other available nodes in the cluster.

Namespaces
Namespaces are a way to divide a single Kubernetes cluster into virtual sub-clusters.

    Resource Isolation: They create isolated environments for resources, preventing naming conflicts and allowing multiple teams to work in the same cluster without interfering with each other.
    Resource Management: They allow administrators to partition cluster resources and set resource quotas for each namespace.
    Built-in Namespaces: A new Kubernetes cluster comes with several predefined namespaces, such as default, kube-system, and kube-public.

Templates
While Kubernetes does not have a built-in templating mechanism, the term often refers to the blueprint for creating resources, defined in YAML or JSON files.

    Declarative Configuration: These templates declare the desired state of an application, including the container image, replicas, and ports.
    Automation: Tools like Helm and Kustomize are commonly used to manage and apply these templates for automated deployments.
    Pod Template: A Deployment, for example, contains a template section that describes the pod Kubernetes will create.

Other important terms

    Deployment: A Kubernetes object that manages a set of identical pods, automatically replacing any instances that fail. It provides declarative updates for pods and ReplicaSets.
    Service: An object that exposes an application running on a set of pods as a network service. It provides a stable IP address and DNS name for the pods, load-balancing traffic among them.
    kubectl: A command-line tool for managing Kubernetes clusters. It communicates with the cluster's API server to create, update, and delete resources.
    Controller: Control loops within the Kubernetes control plane that watch the state of your cluster and request changes to move the current state closer to the desired state
```
