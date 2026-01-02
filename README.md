Cloud-Native 2048 Game Deployment on AWS EKS

This project demonstrates deploying a containerized 2048 web game on Amazon EKS using AWS Fargate and exposing it to the internet via AWS Application Load Balancer (ALB) using the AWS Load Balancer Controller.

🚀Tech Stack
- Amazon EKS (Fargate)
- AWS Load Balancer Controller
- Kubernetes (Deployment, Service, Ingress)
- AWS ALB
- Docker (prebuilt image)



🏗 Architecture Overview
1. Amazon EKS cluster created using eksctl with Fargate
2. AWS Load Balancer Controller installed using Helm
3. Kubernetes Deployment runs the 2048 game container
4. Kubernetes Service exposes the pods internally
5. Ingress resource creates an internet-facing ALB
6. ALB routes external traffic to pods running on Fargate



📦 Setup Steps

1 Create EKS Cluster
eksctl create cluster --name demo-cluster --region us-east-1 --fargate

2 Configure IAM OIDC Provider

eksctl utils associate-iam-oidc-provider --cluster demo-cluster --approve

3 Install AWS Load Balancer Controller
    Create IAM policy
    Create IAM role and service account
    Install controller using Helm

helm install aws-load-balancer-controller eks/aws-load-balancer-controller \
-n kube-system \
--set clusterName=demo-cluster \
--set serviceAccount.create=false \
--set serviceAccount.name=aws-load-balancer-controller

4 Deploy Application
kubectl apply -f manifests/



2048 Game Running (Public ALB URL)
[2048 App Running](2048-app-running.png)

☸️ EKS Cluster Status (Active)
[EKS Cluster Active](eks-cluster-active.png)

📋 EKS Cluster Details
[Cluster Details](cluster-details.png)

🌐 Cluster Networking & OIDC Configuration
[Cluster Networking](cluster-networking.png)

⚙️ AWS Load Balancer Controller Pods
[ALB Controller Pods](alb-controller-pods.png)

🌐 Application Load Balancer Created Automatically
[ALB Created](alb-created.png)
