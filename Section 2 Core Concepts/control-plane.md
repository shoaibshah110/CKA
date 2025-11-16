# Control Plane 

## What is Kubernetes control plane?
- **Control Plane** is the **brain** of kubernetes. 
- It makes all the decisions about the cluster: scheduling, scaling, health and API. 

---

## The key components, responsibilities and how everything works together:

---

# 1. kube-apiserver 
- The front door of the cluster. Every request goes through it. 

## What it does?
- Handles all **kubectl** commands.
- Validates and processes REST API requests. 
- Communicates with **etcd** for reading/writing cluster state. 
- All control-plane components talk through it.

## Key points:
- Only **component that talks to etcd directly**.
- **Stateless** - can scale horizontally. 
- Exposes the Kubernetes API. 

---

# 2. etcd
- The cluster's database - stores the entire state of kubernetes. 

## What it stores:
- Pods
- Deployments 
- Secrets
- ConfigMaps
- Nodes
- Services 
- Everything in the cluster

## Key points:
- MUST be backed up regularly. 
- Highly consistent, distributed key-value store. 
- Control Plane depends completely on etcd health.

---

# 3. Kube-scheduler 
- Decides which node a Pod should run on. 

## How it decides:
- Node resource requests/limits
- Node capacity
- Affinity/anti-affinity rules
- Taints & tolerations
- Pod topology spread
- Node selectors
  
## Key points: 
- Does not run pods it assigns them. 
- If a node becomes unavailable, schedular reschedules to another. 

---

# 4. Kube-controller-manager
- Runs all the controllers that keep the cluster in the desired state. 

## Important controllers:
- **Node controller**: Monitors nodes, marks them NotReady  
- **Replication controller**: Ensures the correct number of pods
- **Deployment controller**: Manages ReplicaSets
- **EndpointSlice Controller**: Updates services 
- Service account & token controllers. 

## Key points:
- A controller = watch + compare + act 
- It's one binary running many controllers

