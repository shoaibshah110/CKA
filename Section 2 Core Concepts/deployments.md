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

- you normally interact with the deployment not the ReplicaSet 

---

## Why use a Deployments?
- Self healing - If a pod crashes or is deleted a new one is created automatically
- Scaling - You increase or decrease the number of replicas 
- Rolling Update - Pods are updated gradually to prevent downtime 
- Rollbacks - You can rollback to a previous version if an update fails 

---

##  Key fields in a Deployment 
- Replicas - Defines how pods should be running 
- selector.matchLabels - Tells the deployment which pods it owns and manages
- template - The pod template used to create pods. This contains: 
    - metadata.labels (labels applied to Pods) 
    - spec (how the Pod runs)