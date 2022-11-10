```bash

# Create a namespace for the secrets demo
kubectl apply -f secrets-ns.yaml

# Switch into the  restricted namespace
kubens secrets-ns

# Now we need to install the Secret Store CSI driver into our cluster
helm repo add secrets-store-csi-driver https://kubernetes-sigs.github.io/secrets-store-csi-driver/charts
helm install csi-secrets-store secrets-store-csi-driver/secrets-store-csi-driver --namespace kube-system

# Install the AWS Secret and Config Provider plugin for the Secret Store CSI driver
curl https://raw.githubusercontent.com/aws/secrets-store-csi-driver-provider-aws/main/deployment/aws-provider-installer.yaml | kubectl apply -f -

# Create a secret in AWS Secrets Manager which we will mount into our container
aws secretsmanager create-secret --name ContainerDayDemoSecret --description "Secret for Container Day demo" --secret-string "Hello, Container Day\!"

# Create an IAM Service Account linked to an IAM role with access to the secret which will be assumed by the pod to access AWS Secrets Manager (in a real cluster you should create a policy scoped to the specific secret!)
eksctl create iamserviceaccount --name aws-node --namespace secrets-ns  --cluster container-day-demo --attach-policy-arn arn:aws:iam::aws:policy/SecretsManagerReadWrite --approve --override-existing-serviceaccounts

# Create the Secret Provider which references the secret in AWS Secrets Manager
kubectl apply -f secretProvider.yaml

# Run a new pod which uses the created Service Account to mount the secret into the pod filesystem
kubectl apply -f secretConsumer.yaml

# View the secret mounted inside the pod using exec and cat
kubectl exec -it nginx-secrets-store-inline -- cat /mnt/secrets-store/ContainerDayDemoSecret

```
