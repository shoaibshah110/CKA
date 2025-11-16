# Control Plane 

## What is Kubernetes control plane?

> - **Control Plane** is the **brain** of kubernetes. 
> - It makes all the decisions about the cluster: scheduling, scaling, health and API. 

## The key components, responsibilities and how everything works together. 

### 1. kube-apiserver 

> - The front door of the cluster. Every request goes through it. 

#### What it does?

> - Handles all **kubectl** commands.
> - Validates and processes REST API requests. 
> - Communicates with **etcd** for reading/writing cluster state. 
> - All control-plane components talk through it.

##### Key points:

> - Only **component that talks to etcd directly**.
> - **Stateless** - can scale horizontally. 
> - Exposes the Kubernetes API. 



