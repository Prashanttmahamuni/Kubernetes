# 🌟 Kubernetes Learning – Day 1

---
dsafsadfasd
## 🚀 Why Kubernetes?

Before Kubernetes, teams used Docker to run containers, but managing them at scale was difficult.  

### Challenges Without Kubernetes:
- ❌ No Auto Restart → If a container crashes, Docker cannot bring it back automatically.  
- ❌ Manual Scaling → Increasing or decreasing app capacity requires manual effort.  
- ❌ No Built-in Load Balancing → External tools were needed to distribute traffic.  
- ❌ Difficult Upgrades → Rolling updates and rollbacks were complex to manage.  
- ❌ Networking Issues → Container-to-container communication was hard.  
- ❌ Secrets & Configs → Storing sensitive data securely was not straightforward.  

### ✅ Kubernetes Solves These By:
- Automated restarts & self-healing.  
- Auto scaling based on demand.  
- Built-in load balancing & service discovery.  
- Rolling updates and rollbacks.  
- Flat networking model for Pods.  
- Secure management of configs & secrets.  
- Efficient scheduling across multiple nodes.  

👉 That’s why Kubernetes is the **industry standard** for container orchestration, used by Google, Netflix, Spotify, AWS, and many others.

---

## ⚡ Kubernetes Core Features

### 1️⃣ Auto Restart
- If a container crashes, **Docker alone cannot restart it automatically**.  
- Kubernetes ensures Pods are always running by **auto-restarting them**.  
- Restart logic is **not dependent on volumes** (volumes = persistent storage).  
- Controlled by:
  - **Liveness Probes** → Restart unhealthy containers.  
  - **Readiness Probes** → Mark pods ready/unready for traffic.  
  - **ReplicaSet** → Ensures desired number of replicas.  

---

### 2️⃣ Auto Healing (Self-Healing)
- Kubernetes **continuously monitors** the health of Pods & Nodes.  
- If a Pod fails health checks:
  - It is **restarted**.  
  - It may be **rescheduled** to a healthy Node.  
- Ensures **high availability** and minimal downtime.  

---

### 3️⃣ Auto Scaling
- Docker cannot scale apps automatically.  
- Kubernetes provides:
  - **HPA (Horizontal Pod Autoscaler)** → Adds/removes Pods based on CPU, memory, or custom metrics.  
  - **VPA (Vertical Pod Autoscaler)** → Adjusts Pod CPU/RAM requests and limits.  
- **Example**: During high traffic, Kubernetes automatically increases the number of Pods.  

---

### 4️⃣ Load Balancing
- Kubernetes Services provide **built-in load balancing**.  
- Distributes traffic across multiple Pods.  
- Supports:
  - **Internal Load Balancing** → Within the cluster.  
  - **External Load Balancing** → Exposed to the internet (via LoadBalancer Service).  

---

### 5️⃣ Networking
- Kubernetes uses a **flat networking model** (all Pods can communicate).  
- Powered by **CNI (Container Network Interface)** plugins like Flannel, Calico, Weave.  
- **Services** → Provide stable internal/external endpoints.  
- **Ingress** → Provides domain-based routing & HTTPS termination.  

---

### 6️⃣ Auto Node Allocation (Scheduling)
- The **Kubernetes Scheduler** decides which Node runs which Pod.  
- Scheduling considers:
  - Available **CPU, RAM, GPU**.  
  - **Taints & Tolerations**.  
  - **Node Affinity / Anti-Affinity rules**.  
- Ensures **efficient resource utilization** across the cluster.  

---
