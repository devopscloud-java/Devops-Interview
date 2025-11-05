# 🌟 Kubernetes Interview Questions and Answers

This directory contains **frequently asked Kubernetes interview questions and answers** — from beginner to advanced DevOps topics.
Perfect for quick revision or interview preparation.

---

## 🧩 Kubernetes Architecture Overview

Below is a simple view of the **Kubernetes architecture** showing how control plane and worker nodes interact:

```
                +------------------------------------+
                |        Control Plane (Master)       |
                |------------------------------------|
                | API Server | etcd | Scheduler | CM  |
                +------------------+-----------------+
                               |
                               |
                     (cluster management)
                               |
          ------------------------------------------------
          |                      |                      |
+----------------+     +----------------+     +----------------+
|   Worker Node 1|     |   Worker Node 2|     |   Worker Node 3|
|----------------|     |----------------|     |----------------|
| kubelet        |     | kubelet        |     | kubelet        |
| kube-proxy     |     | kube-proxy     |     | kube-proxy     |
| Container Runt.|     | Container Runt.|     | Container Runt.|
|----------------|     |----------------|     |----------------|
|   Pods + Svc   |     |   Pods + Svc   |     |   Pods + Svc   |
+----------------+     +----------------+     +----------------+
```

* **Control Plane:** Manages cluster state and scheduling.
* **Worker Nodes:** Run the actual containerized workloads.
* **Pods:** Smallest deployable units.
* **Services:** Expose Pods to internal/external clients.

---

## 📘 1. Basic Kubernetes Questions

### 1. What is Kubernetes?

Kubernetes (K8s) is an open-source container orchestration platform that automates deployment, scaling, and management of containerized applications.

### 2. Main Components of Kubernetes Architecture

* **Control Plane (Master Node):**

  * API Server
  * etcd
  * Controller Manager
  * Scheduler
* **Worker Node:**

  * kubelet
  * kube-proxy
  * Container Runtime (Docker, containerd)

### 3. What is a Pod?

A Pod is the smallest deployable unit that can contain one or more containers sharing the same network and storage.

### 4. What is a ReplicaSet?

Ensures a specified number of identical Pods are running at all times.

### 5. What is a Deployment?

Manages ReplicaSets and supports rolling updates, rollbacks, and versioned deployments.

### 6. What are Namespaces?

Used to divide cluster resources among multiple users or projects for better organization.

### 7. What is the role of Kubelet?

Runs on each node, ensuring containers are running as expected.

### 8. What is etcd?

A distributed key-value store for all cluster configuration data.

---

## ⚙️ 2. Intermediate Questions

### 9. Difference between Deployment and StatefulSet

* **Deployment:** Stateless apps (interchangeable Pods)
* **StatefulSet:** Stateful apps (persistent identity & storage)

### 10. What is a DaemonSet?

Ensures a Pod runs on all (or specific) nodes — often used for monitoring agents.

### 11. What is a Service?

Provides stable networking to access Pods.
Types: `ClusterIP`, `NodePort`, `LoadBalancer`, `ExternalName`

### 12. What is Ingress?

Manages external HTTP/HTTPS access and routing rules.

### 13. What are ConfigMaps and Secrets?

* **ConfigMap:** Non-sensitive configuration data.
* **Secret:** Sensitive data (e.g., passwords, tokens).

### 14. What are PV and PVC?

* **Persistent Volume (PV):** Cluster storage resource.
* **Persistent Volume Claim (PVC):** User request for storage.

### 15. What are Labels and Selectors?

Used to organize and select Kubernetes objects based on key-value pairs.

---

## 🚀 3. Advanced / DevOps-Level Questions

### 16. What is Node Affinity?

Constraint that decides which nodes a Pod can be scheduled on, based on labels.

### 17. What are Taints and Tolerations?

Used to control which Pods can be scheduled on specific nodes.

### 18. How to perform rolling updates and rollbacks?

```bash
kubectl rollout status deployment/<deployment-name>
kubectl rollout undo deployment/<deployment-name>
```

### 19. What are Helm Charts?

Helm is Kubernetes’ package manager. Charts are reusable YAML templates for easy app deployment.

### 20. Difference between HPA and VPA

* **HPA:** Scales Pod count.
* **VPA:** Adjusts CPU/memory of existing Pods.

### 21. What are Probes?

* **Liveness Probe:** Checks if container is running.
* **Readiness Probe:** Checks if ready for traffic.
* **Startup Probe:** Checks if app inside container has started.

### 22. How to troubleshoot a failed Pod?

```bash
kubectl get pods
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl exec -it <pod-name> -- /bin/bash
```

### 23. Difference between ClusterIP, NodePort, LoadBalancer

| Type         | Scope                      | Use Case                   |
| ------------ | -------------------------- | -------------------------- |
| ClusterIP    | Internal only              | Internal communication     |
| NodePort     | Exposes service on node IP | Simple external access     |
| LoadBalancer | Uses cloud load balancer   | Production external access |

### 24. What is kube-proxy?

Manages network rules and routes traffic between Pods and Services.

### 25. How to secure a Kubernetes cluster?

* Use RBAC for user permissions
* Enable Network Policies
* Use Secrets for sensitive data
* Keep Kubernetes and images updated
* Use Namespaces and Service Accounts

---

## 🧠 Additional Resources

* [Kubernetes Official Docs](https://kubernetes.io/docs/)
* [Helm Documentation](https://helm.sh/docs/)
* [Kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

---
