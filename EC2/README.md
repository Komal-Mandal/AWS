
# 📘 Amazon EC2 Instance

## 🔹 What is EC2?

Amazon Elastic Compute Cloud (EC2) is a service that provides virtual servers in the cloud.
It allows you to run applications without buying physical servers.

Think of EC2 as renting a computer from AWS that you can configure as per your needs.

## 🔹 Key Features of EC2

- 🖥 Virtual Servers (Instances) – Launch Linux/Windows servers in minutes.

- ⚡ Elasticity – Start, stop, resize, and terminate servers anytime.

- 💰 Pay-as-you-go – Pay only for what you use.

- 🛡 Security – Control access with Security Groups and IAM Roles.

- 🌍 Scalable – Add or remove instances as demand changes.

- 📦 Storage Options – Supports EBS, Instance Store, and S3.

## 🔹 EC2 Instance Lifecycle

- Launch – Start instance from an AMI.

- Running – Instance is active.

- Stopped – Instance is shut down but can be restarted.

- Terminated – Deleted permanently.

## 🔹 Networking in EC2

- VPC (Virtual Private Cloud): Your private network in AWS.

- Subnet: Divide VPC into smaller networks.

- Security Groups (SG): Firewall for inbound/outbound traffic.

- NACLs: Firewall at subnet level.

- Elastic IP (EIP): Static public IP address for your instance.

## 🔹 Steps to Launch EC2 Instance

Go to AWS Console → EC2 → Launch Instance.

Choose an AMI (Amazon Machine Image) like Ubuntu, Amazon Linux, or Windows.

Choose an Instance Type (e.g., t2.micro for free tier).

Configure network (VPC, subnet, SG).

Add EBS volume if needed.

Add key pair (for SSH).

Launch instance and connect via SSH/RDP.


# Practicals

## 1.Dockerizing-and-Deploying-a-Node.js-Application-on-AWS-EC2

## LINK:

https://github.com/Komal-Mandal/Dockerizing-and-Deploying-a-Node.js-Application-on-AWS-EC2

## 2. streamlit-app-deployment-using-EC2

## LINK:

https://github.com/Komal-Mandal/streamlit-app-deployment-using-EC2


