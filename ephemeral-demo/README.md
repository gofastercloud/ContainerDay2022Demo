```bash

# Create a namespace for the Ephemeral Container demo
kubectl apply -f ephemeral-demo.yaml

# Switch to the new namespace
kubens ephemeral-demo

# Launch a Pod from the Kubernetes 'pause' image
kubectl apply -f pause.yaml

# View the running pod
kubectl get pods

# Exec into the Pod and attempt to run an interactive shell
kubectl exec -it pause -- sh # this should fail because the 'pause' container doesn't contain a shell environment

# Attach a Busybox container to the running Pod using 'kubectl debug' to get a shell
kubectl debug -it pause --image=busybox:latest --target=pause # this should give you a working shell environment

# View the process list to see the 'pause' process
ps
```
