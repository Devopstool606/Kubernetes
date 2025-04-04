# Difference b/w Conatiner, Pod, Deployment

![image](https://github.com/user-attachments/assets/8181e314-5f16-4f48-85da-7cae50b10ffb)

# 📦 What is a Deployment?

A Deployment is a Kubernetes object that:

✅ Manages ReplicaSets (which manage Pods)

✅ Makes sure a specific number of Pods are running

✅ Allows scaling, rolling updates, and rollbacks

✅ Automatically recreates Pods if they fail

🔁 Think of Deployment as a manager for your application pods.


# 🛠️ Commands Related to Deployments

# ✅ 1. Create Deployment from YAML

     kubectl apply -f deployment.yaml

# ✅ 2. Create Deployment using CLI

    kubectl create deployment nginx-deploy --image=nginx

# ✅ 3. List all Deployments

    kubectl get deployments

# ✅ 4. Describe a Deployment

    kubectl describe deployment nginx-deploy

# ✅ 5. Scale a Deployment

    kubectl scale deployment nginx-deploy --replicas=4

# ✅ 6. Update the Image (Rolling Update)

    kubectl set image deployment/nginx-deploy nginx=nginx:1.16

# ✅ 7. Rollback to Previous Version

    kubectl rollout undo deployment nginx-deploy

# ✅ 8. Check Rollout Status

     kubectl rollout status deployment nginx-deploy

# ✅ 9. Delete a Deployment

    kubectl delete deployment nginx-deploy

# 🧠 Key Notes:

replicas: Number of pods you want running.

selector: Tells Deployment which pods it manages (must match labels).

template: Blueprint to create new pods.

Rolling Updates: Done automatically when image/version changes.

Self-healing: If a pod dies, Deployment ensures another is created.

# 📈 Real-World Scenario:

You have a Node.js app and want 3 instances always running, with automatic updates and restarts. You’ll use a Deployment with:

replicas: 3

Your Node.js Docker image

A service to expose the pods


