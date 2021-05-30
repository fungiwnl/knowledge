# ECS

- Elastic Container Service
- Launch Docker containers on AWS
- **You must provision & maintain the infrastructure (the EC2 instances)**
- AWS takes care of starting / stopping containers
- Has integrations with the Application Load Balancer

## Amazon EC2 launch types for ECS

- [Insert diagram]


## Fargate

- Launch Docker containers on AWS
- **You do not provision the infra (no EC2 instances to manage) - simpler!
- Serverless offering
- AWS just runs for you based on the CPU / RAM you need

### Fargate launch type for ECS

- [Insert diagram]


## IAM roles for ECS tasks 

- **ECS Instance Profile**
   - Used by the ECS agent
   - Make API calls to ECS service
   - Send container logs to CloudWatch logs
   - Pull Docker image from ECR
   - Reference sensitive data in Secrets Manager or SSM Parameter Store

- **ECS Task Role**
   - Allow each task to have a specific role
   - Use different roles for different ECS Services you run
   - Task Role is defined in the task definition

## ECS DataVolumes - EFS File Systems

- EC2 + EFS NFS
- Fategate tsks

- Works for both EC2 Tasks and Fategate tasks
- Ability ot mount EFS volumes onto tasks
- Tasks launched in any AZ will be able to share the same data in the EFS volume
- Fargate + ECS = seerverless + data storage without managing servers

- **Use case:** persisitent multi-AZ shared storage for your containers


## ECS Services and Tasks


## Load Balance for EC2 Launch Type

- We get a dynamic port mapping
- The ALB supports finding the right port on your EC2 instances
- **You must allow on the EC2 instance's security group **any port** from the ALB security group**

- [Insert diagram]

## Load Balancing for Fargate

- Each task has a **unique IP**
- You must allow on the ENI's security group the task port from the ALB security group

- [Insert diagram]

## ECS tasks invoked by Event Bridge

- TODO

## ECS Scaling - Service CPU Usage Example

- Autoscaling baed on CPU usage by setting a CloudWatch metric (ECS Service CPU usage)
- Trigger CloudWatch alarm to scale
- Works for EC2 launch type and Fargate
- Scale ECS Capacity Providers (optional)

## ECS Scaling - SQS Queue Example

- CloudWatch Metric (Queue Length)
- Trigger CloudWatch Alarm
- Scale
- Scale Capacity Providers (optional)

## ECS Rolling Updates

- When updating from v1 to v2, we can control how many tasks can be started and stopped, and in which order
- ECS Service update screen

- [Insert diagram]
