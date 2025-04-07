# What is a Namespace in Kubernetes?

A namespace in Kubernetes is like a virtual cluster inside your actual Kubernetes cluster. It helps you organize, isolate, and manage resources (pods, services, deployments, etc.) more effectively.

# 📦 Why are Namespaces Needed?

Here’s why namespaces are useful:

# 1. Multi-Tenancy / Separation of Teams or Projects

Example: You can have dev, qa, and prod namespaces.

Each team/project can manage their resources without stepping on each other’s toes.

# 2. Resource Isolation

You can set resource limits (CPU/memory) per namespace.

This avoids one team hogging all resources.

# 3. Avoid Naming Conflicts

You can have a pod named web-app in both dev and prod.

Same name, but isolated by namespace.

# 4. Access Control (RBAC)

You can give specific teams or users access to certain namespaces.

Improves security and control.

# 5. Cleaner Organization

Helps manage large clusters by logically grouping related workloads.

# ✅ Option 1: Using kubectl with --namespace

       kubectl create namespace <your-namespace-name>

# create the deployment in specific namespace

    kubectl apply -f your-deployment.yaml --namespace=<namespace-name>

# Get the pods or deployments

    kubectl get pods --namespace=myname-space

    kubectl get pods --namespace=my-namespace

# to delete all pods in namespace

     kubectl delete pods --all -n <namespace-name>
    
This will show only the pods inside the monitoring namespace — like your Prometheus pods.

# ✅ Option 2: Define Namespace Inside the YAML File\

In your YAML file, add the namespace field under metadata like this:

![image](https://github.com/user-attachments/assets/a763593a-4b1d-48bd-a796-279916f9d349)

# Option 3: Change the Current Namespace Context (Not recommended for short tasks)

    kubectl config set-context --current --namespace=<namespace-name>

# To reset your current context to the default namespace, simply run:

    kubectl config set-context --current --namespace=default





