# Quick Demo for EKS Security Best Practices Talk for AWS Container Day 2022

To create the demo cluster;

```bash
$ eksctl create cluster -f eksctl-cluster.yaml
```

This will incur charges in your account, so be sure to delete the cluster when you've finished!

 ```bash
 $ eksctl eksctl delete cluster --name container-day-demo 
 ```

See the README.md file in each subfolder for demo instructions
