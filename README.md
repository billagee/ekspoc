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

# To deploy nginx and create an ELB pointing to it:
kubectl apply -f manifests/nginx-deployment.yaml

kubectl get svc nginx-service

# Look for EXTERNAL-IP:
NAME            TYPE           CLUSTER-IP       EXTERNAL-IP                        PORT(S)        AGE
nginx-service   LoadBalancer   xxx.xx.xx.xxx    xxxx.us-east-2.elb.amazonaws.com   80:30749/TCP   13s

# Test it:
THEHOST=$(kubectl get svc nginx-service --template='{{(index .status.loadBalancer.ingress 0).hostname}}')
curl ${THEHOST}

# Exec a shell:
kubectl exec -it nginx-< tab autocomplete the pod name > -- /bin/sh
```
