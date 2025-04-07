# How will you upgrade your EKS kubernetes cluster:

Prequesites:

1. Cordon the nodes(unschedule the nodes)
2. make sure control plane and nodes are same with the kubernetes version
3. Go through the release notes
4. Lower enviornment(test)
5. You can't downgrade once upgraded(you have to freshley install everything)
6. If you are using Cluster auto scalar then make sure it should matches the control plane version
7. You should have five available ip address within the subnet provided during kubernetes cluster creation
   
You should ekctl on your system:
# Create EKS Cluster

eksctl create cluster --name=observability \
                      --region=us-east-1 \
                      --zones=us-east-1a,us-east-1b \
                      --without-nodegroup
                  
eksctl utils associate-iam-oidc-provider \
    --region us-east-1 \
    --cluster observability \
    --approve
   
eksctl create nodegroup --cluster=observability \
                        --region=us-east-1 \
                        --name=observability-ng-private \
                        --node-type=t3.medium \
                        --nodes-min=2 \
                        --nodes-max=3 \
                        --node-volume-size=20 \
                        --managed \
                        --asg-access \
                        --external-dns-access \
                        --full-ecr-access \
                        --appmesh-access \
                        --alb-ingress-access \
                        --node-private-networking

# Update ./kube/config file
     aws eks update-kubeconfig --name observability


# to update latest version

     eksctl upgrade cluster --name observability --region ap-southeast-1 --version 1.33 --approve


# Delete the EKS Cluster 
     eksctl delete cluster --name observability

Useful links: https://docs.aws.amazon.com/eks/latest/userguide/update-cluster.html
