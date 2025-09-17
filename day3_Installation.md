
### 📚 **Kubernetes Cluster Fundamentals**

A **Kubernetes cluster** consists of a group of machines, called **nodes**. These nodes are categorized into two types: a single **Master Node** (or control plane) and one or more **Worker Nodes**. The master node manages the cluster, while worker nodes run the containerized applications.

***

### 🛠️ **Core Components & Prerequisites**

Before setting up a cluster, each node must have a **container runtime** (like Docker) installed. Additionally, three key Kubernetes tools are required on every node:
-   **kubeadm**: A command-line tool used to **bootstrap** the cluster.
-   **kubectl**: The **command-line interface** (CLI) for interacting with and managing the cluster.
-   **kubelet**: An **agent** that runs on each node and ensures that containers are running in a Pod. It communicates with the master node.

***

### 🚀 **Cluster Setup Process**

The cluster is initialized on the **master node** using the `kubeadm init` command. This process sets up the control plane and assigns a virtual private subnet (VPS) for the cluster's networking. **Worker nodes** then join the cluster by executing a specific `kubeadm join` command provided by the master, which includes a unique token for authentication.

To enable **Pod-to-Pod communication** within the cluster, a **CNI plugin** (like Calico or Flannel) must be installed after initialization.

***

### 🌐 **High Availability (HA) & Scaling**

For increased reliability and to prevent a single point of failure, you can deploy **multiple master nodes**. This ensures that if one master node fails, another can take over, maintaining the cluster's availability.

To scale the cluster, new worker nodes can be added by simply running the `kubeadm join` command on them. This process can be automated using scripts or cloud functions to automatically add nodes.

***

### 🖼️ **Kubernetes Architectural Diagram**

The Kubernetes architecture can be visualized with the master node managing the cluster's state and communicating with the worker nodes. The worker nodes, in turn, host the Pods and containers that make up your applications.



The **Master Node** houses the Control Plane components:
-   **API Server**: Exposes the Kubernetes API.
-   **etcd**: A distributed key-value store that holds all cluster data.
-   **Scheduler**: Watches for new Pods and assigns them to available nodes.
-   **Controller Manager**: Runs various controllers that manage the state of the cluster.

The **Worker Nodes** contain the essential components for running workloads:
-   **Kubelet**: The primary agent that ensures Pods are running.
-   **Container Runtime**: The engine (e.g., Docker) that runs the containers.
-   **Kube-proxy**: A network proxy that maintains network rules and enables Pod-to-Pod communication.



