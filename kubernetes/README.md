# Kubernetes

## Creating your kubernetes cluster

```
# IAM User
export AWS_ACCESS_KEY_ID=<>
export AWS_SECRET_ACCESS_KEY=<>
export AWS_DEFAULT_REGION=AWS_REGION

export KOPS_STATE_STORE=BUCKET_NAME
export KOPS_CLUSTER_NAME=pizza.k8s.local

aws s3api create-bucket --bucket $KOPS_STATE_STORE --create-bucket-configuration LocationConstraint=us-west-2 --region us-west-2
aws s3api put-bucket-versioning --bucket $KOPS_STATE_STORE --region us-west-2  --versioning-configuration Status=Enabled


kops create cluster \
--zones "us-west-2a" \
--master-count 1 \
--master-size=t3.medium \
--node-count 1 \
--node-size=t2.micro \
--dry-run \
-oyaml > cluster.yaml

kops update cluster --name pizza.k8s.local --yes --admin


* list clusters with: kops get cluster
* edit this cluster with: kops edit cluster pizza.k8s.local
* edit your node instance group: kops edit ig --name=pizza.k8s.local nodes-us-west-2a
* edit your master instance group: kops edit ig --name=pizza.k8s.local master-us-west-2a

mkdir -p ~/pizza
touch ~/pizza/config
export KUBECONFIG=~/pizza/config
kops export kubecfg --name pizza.k8s.local  --admin



export AWS_ACCESS_KEY_ID=AKIA2XXXXXXQH2W5U
export AWS_SECRET_ACCESS_KEY=AKIA2XXXXXXQH2W5U
export AWS_DEFAULT_REGION=us-west-2
export KUBECONFIG=~/pizza/config
export KOPS_STATE_STORE=s3://pizza-kops-bucket
export KOPS_CLUSTER_NAME=pizza.k8s.local
```