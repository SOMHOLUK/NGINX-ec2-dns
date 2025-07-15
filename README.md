# Deploying NGINX on Amazon EC2 with DNS Configuration

## 📄 Project Description

This project involves launching an Amazon EC2 instance and installing NGINX on it.
The EC2 instance is configured so that its security group allows inbound HTTP traffic from the internet.
NGINX is set up to listen on port 80 and handle incoming HTTP requests.

Then you configure your DNS and create the A record in Route 53 by pointing the domain nginx.filsanhdmohamed.co.uk to the EC2 instance’s public IP.
As a result, the NGINX default welcome page can be accessed through the domain nginx.filsanhdmohamed.co.uk.

---

## 🛠 Technologies Used

- Amazon EC2
- NGINX
- Amazon Route 53

---

## Pre-requisites

Before starting this project, make sure you have:

- 🌐 A registered domain name (you can buy one through Amazon Route 53 or any other domain registrar).
- 🔑 An AWS account with permissions to launch EC2 instances and manage Route 53.

## Step 1: 🛒 Buy a domain name through Amazon Route 53

![ec2-pic-1](images/ec2-pic-1.png)

## Step 2: 🚀 Start the process of launching an Amazon EC2 instance.

![ec2-pic-2](images/ec2-pic-2.png)

## Step 3: ⚙️ In the Instance Type section, choose the instance type: t2.micro

![ec2-pic-3](images/ec2-pic-3.png)

## Step 4: 🔑 In the Key pair (login) section, select: <u>Create a new key pair</u>. A window will appear, allowing you to download the key pair.

⚠️ **Remember:** It is best practice to create a separate key for each EC2 instance.  
That way, if a key is compromised, only that one instance is at risk.

![ec2-pic-4](images/ec2-pic-4.png)

## Documentation resources

- [NGINX Deployment Guide on Amazon EC2](https://docs.nginx.com) — Official NGINX documentation for deploying on AWS EC2.
- [Amazon Web Services (AWS) Documentation](https://docs.aws.amazon.com/) — Official AWS documentation and user guides.
