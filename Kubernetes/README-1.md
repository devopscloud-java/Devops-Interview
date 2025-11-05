🧩 Kubernetes Interview Cheat Sheet (for DevOps Engineers)
🚀 1. Core Concepts

Pod: Smallest deployable unit; runs one or more containers.

ReplicaSet: Ensures the desired number of identical pods.

Deployment: Manages ReplicaSets, supports rolling updates & rollbacks.

Namespace: Logical grouping of resources.

Labels & Selectors: Identify and filter resources.

Annotations: Store non-identifying metadata.

⚙️ 2. Services & Networking

ClusterIP: Internal access only.

NodePort: Exposes app on <NodeIP>:<Port>.

LoadBalancer: External access via cloud load balancer.

Ingress: Routes HTTP/HTTPS traffic to services.

Network Policy: Controls pod-to-pod communication.

💾 3. Storage & Configuration

Volume: Temporary storage for a pod.

PersistentVolume (PV): Cluster-wide storage resource.

PersistentVolumeClaim (PVC): Pod’s storage request.

StorageClass: Enables dynamic provisioning of PVs.

ConfigMap: Inject non-sensitive config (e.g. app settings).

Secret: Inject sensitive data (e.g. passwords, keys).

🔄 4. Workloads & Controllers

DaemonSet: One pod per node (e.g., log agents).

StatefulSet: For stateful apps (stable IDs & storage).

Job: Run once and exit after completion.

CronJob: Run on a schedule (like cron).

⚖️ 5. Scheduling & Scaling

Requests & Limits: Control resource usage (CPU/mem).

HPA (Horizontal Pod Autoscaler): Scales pods by metrics.

Node Affinity / Anti-Affinity: Pod placement rules.

Taints & Tolerations: Control which pods can run on which nodes.

🧰 6. Configuration & Tools

kubectl: CLI to interact with cluster.

kubeconfig: Cluster connection credentials.

Helm: Package manager for deploying apps.

YAML: Declarative configuration format.

🔐 7. Security

RBAC: Role-Based Access Control (User, Role, RoleBinding).

ServiceAccount: Identity for pod processes.

Secrets Encryption: Protect sensitive values.

Network Policies: Restrict ingress/egress traffic.

📊 8. Monitoring & Logging

kubectl logs / describe / exec: Debug pods.

Liveness Probe: Restarts unhealthy containers.

Readiness Probe: Traffic only to ready pods.

Prometheus + Grafana: Metrics & visualization.

Fluentd / ELK / Loki: Log aggregation.

⚙️ 9. CI/CD & GitOps

Jenkins / GitLab / ArgoCD / Tekton: Integrate K8s in pipelines.

Blue-Green / Canary Deployments: Safe rollout strategies.

GitOps: Manage K8s manifests via Git repos.

☁️ 10. Cloud & Advanced Topics

EKS / AKS / GKE: Managed K8s on AWS, Azure, GCP.

Cluster Autoscaler: Scale nodes automatically.

CRD & Operator: Extend Kubernetes APIs.

Service Mesh (Istio/Linkerd): Traffic control, security, observability.

💡 Quick Commands
kubectl get pods,svc,deploy           # List resources
kubectl describe pod <name>           # Debug pod details
kubectl logs <pod>                    # View pod logs
kubectl exec -it <pod> -- /bin/bash   # Access container shell
kubectl apply -f <file>.yaml          # Apply manifest
kubectl scale deploy <name> --replicas=5
kubectl rollout undo deploy/<name>    # Rollback deployment
