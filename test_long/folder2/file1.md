# AWS

## Container Orchestration Tools

> Container Orchestration Tools = Managing, scaling and deploying containers

- Docker Swarm
- Kubernetes
- Mesos
- Nomad
- ECS(AWS Elastic Container Service)

## What is ECS?

- Container Orchestration Service
- Manages the whole container lifecycle(start, re-schedule, load balance)

### How does ECS work?
 
![ecs1](./images/ecs1.png)

Where are these containers hosted?

> ECS hosted onEC2 Instances

![ecs2](./images/ecs2.png)

 But you still have to do:
 - [x] Create EC2 instances
 - [x] Join to ECS cluster
 - [x] Check resources
 - [x] Manage Operating System
 - [x] Docker Runtime, ECS Agent

## ECS with AWS Fargate

If you want AWS to manage both **Container Orchestration** and **Infrastructure Management**, here is AWS Fargate.

- Serverless way to launch containers

> Tell AWS, Here is my container, please run it.

Pros:
- [x] No need to provision and manage servers. 
- [x] on demand
- [x] Only the infrastructure resources needed to run your containers
- [x] pay only for what you use
- [x] Easily scales up/down without fixed resources defined before hand 

EC2 Instance Pricing: Pay for whole Server.

Fargate Pricing: How long and how much capacity.

## EKS (Elastic Kubernetes Service)

What if you want to use Kubernetes?

> Thankfully, AWS has EKS which manages Kubernetes cluster on AWS infrastructure.

Pros:
- [x] Easier to migrate to another platform. e.g. Google Cloud, MS Azure
- [x] Kubernetes is open-source
- [x] Large community 

![ecs3](./images/ecs3.png)

## Command

### eksctl

#### Create cluster
```bash
eksctl create cluster \
--name kf-demo \
--version 1.19 \
--region us-east-2 \
--with-oidc \
--ssh-access \
--ssh-public-key aws-hictc-kfserving-key \
--nodes 1 \
--node-type m5.large \
--node-volume-size=20 \
--managed
```

#### Delete cluster

Delete whole cluster
```bash
eksctl delete cluster --name=kf-demo --region=us-east-2
```

Delete a nodegroup separately using `eksctl delete nodegroup`

```bash
# List EKS Clusters
eksctl get clusters

# Capture Node Group name
eksctl get nodegroup --cluster=<clusterName>
eksctl get nodegroup --cluster=eksdemo1

# Delete Node Group
eksctl delete nodegroup --cluster=<clusterName> --name=<nodegroupName>
eksctl delete nodegroup --cluster=eksdemo1 --name=eksdemo1-ng-public1
```

[more](https://www.stacksimplify.com/aws-eks/eks-cluster/delete-eks-cluster-nodegroup/)

