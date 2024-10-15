# Provision an EKS Cluster with Terraform

Based on [Provision an EKS Cluster tutorial](https://developer.hashicorp.com/terraform/tutorials/kubernetes/eks)

```
terraform init
terraform apply

terraform output

# To configure kubectl to use the new cluster:
aws eks --region $(terraform output -raw region) update-kubeconfig \
    --name $(terraform output -raw cluster_name)

kubectl cluster-info
kubectl get all
```
