# Kubernetes

**Kubernetes**, also known as **K8s**, is an open source system for automating deployment, scaling, and management of containerized applications.

- High scaling
- Automated rollouts and rollbacks
- Service discovery and load balancing
- Storage orchestration
- Self-healing

## Architecture

- Nodes: typically virtual or physical machines
  - Worker nodes: run applications
    - Each node runs following components:
      - Container runtime: e.g., Docker, containerd
      - Kubelet: agent that communicates with the master
      - Kube-proxy: network proxy for services
  - Master nodes: manage the cluster
    - API server: front-end for the control plane
    - Controller manager: manages controllers
    - Scheduler: assigns work to nodes
    - etcd: distributed key-value store for configuration data
