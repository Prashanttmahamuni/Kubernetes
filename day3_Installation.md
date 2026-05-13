
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

# Kubernetes Cluster Setup Guide

This guide provides a simple, step-by-step process for setting up a basic Kubernetes cluster on Ubuntu 20.04/22.04 using `kubeadm`. This process assumes you have two or more virtual machines or servers (one master node and at least one worker node).

---

## Prerequisites

- Two or more machines running a compatible Linux distribution (e.g., Ubuntu).
- Sufficient resources on each machine:  
  - **Master:** 2 CPU, 4GB RAM minimum  
  - **Worker:** 1 CPU, 1GB RAM minimum
- Root access or `sudo` privileges on all machines.

---

## Step 1: Install Prerequisites (On Both Master and Worker Nodes)

Run the following commands on **all nodes** to install Docker and Kubernetes tools:

```bash
# Update package list
sudo apt-get update -y

# Install Docker
sudo apt-get install docker.io -y

# Enable and start Docker
sudo systemctl enable --now docker

# Install Kubernetes dependencies
sudo apt-get install -y apt-transport-https ca-certificates curl gnupg
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.29/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

# Add Kubernetes repository
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.29/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update

# Install kubelet, kubeadm, kubectl
sudo apt-get install -y kubelet kubeadm kubectl

# Enable kernel modules for networking
sudo modprobe br_netfilter
echo 'br_netfilter' | sudo tee /etc/modules-load.d/br_netfilter.conf

# Configure network settings
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward = 1
EOF

# Apply sysctl settings
sudo sysctl --system
Step 2: Initialize the Cluster (Master Node Only)
Set up the Kubernetes control plane:

bash
Copy code
# Initialize Kubernetes cluster
sudo kubeadm init --kubernetes-version=1.29.15

# Configure kubectl for your user
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

# Install a Pod Network (CNI), e.g., Calico
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml

# Generate join command for worker nodes
kubeadm token create --print-join-command
Step 3: Join Worker Node (Worker Node Only)
Run the join command copied from the master node:

bash
Copy code
sudo kubeadm join <master-ip>:6443 --token <token> --discovery-token-ca-cert-hash <hash>
Verification
On the master node, verify both nodes are Ready:

bash
Copy code
kubectl get nodes

