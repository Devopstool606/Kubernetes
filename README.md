# Kubernetes

Kubernetes (often abbreviated as K8s) is an open-source container orchestration platform used to automate the deployment, scaling, and management of containerized applications. It was originally developed by Google and is now maintained by the Cloud Native Computing Foundation (CNCF).

# Key Features of Kubernetes

✅ Automated Deployment & Scaling – Deploy and scale applications based on demand.

✅ Load Balancing – Distributes network traffic across containers for high availability.

✅ Self-Healing – Automatically restarts failed containers and replaces unhealthy nodes.

✅ Service Discovery – Manages internal networking for container communication.

✅ Storage Orchestration – Manages storage dynamically for different workloads.

✅ Rolling Updates & Rollbacks – Updates applications without downtime.

Why Use Kubernetes?
-----------------------
Manages multiple containers efficiently.

Ensures high availability of applications.

Works well with microservices architecture.

Supports cloud-native applications and hybrid cloud environments.

Orchestration:
--------------

In Kubernetes (or Container Orchestration):
Orchestration refers to automating the deployment, scaling, networking, and management of containers. Instead of manually starting and stopping containers, Kubernetes does it for you.

Example:
--------
Imagine you have a web application with:

A frontend container (React or Angular)

A backend container (Node.js or Java)

A database container (MySQL or PostgreSQL)

Kubernetes orchestrates them by:
================================

✅ Ensuring they start in the right order.

✅ Keeping them running even if one crashes.

✅ Scaling them up/down based on traffic.

✅ Managing how they communicate with each other.


How Minikube Works Internally
--------------------------------
1. When you start Minikube (minikube start)

	○ It creates a virtual Kubernetes node (inside Docker, VM, or bare metal).

	○ It starts the Kubernetes control plane (API server, scheduler, etc.).

	○ It configures your kubectl to talk to this local cluster.

	2. When you deploy an app (kubectl create deployment ...)
    
		○ The API server inside Minikube schedules a pod to run inside its node.

		○ The pod pulls the container image (nginx, for example).

		○ The container starts running inside the Kubernetes cluster.

	4. If Minikube is stopped (minikube stop)
    
		○ The cluster shuts down, and your application stops running.

		○ Running kubectl get pods or kubectl get nodes will fail.

Conclusion
----------
✅ Minikube is the Kubernetes environment where your applications run.

✅ You must start Minikube before using kubectl to deploy or manage apps.

✅ If Minikube stops, your Kubernetes cluster stops. You need to restart Minikube to continue using Kubernetes.

Deploy Nginx on Minikube 🚀
-----------------------------
Since Minikube is a single-node Kubernetes cluster, let's deploy Nginx and expose it so that we can access it from outside.

Step 1: Start Minikube
-----------------------
Make sure Minikube is running before deploying anything:

    minikube start

You can verify the status

    minkube status

Step 2: Deploy Nginx
-----------------------

Run the following command to create a deployment named my-nginx using the official Nginx image:

    Kubectl create deployment mynginx --image=nginx

Check if the deployment is cerated

    Kubectl get deployments

Check if the pod is running

    Kubectl get pods

Step 3: Expose the Deployment

    kubectl expose deployment my-nginx --type=NodePort --port=80

Check services

    kubectl get services

Step 4: Access Nginx in Minikube

Minikube provides a command to open the exposed service in a browser:

     minikube service my-nginx
Or 
Get the URL manually 

    minikube service my-nginx --url

Step 5: Cleanup (Optional)

If you want to delete the deployment and service:

    kubectl delete deployment my-nginx
    kubectl delete service my-nginx

Different Objects in the Kubernets
=========================================

![image](https://github.com/user-attachments/assets/13017a6c-9c09-46bb-bc46-1c7995d8a5e0)

A manifest file in Kubernetes is a YAML or JSON file that defines the desired state of a Kubernetes resource, such as Pods, Deployments, Services, ConfigMaps, etc. It is used to tell Kubernetes how to create and manage resources.

YAML is a human-readable data format that is often used for configuration files, including Kubernetes manifests. Let me give you a quick introduction. 🚀

📝 YAML Basics
-------------------
YAML (Yet Another Markup Language) follows a few simple rules:

1. Uses indentation (spaces, not tabs) for structure.
	
2. Key-value pairs are separated by :.
	
3. Lists use - (dash) for items.

🔹 Example 1: Key-Value Pairs

![image](https://github.com/user-attachments/assets/00e91c15-35fc-4fa2-a1fc-ced5d902df55)

![image](https://github.com/user-attachments/assets/09e53ae7-bb72-43e4-8b26-91c03dbffbb3)

![image](https://github.com/user-attachments/assets/00dbf8bf-61c6-496e-ad53-e1fe375ed367)

![image](https://github.com/user-attachments/assets/3419e481-0b0f-46c4-b89a-9b26ad30b9e7)






✅ Breakdown:
	• apiVersion: v1 → API version
	• kind: Pod → Type of resource
	• metadata.name: my-pod → Pod name
	• spec.containers → Defines container details
	• image: nginx:latest → Container image
	• ports.containerPort: 80 → Exposes port 80



Cluster and node management

kubectl get nodes                 # List all nodes in the cluster  
kubectl get namespaces            # List all namespaces  
kubectl config view               # View current Kubernetes config  
kubectl cluster-info              # Display cluster info  
kubectl describe node <node-name> # Detailed info about a specific node 


Pods management
========================================
kubectl get pods                   # List all pods in the default namespace  
kubectl get pods -A                # List all pods in all namespaces  
kubectl get pods -n <namespace>    # List pods in a specific namespace  
kubectl describe pod <pod-name>    # Get detailed info about a specific pod  
kubectl logs <pod-name>            # View logs of a pod  
kubectl exec -it <pod-name> -- /bin/sh  # Access a pod interactively  
kubectl delete pod <pod-name>      # Delete a pod  


Deployment management
==================================
kubectl create deployment my-nginx --image=nginx  # Create a deployment  
kubectl get deployments                           # List all deployments  
kubectl describe deployment <deployment-name>     # Detailed info about deployment  
kubectl delete deployment <deployment-name>       # Delete a deployment  


Minikube specific commands
=====================================
minikube start                 # Start Minikube  
minikube stop                  # Stop Minikube  
minikube delete                # Delete Minikube cluster  
minikube status                # Check Minikube status  
minikube dashboard             # Open Minikube dashboard  


1. Deployment (Managing Pods)
   -------------------------

A Deployment is responsible for managing and scaling Pods (which run containers). It ensures that a specified number of replicas of an application are always running and handles updates smoothly.

🔹 Why Use a Deployment?
----------------------------
Ensures high availability by maintaining multiple replicas.

Allows rolling updates and rollbacks.

Handles self-healing (if a Pod crashes, it restarts).

2. Service (Exposing Applications)
   --------------------------------
   
A Service exposes a set of Pods to the network. Since Pods have dynamic IPs, a Service provides a stable way to access them.

🔹 Why Use a Service?
=============================
Provides a fixed IP/hostname for Pods.

Balances traffic across multiple Pods.

Supports different access types (ClusterIP, NodePort, LoadBalancer).

![image](https://github.com/user-attachments/assets/e80813be-2e72-4583-b8c9-8ca8ea804304)
