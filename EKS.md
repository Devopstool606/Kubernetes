# 💡 What is EKS?

EKS stands for Amazon Elastic Kubernetes Service.

It is:

A managed Kubernetes service by AWS.

AWS hosts and manages the Kubernetes control plane (like the API server, etcd, etc.).

You only manage and pay for the worker nodes (EC2 instances).

Makes it easier to run Kubernetes on AWS without setting up your own cluster from scratch.

# 💻 What is eksctl?

eksctl is a command-line tool to manage EKS clusters.

It helps you:

Create, update, and delete EKS clusters easily.

Add node groups (worker nodes).

Configure access and permissions.

Simplifies complex tasks into one command.

It’s like a shortcut tool for working with EKS.

# 🔁 How they relate:
Tool	                          Purpose
EKS                         	The Kubernetes service provided by AWS
eksctl	                      A CLI tool to manage your EKS clusters easily



![image](https://github.com/user-attachments/assets/4bcf1381-f2e3-4dd6-a7a6-9e6856a371fe)


eksctl create cluster --name=my-cluster --region=us-east-1


# Step-by-Step EKS Setup and Cleanup Guide

# 🛠️ 1. Install Prerequisites

# a. Install eksctl

     curl -LO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_Linux_amd64.tar.gz"
     tar -xzf eksctl_Linux_amd64.tar.gz
    sudo mv eksctl /usr/local/bin

# b. Install AWS CLI

    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
    sudo apt install unzip -y
    unzip awscliv2.zip
    sudo ./aws/install

# c. Install kubectl

     curl -LO "https://dl.k8s.io/release/$(curl -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
     chmod +x kubectl
     sudo mv kubectl /usr/local/bin/
     
# 🔐 2. Configure AWS Credentials

    aws configure
    
Enter your AWS Access Key, Secret Key, region (e.g. us-east-1), and output format.

# ☁️ 3. Create EKS Cluster (with node group)

    eksctl create cluster \
    --name=my-cluster \
    --region=us-east-1 \
    --nodegroup-name=my-nodes \
    --node-type=t3.medium \
    --nodes=2 \
    --nodes-min=2 \
    --nodes-max=3 \
    --managed

 ⏳ This may take 15–20 minutes. It provisions the control plane, VPC, networking, IAM roles, and worker nodes.

# 🔗 4. Connect to EKS Cluster

    aws eks --region us-east-1 update-kubeconfig --name my-cluster

Check context:

    kubectl config current-context

# 🧪 4. (Optional) Deploy a Test App

    kubectl create deployment hello-eks --image=nginx
    kubectl expose deployment hello-eks --type=LoadBalancer --port=80
    kubectl get svc

# 🧹. Cleanup – Delete Everything

# a. Delete the entire cluster and its resources:

    eksctl delete cluster --name=my-cluster --region=us-east-1

⛔ This deletes the control plane, node group, and all AWS resources created by eksctl.

