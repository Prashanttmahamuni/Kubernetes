# 🌟 Kubernetes Learning – Day 2
This section covers the **core Kubernetes objects** that form the building blocks of every cluster.

---asdsad

## 1️⃣ Pod
- The **smallest deployable unit** in Kubernetes.  
- Wraps **one or more containers** that share:
  - Networking (same IP & port space).  
  - Storage (volumes).  
- **Ephemeral** → Pods can be created, destroyed, restarted anytime.

### Types of Workload Controllers
- **Pod** → Standalone container, no self-healing.  
- **ReplicationController (RC)** → Legacy, ensures a fixed pod count.  
- **ReplicaSet (RS)** → Ensures replicas, but no rollback/versioning.  
- **Deployment** → ⭐ Most used. Supports rolling updates, rollback, scaling.  
- **StatefulSet** → For stateful apps (databases), stable identity & storage.  
- **DaemonSet** → Runs one pod per node (e.g., logging agents).  

---

## 2️⃣ Service
Provides a **stable networking endpoint** for accessing Pods (since Pod IPs are dynamic).

### Types of Services
- **ClusterIP** → Default, internal-only load balancing.  
- **NodePort** → Exposes app on `<NodeIP>:<NodePort>`.  
- **LoadBalancer** → Uses cloud provider’s load balancer (e.g., AWS ELB/ALB).  
- **ExternalName** → Maps service to an external DNS name.  

---

## 3️⃣ Volume
Manages **storage for containers**.  
- `emptyDir` → Temporary storage, deleted with Pod.  
- `hostPath` → Mounts host node’s directory.  
- **Cloud Volumes** → AWS EBS, EFS, GCP Persistent Disk.  
- **PersistentVolume (PV) + PersistentVolumeClaim (PVC)** → Kubernetes-native persistent storage.  

---

## 4️⃣ Networking
- Kubernetes uses a **flat networking model**.  
- Every Pod gets its **own IP**.  
- Pods can communicate **without NAT**.  
- Powered by **CNI plugins** like Calico, Flannel, Weave.  

---

## 5️⃣ ConfigMap
- Stores **non-sensitive config data** in key-value pairs.  
- Mounted as files or environment variables.  
- Example: Database hostnames, app settings.  

---

## 6️⃣ Secret
- Stores **sensitive data** (passwords, API keys, TLS certs).  
- Encoded in **base64** (⚠️ not encrypted by default).  
- Best practice → integrate with **AWS Secrets Manager / KMS / CloudHSM** for real encryption.  

---

## 7️⃣ Ingress
- Manages **HTTP/HTTPS access** into the cluster.  
- Provides:
  - Domain-based routing (`api.example.com → service`).  
  - SSL/TLS termination.  
  - Load balancing for HTTP apps.  
- Needs an **Ingress Controller** (NGINX, AWS ALB Ingress, etc.).  

---
