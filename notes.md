# Installation (Win)
- `scoop install kind kubectl helm aws`
- Install Docker Desktop
- Create Kind Cluster

  ```kind create cluster```
- Install Crossplane 
  ```
  kubectl create namespace crossplane-system
  helm repo add crossplane-stable https://charts.crossplane.io/stable
  helm repo update
  helm install crossplane --namespace crossplane-system crossplane-stable/crossplane

  helm list -n crossplane-system
  kubectl get all -n crossplane-system
  ```
  Validate (make sure crossplane and rbac-manager deployment/pods are healthy)
  ```
  kc get all -n crossplane-system
  ```
- Install aws provider
  ```
  kubectl apply -f provider-aws
  ```
  Wait for provider install to finish
  ```
  kubectl get provider -w
  ```
- Configure AWS credentials
  ```
  kubectl create secret generic aws-creds -n crossplane-system --from-file=creds=~/.aws/credentials
  kubectl apply -f providerconfig-aws.yaml
  ``` 
 
- Create Bucket 
  ```
  kubectl apply -f s3-bucket.yaml
  kubectl get bucket -w
  ```
  

- Kubectl crossplane plugin
  - Download crank.exe from https://releases.crossplane.io/stable/current/bin/windows_amd64/
  - Rename to `kubectl-crossplane.exe` and save in a folder on `PATH`
