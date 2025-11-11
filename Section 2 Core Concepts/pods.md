# PODS

## What are pods?

- Pod is a single instance of an application. 
- Smallest object that can be created in kubernetes. 
- Usually 1 pod = 1 container but sometimes multiple container run in the same pod to help each other. - e.g main app + helper for logging or metrics. 

## Key features:

- **Shared Network** - All containers in the same pod share the same IP and Ports. They can communicate via localhost. 
- **Shared Storage** - You can mount the same volumes to all containers   
- **Single Unit of Scheduling** - Kubernetes schedules pods onto nodes. 
- **Ephemeral** - Pods can be created, destroyed or moved - they are not permanent. 
- **Restart Behaviour** - If a pod dies it is not restarted - Kubernetes creates a new one which will have a new ID. 

# Example YAML

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
    - name: nginx
      image: nginx
      ports:
        - containerPort: 80
```

This pod runs one container using the nginx image, exposing port 80. 