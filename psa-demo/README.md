```bash
kubectl apply -f priv-ns.yaml

kubectl apply -f rest-ns.yaml

kubectl describe ns -l type=demo

kubens priv-ns

kubectl apply -f priv-pod.yaml

kubens rest-ns

kubectl apply -f priv-pod.yaml

kubectl apply -f unpriv-pod.yaml

kubectl get pods

kubectl logs psa-demo-pod-unpriv

kubectl apply -f unpriv-pod-cgr.yaml

kubectl get pods
```
