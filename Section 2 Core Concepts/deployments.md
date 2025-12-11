# Deployments 

## What are deployments?
- A deployment is a Kubernetes controller that manages pods declaratively
- You define the desired state, and kubernetes ensure the cluster matches it
- A deployment does not run containers directly 
- It creates and manages ReplicaSets, which create pods 

---

## Model
 - Deployment
    - ReplicaSet
        - Pods
