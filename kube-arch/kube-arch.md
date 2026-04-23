# Kubernetes Architecture
A Kubernetes Cluster is a group of nodes that work together to run containerized applications.

It contains two main components:
- **Control Plane -** Manages and controls the entire kubernetes cluster.
- **Worker Nodes -** These nodes run application workloads(pods)

## Control Plane Components
### API Server
The API server is the central communication hub for kubernetes cluster. In simple words, it is the front door of the cluster.

**What it does -**
- receives requests from kubectl
- validates and processes requests
- updates cluster ste in etcd
- communicates with other components such as kubectl, schedular, controllers, etcd, kubelet etc.

### Schedular
The schedular is a control plane component that decides which worker node a newly created pod should run on. It makes decision based on few factors like:
- CPU and memory availability
- node health
- scheduling policies
- affinity and taints/tolerations
- resource request/limits

### etcd
Database of the kubernetes cluster, stores all cluster data and configurations (pods, nodes, configs, secrets etc.). Because it stores the entire cluster data, it must be
highly available and backed up regularly.

### Controller Manager
The controller manager runs multiple controllers that continuously monitor the cluster and maintain the desired state of the cluster.
- **Node Controller -** detects node failure
- **Replicaset Controller -** maintains pod replicas
- **Deployment Controller -** manages rollout/rollback

Example - if a pod crashes, a controller ensures a new pod is created automatically.

## Worker Node Components
### Kubelet
The kubelet is an agent that runs on every worker node. It:
- receives instructions from the API server
- ensures containers defined in pods are running
- reports node and pod status back to the control plane

### Kube-proxy / Service-proxy
Kube-proxy is a networking component that runs on every worker node. It:
- manages network rules
- enables communication between service and pods
- provides basic load balancing across pods

### Container Runtime
The container runtime is the component responsible for running containers. Examples: containerd, CRI-O etc.

### CNI 
CNI (Container Network Interface) is a network plugin system for kubernetes that provides networking for pods in the cluster. It ensures that:
- pods can communicate with each other
- pods can communicate across nodes
Popular CNI plugins include: Calico, Flannel, WeaveNetm Cilium etc.

## Kubectl
Kubectl is the command-line-interface(CNI) tool used to interact with a kubernetes cluster, technically it is not part of either control-plane or worker node.

**What it does -**
- sends commands to the API server
- creates, updates, deletes kubernetes resources
- retrieves cluster informations
