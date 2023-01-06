# Installing Kubernetes on EKS

## Prerequisites

- An AWS account
- The AWS CLI installed and configured on your local machine
- kubectl installed on your local machine
aws-iam-authenticator installed on your local machine
## Step 1: Create an EKS cluster

Use the following AWS CLI command to create an EKS cluster, replacing `CLUSTER_NAME` and `REGION` with your desired cluster name and region:

```
aws eks create-cluster --name CLUSTER_NAME --region REGION
```

This command will create a new VPC and all the necessary resources for the EKS cluster. It may take a few minutes for the cluster to be created.

## Step 2: Configure kubectl

Use the following AWS CLI command to retrieve the cluster's endpoint and certificate data, replacing `CLUSTER_NAME` and `REGION` with your cluster name and region:

```
aws eks describe-cluster --name CLUSTER_NAME --region REGION
```
Copy the `endpoint` and `certificate-authority-data` values from the output.

Use the following command to create a `kubeconfig` file for the cluster, replacing `ENDPOINT` and `CERTIFICATE_AUTHORITY_DATA` with the values you copied and `CLUSTER_NAME` with your cluster name:

```
aws eks update-kubeconfig --name CLUSTER_NAME --region REGION --kubeconfig ~/.kube/config --endpoint-url ENDPOINT --certificate-authority-data CERTIFICATE_AUTHORITY_DATA
```
This will update the `kubeconfig` file with the necessary information to access the EKS cluster.

## Step 3: Create an IAM role for the worker nodes

Use the following AWS CLI command to create an IAM role for the worker nodes, replacing ROLE_NAME with your desired role name:

```
aws iam create-role --role-name ROLE_NAME --assume-role-policy-document file://trust-policy.json
```
Replace the contents of trust-policy.json with the following:

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "ec2.amazonaws.com"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

This policy allows EC2 instances to assume the role.

Use the following AWS CLI command to attach the `AmazonEKSWorkerNodePolicy` policy to the IAM role:

```
aws iam attach-role-policy --role-name ROLE_NAME --policy-arn arn:aws:iam::aws:policy/AmazonEKSWorkerNodePolicy
```
## Step 4: Create a worker node group

Use the following AWS CLI command to create a worker node group, replacing `CLUSTER_NAME` with your cluster