```bash
# Create our privileged namespace (allows all pods to run)
kubectl apply -f priv-ns.yaml

# Create our restricted namespace (enforces a number of best practices on pods being launched)
kubectl apply -f rest-ns.yaml

# View the namespace configurations - note the different labels which deternmine the security level
kubectl describe ns -l type=demo

# Switch into the privileged namespace
kubens priv-ns

# Launch our privileged pod (runs as root, requests additional capabilities)
kubectl apply -f priv-pod.yaml

# Switch into the  restricted namespace
kubens rest-ns

# Launch our privileged pod and review the errors
kubectl apply -f priv-pod.yaml

# View the differences between the privileged and unprivileged pod specifications
sdiff priv-pod.yaml unpriv-pod.yaml

# Launch our unprivileged pod
kubectl apply -f unpriv-pod.yaml

# Check whether the new pod is running
kubectl get pods

# Review the errors from the pod - nginx isn't able to start because the pod is no longer running as root
kubectl logs psa-demo-pod-unpriv

# Launch the unprivileged pod using the ChainGuard-provided nginx base image which does not require root
kubectl apply -f unpriv-pod-cgr.yaml

# Check that the new pod is able to start correctly
kubectl get pods
```
