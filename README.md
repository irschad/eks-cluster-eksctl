# Create EKS Cluster with eksctl

## Project Overview

This project demonstrates how to create and manage an Amazon Elastic Kubernetes Service (EKS) cluster using `eksctl`, a powerful command-line tool. By leveraging `eksctl`, we simplify the manual effort involved in setting up EKS clusters and gain an efficient, reproducible way to manage Kubernetes infrastructure on AWS.

## Technologies Used

- **Kubernetes**: Container orchestration platform for managing applications.
- **AWS EKS**: Managed Kubernetes service by Amazon Web Services.
- **eksctl**: Command-line tool for EKS cluster creation and management.
- **Linux**: Operating system used for this project setup.

---

## Installation and Setup

### 1. Install eksctl
Follow these steps to install `eksctl` on a Linux system:

1. Download and install `eksctl`:
   ```bash
   curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
   sudo mv /tmp/eksctl /usr/local/bin
   ```
2. Verify the installation:
   ```bash
   eksctl version
   ```

### 2. Configure AWS Credentials
Before using `eksctl`, ensure your AWS account is properly configured:

1. Use `aws configure` to set your AWS credentials and default region:
   ```bash
   aws configure
   ```
   Alternatively, verify existing credentials:
   ```bash
   aws configure list
   ```

---

## Steps to Create an EKS Cluster

### 1. Create the EKS Cluster
Run the following `eksctl` command to create a new EKS cluster:

```bash
eksctl create cluster \
--name demo-cluster \
--version 1.31 \
--region us-east-1 \
--nodegroup-name demo-nodes \
--node-type t2.micro \
--nodes 2 \
--nodes-min 1 \
--nodes-max 3
```

- **Cluster Name**: `demo-cluster`
- **Kubernetes Version**: `1.31`
- **Region**: `us-east-1`
- **Node Group Name**: `demo-nodes`
- **Instance Type**: `t2.micro`
- **Number of Nodes**: 2 (scales between 1 and 3)

### 2. Validate the Cluster
Once the cluster is created, verify its status and configuration:

1. Check the nodes in the cluster:
   ```bash
   kubectl get nodes
   ```
   Expected output: Two nodes (as specified during cluster creation).

2. Check the default namespace for pods:
   ```bash
   kubectl get pod
   ```
   Expected output: No resources found (no pods deployed yet).

---

## Exploring AWS Resources

After creating the cluster, explore the associated AWS resources:

1. **IAM Roles**:  
   - Navigate to the IAM console and verify the roles created by `eksctl`.
   - Check the permissions associated with these roles.

2. **VPC Configuration**:  
   - Open the VPC console and filter resources by `eksctl`.
   - Review the public and private subnets created for the cluster.

3. **EKS Console**:  
   - Go to the EKS page and locate the cluster `demo-cluster`.
   - Review the cluster's configuration, including:
     - **Compute**: Shows the nodes and node groups.
     - **Workloads**: Displays system processes like `coredns`, `aws-node`, and `kube-proxy`.

4. **EC2 Instances**:  
   - Check the EC2 console for the instances corresponding to the worker nodes.

5. **EKS API Endpoint**:  
   - View the API server endpoint in the EKS console's overview tab.

---

## Notes and Observations

- The EKS control plane is managed by AWS and does not appear as instances in the EC2 console.
- Worker nodes are visible in both the EKS and EC2 consoles.
- System workloads (`coredns`, `aws-node`, and `kube-proxy`) are automatically deployed on the worker nodes.

---

## Conclusion

By using `eksctl`, creating and managing an EKS cluster becomes a streamlined and efficient process. This approach minimizes manual effort, ensures consistency, and leverages AWS’s fully managed Kubernetes service for robust container orchestration.

For further customizations, refer to the [eksctl documentation](https://eksctl.io/). Also, explore customizing cluster by using a config file:
```bash
eksctl create cluster -f cluster.yaml
```

