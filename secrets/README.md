```bash
helm repo add secrets-store-csi-driver https://kubernetes-sigs.github.io/secrets-store-csi-driver/charts

helm install csi-secrets-store secrets-store-csi-driver/secrets-store-csi-driver --namespace kube-system

curl https://raw.githubusercontent.com/aws/secrets-store-csi-driver-provider-aws/main/deployment/aws-provider-installer.yaml | kubectl apply -f -

aws secretsmanager create-secret --name ContainerDayDemoSecret --description "Secret for Container Day demo" --secret-string "Hello, Container Day\!"

eksctl create iamserviceaccount --name aws-node --namespace default --cluster container-day-demo --attach-policy-arn arn:aws:iam::aws:policy/SecretsManagerReadWrite --approve --override-existing-serviceaccounts

kubectl apply -f secretProvider.yaml

kubectl apply -f secretConsumer.yaml

kubectl exec -it nginx-secrets-store-inline -- cat /mnt/secrets-store/ContainerDayDemoSecret

```
