
Kubernetes Architecture — Kubelet’s Role

                 ┌──────────────────────────────┐
                 │       Control Plane           │
                 │──────────────────────────────│
                 │                              │
                 │  +------------------------+  │
                 │  |  API Server            |◄────────────┐
                 │  +------------------------+  │          │
                 │  |  Controller Manager     |  │          │
                 │  +------------------------+  │          │
                 │  |  Scheduler              |  │          │
                 │  +------------------------+  │          │
                 │  |  etcd (Key-Value Store) |  │          │
                 │  +------------------------+  │          │
                 └──────────────────────────────┘          │
                                                           │ communicates via API
                                                           │
            ┌────────────────────────────────────────────────────────────┐
            │                        Worker Node                         │
            │────────────────────────────────────────────────────────────│
            │                                                            │
            │   +-------------------+       +-------------------------+  │
            │   |   Kubelet Agent   |◄────► |  API Server (Control)   |  │
            │   | - Starts/Stops Pods|      |                         |  │
            │   | - Reports Status   |      |                         |  │
            │   +-------------------+       +-------------------------+  │
            │            │
            │            │ manages
            │            ▼
            │   +-------------------+
            │   | Container Runtime |
            │   |  (Docker, CRI-O)  |
            │   +-------------------+
            │            │
            │            ▼
            │   +-------------------+
            │   | Running Pods       |
            │   +-------------------+
            └────────────────────────────────────────────────────────────┘

Explanation:

The Kubelet is the bridge between the Control Plane and the node.

The API Server sends Pod specifications to the Kubelet.

The Kubelet:

Talks to the container runtime (e.g., Docker or containerd)

Starts the containers

Reports their health and status back to the Control Plane

This ensures that each node stays in sync with the cluster’s desired state.
