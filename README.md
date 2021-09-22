# Monitoring with Amazon CloudWatch

## What is Amazon CloudWatch?

Amazon CloudWatch is a monitoring and observability service built for DevOps engineers, developers, site reliability engineers (SREs), and IT managers. CloudWatch provides you with data and actionable insights to monitor your applications, respond to system-wide performance changes, optimize resource utilization, and get a unified view of operational health. CloudWatch collects monitoring and operational data in the form of logs, metrics, and events, providing you with a unified view of AWS resources, applications, and services that run on AWS and on-premises servers. You can use CloudWatch to detect anomalous behavior in your environments, set alarms, visualize logs and metrics side by side, take automated actions, troubleshoot issues, and discover insights to keep your applications
running smoothly.

## Benefits

- Observability on a single platform across applications and infrastructure
- Easiest way to collect metrics in AWS and on-premises
- Improve operational performance and resource optimization
- Get operational visibility and insight
- Derive actionable insights from logs

## How it works

![alt text](https://github.com/ioanan11/SRE_monitoring/blob/main/Screenshot%202021-09-10%20120436.png)

## Use cases 

- Infrastructure monitoring and troubleshooting
- Mean-time-to-resolution improvement
- Proactive resource optimization
- Application monitoring
- Log analytics



# Load Balancing and Auto Scaling

## Amazon Application Load Balancer

Elastic Load Balancing automatically distributes your incoming traffic across multiple targets, such as EC2 instances, containers, and IP addresses, in one or more Availability Zones. It monitors the health of its registered targets, and routes traffic only to the healthy targets. Elastic Load Balancing scales your load balancer as your incoming traffic changes over time. It can automatically scale to the vast majority of workloads.

![alt text](https://github.com/ioanan11/SRE_monitoring/blob/main/Screenshot%202021-09-10%20121736.png)

## Amazon EC2 Auto Scaling

Amazon EC2 Auto Scaling helps you ensure that you have the correct number of Amazon EC2 instances available to handle the load for your application. You create collections of EC2 instances, called Auto Scaling groups. You can specify the minimum number of instances in each Auto Scaling group, and Amazon EC2 Auto Scaling ensures that your group never goes below this size. You can specify the maximum number of instances in each Auto Scaling group, and Amazon EC2 Auto Scaling ensures that your group never goes above this size. If you specify the desired capacity, either when you create the group or at any time thereafter, Amazon EC2 Auto Scaling ensures that your group has this many instances. If you specify scaling policies, then Amazon EC2 Auto Scaling can launch or terminate instances as demand on your application increases or decreases.

![alt text](https://github.com/ioanan11/SRE_monitoring/blob/main/Screenshot%202021-09-10%20121434.png)

We can scale **up**, **down**, **out** and **in**.

Scaling up is when you change the instance types within your Auto Scaling Group to a higher type (for example: changing an instance from a m4.large to a m4.xlarge), scaling down is to do the reverse.

Scaling out is when you add more instances to your Auto Scaling Group and scaling in is when you reduce the number of instances in your Auto Scaling Group.


# Amazon SNS
Amazon Simple Notification Service (Amazon SNS) is a fully managed messaging service for both application-to-application (A2A) and application-to-person (A2P) communication.

![alt text](https://github.com/ioanan11/SRE_monitoring/blob/main/Product-page-diagram-Amazon-SNS_event-driven-SNS-compute%402X_.4b9c0a75aa40bda9cdb12f0176930a12da2872bf.png)

Benefts:

- managed service: you don't have to run or maintain it
- instantaneous delivery: it is a very simple service to use as Web-based AWS Management Console offers the effortlessness of the point-and-click interface
- ease of use 

# Amazon SQS

![alt text](https://github.com/ioanan11/SRE_monitoring/blob/main/Diagram2.png)

# Task: Using CloudWatch with our app

![alt text](https://github.com/ioanan11/SRE_monitoring/blob/main/Screenshot%202021-09-10%20115652.png)

## 1. Autoscaling and Load Balancing
### Step 1: Create a launch template

- On AWS EC2: Launch Templates -> Create Launch Template 
(Note: the resources you create for auto scaling will be related strictly to the region you create them on)
- Enter a valid name (ioana_template_auto_scaling)
- Tick the box under Auto Scaling guidance
- For AMI choose Amazon Linux 2 AMI (HVM), SSD
- Instance type: t2 micro
- Network Settings: VPC
- Choose a SG (ioana_app_SG in this case)
- Create launch template -> Create Auto Scaling Group

### Step 2: Create an Auto Scaling Group (ASG)

- Enter a valid name (SRE_ioana_auto_scaling_group)
- Network: pick the VPC and subnet you want to use (Default and Default 1a in this case)
- Insert min, max and desired capacity of the auto scaling group (min = 1, max = 3, desired = 1)
- (We would normally add notification with SNS)
- Create Auto Scaling Group  

**Note: An EC2 instance should have been launched once we created the Auto Scaling Group. This instance will be running as long as the ASG exists.**

### Step 3: Create a Load Balancer (LB)

- On AWS EC2: `Load Balancer` -> `Create Load Balancer`
- Select `Application Load Balancer` and name it
- Has to be `Internet Facing` + `IPv4`
- Default VPC -> all 3 subnets
- Select (or create) target group

	#### Target group setup
	- target type: Instances
	- name it
	- HTTP and port 80
	- register targets: select the instances associated with ASG

## 2. Scaling policies

- `From EC2 -> Auto Scaling groups` select your ASG and go to automatic scaling.  
- Create dynamic scaling policy
- there are 3 types: target tracking, step and simple. 

![alt text](https://github.com/ioanan11/SRE_monitoring/blob/main/Screenshot%202021-09-22%20125638.png)

### What are we monitoring?

- **Resource Monitoring**: how the servers are running (CPU load, disk space, RAM etc.)
- **Network Monitoring**: 
- **Application Performance Monitoring**
- **Third-party component Monitoring**


## 3. Cloud Watch Alarms


**Note: everything we have done manually can be automated using Terraform. Please have a look at this repo: https://github.com/ioanan11/sre_terraform**

# How everything works

![alt text]()
