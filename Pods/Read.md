# Why Can't You Deploy a Container Directly in Kubernetes?

# ✅ Key Reasons

1️⃣ Pods provide abstraction – Pods wrap containers and handle networking, storage, and lifecycle.

2️⃣ Multi-container support – Pods allow multiple containers to share resources.

3️⃣ Scaling & orchestration – Kubernetes manages and scales Pods, not individual containers.

4️⃣ Standard deployment model – Everything in Kubernetes is managed as a Pod for consistency.

💡 Even for a single container, you must wrap it inside a Pod.

# Deploy Your First Application in Kubernetes

We’re deploying a simple Nginx web server using a YAML file.

# Step 1: Create the Pod YAML file Pod.yaml

# 💻 Step 2: Deploy the Pod

      kubectl apply -f nginx-pod.yaml

  This creates a Pod using the public nginx image.

# 🔍 Step 3: Check Pod Status

       kubectl get pods

       kubectl describe pod nginx-pod

       kubectl logs nginx-pod

# 🌐 Step 4: Expose the Pod (Optional)

  To access the Pod from outside, expose it using a Service:

       kubectl expose pod nginx-pod --type=NodePort --port=80
     
        kubectl get svc

# How to delete single pod

       kubectl delete pod <pod name>

# Delete All Pods in the Current Namespace

    kubectl delete pods --all

#  Watch Pods in real-time

    kubectl get pods -w
    
#  Get detailed info about a Pod

    kubectl describe pod <pod name>

#  List Pods in all namespaces

    kubectl get pods --all-namespaces

# 🗂️ What is a Namespace in Kubernetes?

A Namespace is like a virtual cluster inside your main Kubernetes cluster.

It helps you organize and separate resources like Pods, Services, Deployments, etc., within the same cluster.

📦 Think of it like:

A folder in your computer that keeps related files grouped.

Or, separate workspaces for different teams or environments.

# ✅ Why Namespaces are useful:

1️⃣ Environment separation – dev, test, staging, prod

2️⃣ Team isolation – frontend team vs backend team

3️⃣ Avoid name conflicts – same resource names can exist in different namespaces

4️⃣ Access control – apply RBAC (permissions) per namespace

# 📋 Common Built-in Namespaces:

# Namespace	                                                Purpose

default---------->                                                      Where resources go if no namespace is given

kube-system------->	                                                  Core Kubernetes components (DNS, scheduler)

kube-public ------>	                                                  Readable by all users, even unauthenticated

kube-node-lease ------>                                                    Node heartbeats
