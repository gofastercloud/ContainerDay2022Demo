```bash
kubectl apply -f ephemeral-demo.yaml

kubens ephemeral-demo

kubectl apply -f pause.yaml

kubectl get pods

kubectl exec -it pause -- sh # this should fail

kubectl debug -it pause --image=busybox:latest \
--target=pause # this should work
```
