⚡ Kubernetes Core Features

1️⃣ Auto Restart

If a container crashes, Docker alone cannot restart it automatically.

Kubernetes automatically restarts Pods to maintain the desired state.

It doesn’t depend on volumes for restart (volumes are for persistent storage).

Controlled by Liveness/Readiness Probes and the ReplicaSet mechanism.

2️⃣ Auto Healing (Self-Healing)

Kubernetes continuously monitors health of Pods and Nodes.

If a Pod fails health checks, Kubernetes:

Restarts the Pod.

Reschedules it on a healthy Node if required.

Ensures services remain available during failures.

3️⃣ Auto Scaling

Docker alone cannot scale apps automatically.

Kubernetes provides Autoscaling mechanisms:

HPA (Horizontal Pod Autoscaler) → Adds/removes Pods based on CPU, memory, or custom metrics.

VPA (Vertical Pod Autoscaler) → Adjusts CPU/RAM requests and limits of Pods.

Example: During high traffic, Kubernetes can add more Pods automatically.

4️⃣ Load Balancing

Kubernetes Services provide built-in load balancing.

Distributes traffic across multiple Pods.

Supports:

Internal Load Balancing → within the cluster.

External Load Balancing → exposed to the outside world.

5️⃣ Networking

Kubernetes uses a flat networking model → all Pods can communicate with each other.

Uses CNI (Container Network Interface) plugins such as Flannel, Calico, Weave.

Services and Ingress expose apps inside/outside the cluster.

6️⃣ Auto Node Allocation (Scheduling)

Kubernetes scheduler decides which Node runs which Pod.

Scheduling is based on:

Available CPU, RAM, GPU, etc.

Taints, Tolerations, and Node Affinity rules.

Ensures efficient resource utilization.
