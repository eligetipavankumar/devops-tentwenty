# devops-tentwenty
assignment of tentwenty goa
# DevOps Hello World on AWS

## 1. Project Overview

This project demonstrates a simple **Hello World web application** deployed on AWS using core DevOps and cloud infrastructure concepts. The solution follows AWS best practices by placing application servers in private subnets and exposing them securely via an Application Load Balancer.

The goal is to showcase understanding of:

* AWS networking (VPC, subnets, routing)
* Compute (EC2)
* Load balancing (ALB)
* Security (security groups, least privilege)
* Automation (EC2 user-data)

---

## 2. Architecture Diagram

Designed a architecture with drwa.io. That is a architecture.png

**Traffic Flow:**
Internet → Application Load Balancer (Public Subnets) → EC2 Instances (Private Subnets)

---

## 3. AWS Resources Created

### Networking

* VPC (10.0.0.0/16)
* 2 Public Subnets (across 2 Availability Zones)
* 2 Private Subnets (across 2 Availability Zones)
* Internet Gateway
* NAT Gateway
* Route Tables (public and private)

### Compute

* 2 EC2 instances (t2.micro)
* Amazon Linux 2023 AMI
* Instances deployed in private subnets

### Load Balancing

* Application Load Balancer (internet-facing)
* Target Group with EC2 instances
* Health checks on HTTP port 80

### Security

* ALB Security Group (allows HTTP from internet)
* EC2 Security Group (allows HTTP only from ALB)

---

## 4. Step-by-Step Deployment

1. Created a VPC with public and private subnets using the AWS VPC console.
2. Configured route tables:

   * Public subnets routed to Internet Gateway.
   * Private subnets routed to NAT Gateway.
3. Created security groups following least-privilege principles.
4. Launched EC2 instances in private subnets with no public IP addresses.
5. Installed and configured Nginx automatically using EC2 user-data.
6. Created a target group and registered EC2 instances.
7. Created an internet-facing Application Load Balancer in public subnets.
8. Verified application accessibility via ALB DNS name.

---

## 5. Security Configuration

### Application Load Balancer Security Group

* Inbound: HTTP (80) from 0.0.0.0/0
* Outbound: All traffic

### EC2 Instance Security Group

* Inbound: HTTP (80) from ALB security group only
* SSH: Not allowed
* Outbound: All traffic

This ensures EC2 instances are not directly accessible from the internet.

---

## 6. Application Details

The Nginx server hosts a custom HTML page displaying:

* Hello World message
* EC2 Instance ID
* Availability Zone
* Served by Nginx

Instance metadata is retrieved securely using **IMDSv2**.

---

## 7. How to Access the Application

1. Navigate to EC2 → Load Balancers in AWS Console.
2. Copy the DNS name of the Application Load Balancer.
3. Open the DNS name in a web browser.

Example:

```
http://devops-alb-xxxx.us-east-1.elb.amazonaws.com
```

---

## 8. Repository Structure

```
|   README.md - for understanding complete step by step process how i did the assignment.
│   architecture.pn - diagram
│   nginx-userdata - To install nginx at the time of creating EC2 instance
│   index.html - To display the content on the web page.
```

---

## 9. Conclusion

This project demonstrates a secure and production-style AWS deployment using private EC2 instances behind an Application Load Balancer, following modern DevOps and cloud best practices.
