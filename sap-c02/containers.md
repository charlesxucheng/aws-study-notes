# ECS
* EC2 launch type: Can use Docker volumes, EFS and FSx (Windows)
* Fargate launch type: Only EFS

An ECS Container Instance is an EC2 instance running the ECS agent (worker node). A Task is a running container using settings in a Task Definition. A Service can control task count with auto scalling and attach an ELB.

IAM role permissions of the Container Instance (EC2) are supplied to the tasks (instances). Fargate only has IAM Task Roles.

## ECS Autoscaling
* Service autoscaling: Supports Target Tracking, Step and Scheduled scaling policies
* Cluster autoscaling: Uses a Capacity Provider ECS resource type associated with an EC2 ASG. Has container-aware EC2 instance termination.

# EKS
Supports AWS and on-prem deployments, hybrid deployments. Runs on EC2, Fargate and AWS Outposts. Across multiple AZs in the same region.

AWS Load Balancer Controller manages AWS ELBs for a Kubernetes Cluster. It is installed using Helm v3 or K8S manifest. 
It supports NLB and ALB. K8S Ingress -> ALB. K8S LoadBalancer type Service -> NLB. 
With LB Controller 2.3 or later, you can create NLBs using either instance targets or IP targets.

EKS Distro - a distro of K8S with the same dependencies as Amazon EKS. Allows running of K8S anywhere.

ECS Anywhere, EKS Anywhere - on customer-managed infra, including VMWare VSphere.

# Elastic Beanstalk
* Fully managed. Multi-AZ
* Auto created: EC2 ASG, ALB
* Can use EC2 or Docker containers on ECS
* Apps can have multiple versions stored on typically S3 buckets
* Versions can be applied to different Environments

## Deployment Policies
* All at once - down all then up all
* Rolling - down and update a batch of instances at a time
* Rolling with additional batch - up a batch of instances first then down the same number
* Immutable - A new ASG with all instances up before the old ASG is down, longest deployment, quick rollback in case of failures
* Blue/green - multiple versions co-exist based on weights (not a feature of Beanstalk, can use Route 53 to achieve this with a new staging environment.

# CICD
* CodePipeline: CodeCommit, CodeBuild, CodeDeploy (EC2s, Lambdas, containers)
* CodeStar: pre-configured CD toolchain for developing, building, testing and deploying on services such as EC2, Lambda, Beanstalk. Can use popular editors.
* CodeArtifact: artifact repo
* CodeGuru: Recommendations for improving app. Reviewer revuews Java and Python code. Secret detector. Profiler - runtime performance profiling.
* Cloud9: Cloud-based IDE

# App Runner
Fully managed service for deploying containerized we apps and APIs





