# Control Plane 

## What is Kubernetes control plane?
- **Control Plane** is the **brain** of Kubernetes
- It makes all the decisions about the cluster: scheduling, scaling, health and API

---

## The key components, responsibilities and how everything works together:

---

# 1. kube-apiserver 
- The front door of the cluster. Every request goes through it

## What it does?
- Handles all **kubectl** commands
- Validates and processes REST API requests
- Communicates with **etcd** for reading/writing cluster state
- All control-plane components talk through it

## Key points:
- Only **component that talks to etcd directly**
- **Stateless** - can scale horizontally
- Exposes the Kubernetes API

---

# 2. etcd
- The cluster's database - stores the entire state of Kubernetes

## What it stores:
- Pods
- Deployments 
- Secrets
- ConfigMaps
- Nodes
- Services 
- Everything in the cluster

## Key points:
- MUST be backed up regularly
- Highly consistent, distributed key-value store
- Control Plane depends completely on etcd health

---

# 3. Kube-scheduler 
- Decides which node a Pod should run on

## How it decides:
- Node resource requests/limits
- Node capacity
- Affinity/anti-affinity rules
- Taints & tolerations
- Pod topology spread
- Node selectors
  
## Key points: 
- Does not run pods it assigns them
- If a node becomes unavailable, schedular reschedules to another

---

# 4. Kube-controller-manager
- Runs all the controllers that keep the cluster in the desired state

## Important controllers:
- **Node controller**: Monitors nodes, marks them NotReady  
- **Replication controller**: Ensures the correct number of pods
- **Deployment controller**: Manages ReplicaSets
- **EndpointSlice Controller**: Updates services 
- Service account & token controllers

## Key points:
- A controller = watch + compare + act 
- It's one binary running many controllers

--- 

# 5. cloud-controller-manager
Integrates Kubernetes with your cloud provider(AWS, GCP, Azure)

## What it handles:
- Load balancers
- Persistent Volumes (EBS/EFS)
- Node lifecycle
- Cloud-specific networking

## Key points:
- Only runs when using a cloud provider integration
- Separates cloud logic from core Kubernetes logic
  
---

# How the control plane works together:
- 1. You run a command 'kubectl apply -f deployment.yaml'
- 2. **kube-apiserver** validates it and writes the desired state to etcd
- 3. **controller-manager** notices the new Deployment and creates a ReplicaSet
- 4. The ReplicaSet needs pods - controller-manager requests them
- 5. **scheduler** finds nodes for each Pod (based on rules + resources) 
- 6. **Nodes** run the Pods via **kubelet** (worker node component)
- 7. if anything changes (Pod dies, node dies) controllers fix it
  
---

# Key control plane concepts you must know for CKA:
**Desired VS Actual State**
- Controllers are constantly trying to make the actual state match the desired state stored in etcd

**The API server is the centre**
- All commands, controllers, scheduler and kubelets communicate only through the API server

**etcd must be protected**
- backups are essential
- if etcd is corrupted or lost, the entire cluster is lost 

**Control plane components run on master nodes**
- Usually in /etc/kubernetes/manifests as static Pods (in kubeadm clusters)

**Highly available setups**
- Multiple API servers
- **etcd** clusters (recommend 3, 5, 7 nodes) 
  


