

### 🔹 1. **Pods**
> Smallest unit in Kubernetes — like a wrapper around 1 or more containers.

✅ Think of it as:  
> “A box holding one app container, with its own IP, storage, and settings.”

---

### 🔹 2. **Nodes**
> A physical or virtual **machine** that runs your Pods.

✅ Master node = Control plane  
✅ Worker node = Runs your apps

---

### 🔹 3. **Cluster**
> A **group of nodes** managed by Kubernetes.

✅ Think of a "Kubernetes farm" where your apps live.

---

### 🔹 4. **Control Plane**
> The “brain” of Kubernetes.  
Manages everything — scheduling, scaling, healing.

Includes:
- kube-apiserver
- kube-scheduler
- kube-controller-manager
- etcd

---

### 🔹 5. **etcd**
> The **database** of Kubernetes — stores the entire cluster state.

✅ Like the central nervous system 🧠

---

### 🔹 6. **Deployment**
> A Kubernetes object to **manage your app’s rollout** (replicas, upgrades, rollback).

✅ Automates running and scaling containers.

---

### 🔹 7. **ReplicaSet**
> Ensures a certain **number of identical Pods** are always running.

✅ If 3 pods are expected and 1 dies, a new one is created.

---

### 🔹 8. **Service**
> A **stable endpoint** (IP or DNS) to access your Pods — even if Pods change.

Types:
- **ClusterIP** (internal)
- **NodePort** (exposes via node’s IP)
- **LoadBalancer** (cloud external IP)

---

### 🔹 9. **Ingress**
> A smarter way to **route external traffic (HTTP/HTTPS)** to Services.

✅ Acts like a reverse proxy with routing rules and TLS support.

---

### 🔹 10. **Namespace**
> A way to **group resources** in Kubernetes for isolation (like folders).

✅ Great for multi-team, multi-app environments.

---

### 🔹 11. **ConfigMap & Secret**
> Inject configuration into Pods:
- **ConfigMap** = plain text (env variables, config files)
- **Secret** = encrypted data (passwords, keys)

---

### 🔹 12. **StatefulSet**
> Like a Deployment but for **stateful apps** (like databases).

✅ Guarantees **persistent storage** and **stable network identity**.

---

### 🔹 13. **DaemonSet**
> Ensures a Pod runs on **every node** (e.g., logging agents like Fluentd, monitoring agents).

---

### 🔹 14. **Job & CronJob**
> Run **one-time** (Job) or **scheduled** (CronJob) tasks.

✅ Like scheduled scripts or background tasks.

---

### 🔹 15. **Helm**
> The **package manager** for Kubernetes apps.

✅ You install apps via Helm Charts, like:
```bash
helm install my-app bitnami/nginx
```

---

### 🔹 16. **Operator**
> A **custom controller** that knows how to manage a specific app’s full lifecycle (e.g., PostgreSQL, Kafka).

✅ Smart automation beyond what Helm offers.

---

### 🔹 17. **Service Mesh**
> A networking layer (like Istio or Linkerd) that:
- Secures
- Monitors
- Routes
traffic between services.

✅ Great for observability and zero-trust networks.

---

### 🔹 18. **Taints & Tolerations**
> Used to **control Pod scheduling** to nodes.

✅ Example: run only critical Pods on dedicated high-CPU nodes.

---

### 🔹 19. **Affinity & Anti-Affinity**
> Define **where Pods should (or shouldn’t) run** based on rules.

✅ Example: keep Pods on different nodes for high availability.

---

### 🔹 20. **Kubelet**
> A small agent that runs on each node and **talks to the control plane** to manage Pods locally.

---

## 🧠 Summary Table

| Buzzword | Meaning |
|----------|---------|
| Pod | Smallest deployable unit (holds container) |
| Node | Worker machine |
| Deployment | Controller for managing app pods |
| Service | Stable access to pods |
| Ingress | HTTP(S) router |
| ConfigMap/Secret | Inject app configs |
| StatefulSet | Run stateful apps like DBs |
| DaemonSet | Run on every node |
| Job/CronJob | One-time or scheduled task |
| Helm | App package manager |
| Operator | App-specific automation logic |
| Kubelet | Node-level agent |

---
