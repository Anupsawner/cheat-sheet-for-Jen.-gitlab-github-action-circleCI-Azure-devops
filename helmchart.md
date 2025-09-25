# Karpenter in Kubernetes – Architecture Flow

```text
                 ┌───────────────────────────────┐
                 │   Git Repo / Helm Charts       │
                 └───────────┬───────────────────┘
                             │
                             ▼
                    ┌──────────────────────┐
                    │   K8s API Server      │
                    └─────────┬────────────┘
                              │
           ┌──────────────────┼──────────────────┐
           ▼                  ▼                  ▼
   ┌─────────────┐    ┌──────────────┐   ┌─────────────────┐
   │ Controller  │    │  Scheduler    │   │ etcd (state DB) │
   └───────┬─────┘    └───────┬──────┘   └─────────────────┘
           │                  │
           ▼                  ▼
   ┌─────────────┐     Pod needs CPU > nodes
   │ kube-proxy  │               │
   └───────┬─────┘               ▼
           │              ┌──────────────┐
           ▼              │   Karpenter   │
   ┌───────────────┐      └───────┬──────┘
   │ Worker Node(s)│              │
   │ (kubelet+CR)  │              ▼
   └───────┬───────┘      AWS EC2 Launch API
           │                      │
           ▼                      ▼
      Running Pods        New Node → joins cluster

Step-by-Step Explanation of Each Component
1. Git Repo / Helm Charts

Stores Kubernetes manifests and Helm charts.

Developers push deployment configs here.

CI/CD pipelines (e.g., ArgoCD, Flux, Jenkins) apply these manifests to the cluster.

2. Kubernetes API Server

Central control point of Kubernetes.

Validates and accepts all requests (e.g., deploy pods, create services).

Every other component (controller, scheduler, kubectl, karpenter) talks to the API server.

3. etcd (State Database)

The source of truth for the cluster.

Stores current state (running pods, nodes, configs) and desired state.

When you deploy a pod, the desired state is written to etcd.

4. Controller

Watches the cluster’s state in etcd.

Ensures the actual state matches the desired state.

Example: If a Deployment wants 5 pods but only 3 are running, the controller creates 2 more.

5. Scheduler

Decides where a pod should run.

If no node has enough CPU/Memory → the pod stays in Pending state.

This is when Karpenter comes in.

6. kube-proxy

Runs on each node.

Manages network rules to allow communication between services and pods.

7. Worker Nodes (EC2 instances)

The actual servers (VMs) that run your pods.

Each node runs:

kubelet → agent that talks to API server.

container runtime (e.g., containerd, Docker).

System pods like CoreDNS, kube-proxy.

8. Karpenter

A Kubernetes autoscaler (controller).

Watches for Pending pods that cannot be scheduled.

Decides which instance type (EC2) to launch to fit those pods.

Works much faster and more flexibly than the default Cluster Autoscaler.

9. AWS EC2 Launch API

Karpenter directly calls AWS EC2 APIs.

Launches new instances with the correct subnet, security group, and IAM role.

These new nodes automatically join the cluster via kubelet.

10. Running Pods

Once the new node joins, the pending pods are scheduled there.

Cluster state is updated in etcd.

Karpenter can later terminate unused nodes to save cost.

🔹 End-to-End Flow (Simple Example)

Developer pushes code → CI/CD applies Helm chart to cluster.

API Server receives the request and stores desired state in etcd.

Scheduler tries to place the pod → but finds no node with enough CPU.

Pod remains Pending.

Karpenter detects pending pods via API server.

Karpenter calls AWS EC2 API → provisions a suitable node (e.g., m5.large).

New node boots up, kubelet registers with API server.

Scheduler assigns pending pods to the new node.

Pods run successfully → cluster scales automatically.
