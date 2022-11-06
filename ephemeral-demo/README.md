```bash
kubectl apply -f ephemeral-demo.yaml

kubens ephemeral-demo

kubectl apply -f pauseDeployment.yaml

kubectl get pods

kubectl exec -it pause-deployment-ID -- sh # this should fail

kubectl debug -it pause-deployment-ID --image=busybox:latest \
--target=pause # this should work
```
