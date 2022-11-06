```bash
kubectl exec -it pause-deployment-5df97c5fff-j2gkf -- sh # this should fail

kubectl debug -it pause-deployment-ID --image=busybox:latest \
--target=pause # this should work
```
