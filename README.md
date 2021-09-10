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


# Task

![alt text](https://github.com/ioanan11/SRE_monitoring/blob/main/Screenshot%202021-09-10%20115652.png)

## 1. Auto Scaling
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

### Step 2: Create an Auto Scaling Group

- Enter a valid name (SRE_ioana_auto_scaling_group)
- Network: pick the VPC and subnet you want to use (Default and Default 1a in this case)
- Insert min, max and desired capacity of the auto scaling group (min = 1, max = 3, desired = 1)
- (We would normally add notification with SNS)
- Create Auto Scaling Group  

Note: An EC2 instance should have been launched once we created the Auto Scaling Group
