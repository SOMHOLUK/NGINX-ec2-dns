# Deploying NGINX on Amazon EC2 with DNS Configuration

### 📄 Project Description

This project involves setting up a publicly accessible NGINX web server on an Amazon EC2 instance. After launching an EC2 instance, NGINX is installed and configured to serve content over HTTP on port 80, with the necessary inbound rules added to the EC2 instance’s security group to allow both SSH and HTTP traffic. To make the server reachable through a domain name instead of just an IP address, an A record is created in the DNS provider Amazon Route 53. This A record points the chosen domain to the public IP of the EC2 instance. As a result, you can open a browser and access the default NGINX welcome page simply by visiting the domain, in this case nginx.filsanhdmohamed.co.uk

---

### 🛠 Technologies Used

- Amazon EC2
- NGINX
- Amazon Route 53

---

### Pre-requisites

Before starting this project, make sure you have:

- 🌐 A registered domain name (you can buy one through Amazon Route 53 or any other domain registrar).
- 🔑 An AWS account with permissions to launch EC2 instances and manage Route 53.

---

<br> 
### Step 1: 🛒 Buy a domain name through Amazon Route 53

![ec2-pic-1](Images/ec2-pic-1.png)

---

<br> 
### Step 2: 🚀 Start the process of launching an Amazon EC2 instance.

![ec2-pic-2](Images/ec2-pic-2.png)

---

### Step 3: ⚙️ In the Instance Type section, choose the instance type: t2.micro

![ec2-pic-3](Images/ec2-pic-3.png)

---

<br> 
### Step 4: 🔑 In the Key pair (login) section, select: <u>Create a new key pair</u>. A window will appear, allowing you to download the key pair.

#### Download the key pair.

⚠️ **Remember:** It is best practice to create a separate key for each EC2 instance.  
That way, if a key is compromised, only that one instance is at risk.

![ec2-pic-4](Images/ec2-pic-4.png)

---

<br> 
### Step 5: In the network setting section, click on edit and enable the Auto-assign public IP address.

Enabling auto‑assign public IP means that a public IPv4 address is automatically assigned to the EC2 instance when it launches (when it is created). Because of the EC2 instance's public IPv4 address, the EC2 instance can be accessed from the internet.

⚠️ **Be aware:** Although you will understand this after you have read all the steps of this project, it will be mentioned here, so you can always come back to read this part. Since you have enabled the default auto-assigned public IP, this will automatically give your EC2 instance an IPv4 address, when it launches(or is created) , so if you stop the EC2 instance after it has been launched at a later stage and start it again later on (stop/start EC2 instance), your EC2 instance could be assigned a new public IPv4 address. This means you will have to update the DNS record, in other words update the value field/section with the new public IPv4 address your EC2 instance has been given after you stopped the EC2 instance and started the EC2 instance. If you do not update the DNS record with the new IPv4 address, your domain (example.com or example.co.uk) would still be pointing to the old IPv4 address and therefore your website would stop working.

- This is outside the scope of this project, but an Elastic IP provides a static IPv4 address that remains the same even if you stop and start your EC2 instance.

![ec2-pic-5](Images/ec2-pic-5.png)

---

<br> 
### Step 6: In the Network settings section, under the Firewall(Security Groups), keep Create security group selected, if this is your first setup. Furthermore, add the following rules to this security group: 1. Allow SSH traffic 2. Allow HTTP traffic from the internet.

Allowing SSH traffic opens port 22 which helps you to connect to your EC2 instance.

Allowing HTTP traffic from the internet opens port 80, as port 80 is the default port for HTTP, so your web server’s (in this case it will be NGINX's) HTTP endpoint can be accessed from anywhere.

![ec2-pic-6](Images/ec2-pic-6.png)

---

<br> 
### Step 7: Launch the EC2 instance.

![ec2-pic-7](Images/ec2-pic-7.png)

---

<br> 
### Step 8: You will see this message after you have successfully launched the instance.

![ec2-pic-8](Images/ec2-pic-8.png)

---

<br> 
### Step 9: The EC2 instance is now running. You can now connect to it using SSH.

![ec2-pic-9](Images/ec2-pic-9.png)

---

<br> 
### Step 10: In the inbound rules tab of your security group, verify that the rules you created in Step 6 such as SSH on port 22 and HTTP on port 80 are listed.

![ec2-pic-10](Images/ec2-pic-10.png)

---

<br> 
### Step 11: Click on Connect above the EC2 instance and you will be directed to the Connect to instance page, with the SSH client tab selected by default.

![ec2-pic-11](Images/ec2-pic-11.png)
![ec2-pic-12](Images/ec2-pic-12.png)

---

<br> 
### Step 12: Navigate to the Desktop, create a directory/folder called Nginx, navigate to the directory/folder Nginx and drag the Nginx-key.pem into the Nginx folder.

```
Step 1. cd Desktop
step 1. mkdir Nginx
step 2. cd Nginx

```

![ec2-pic-13](Images/ec2-pic-13.png)

---

<br> 
### Step 13: To ensure only you have access to this key, run the following command:

```
chmod 400 "Nginx-key.pem"
```

![ec2-pic-14](Images/ec2-pic-14.png)

---

<br> 
### Step 14: Copy the ssh command (at the bottom of the first picture) from the Connect to instance page and run it in your terminal, in the Nginx folder you created for step 12, to connect to your EC2 instance (as you can see in the 2nd picture below).

![ec2-pic-12](Images/ec2-pic-12.png)
![ec2-pic-15](Images/ec2-pic-15.png)

---

<br> 
### Step 15: You are now connected to the instance over SSH.

![alt text](Images/ec2-pic-16.png)

---

<br> 
### Step 16: Install Nginx using the following command, as you can see in the screenshot below as well:

```
sudo apt update -y && \
sudo apt install nginx
```

![ec2-pic-17](Images/ec2-pic-17.png)

---

<br> 
### Step 17: Once the installation of Nginx is complete, check if Nginx is running by using the following command, like in the screenshot:

```
sudo systemctl status nginx
```

![ec2-pic-18](Images/ec2-pic-18.png)

In this case, the status of Nginx was: active, Nginx was running. However, if Nginx is not active/not running in your case, you can start Nginx with the following command:

```
sudo systemctl start nginx

```

---

<br> 
### Step 18: When you stop and then start your EC2 instance again, or if it reboots for any reason (e.g., AWS maintenance or a crash), NGINX will automatically start running without you having to manually start it if you use the following command:

```
sudo systemctl enable nginx
```

![ec2-pic-19](Images/ec2-pic-19.png)

---

<br>

### Step 19: If you put the EC2 public Ipv4 address in the browser now, you should see the Nginx default welcome page, like in the screenshot below:

<br>

![ec2-pic-20](Images/ec2-pic-20.png)

However, this is not what we want. We want the domain name nginx.filsanhdmohamed.co.uk pointing to the public IP of the EC2 instance.

### Step 20: You go to the hosted zones in Amazon route 53 and click on your domain name.

![ec2-pic-21](Images/ec2-pic-21.png)

<br>

### Step 21: Click on create record.

![ec2-pic-22](Images/ec2-pic-22.png)

### Step 22: The subdomain was given the name nginx as you can see in the screenshot below, the Rercord type was set to A, and the public IP of the EC2 instance was put into the value section as you can see in the screenshot below.

Here, you have created an A record in DNS that points your domain name to the EC2 IP.

![ec2-pic-23](Images/ec2-pic-23.png)

### Step 23: The below message will appear and the website is now live and accessible via the domain name nginx.filsanhdmohamed.co.uk.

![ec2-pic-24](Images/ec2-pic-24.png)

### Step 24: The website was accessed via the domain name nginx.filsanhdmohamed.co.uk.

![ec2-pic-25](Images/ec2-pic-25.png)

### Documentation resources

- [NGINX Deployment Guide on Amazon EC2](https://docs.nginx.com) — Official NGINX documentation for deploying on AWS EC2.
- [Amazon Web Services (AWS) Documentation](https://docs.aws.amazon.com/) — Official AWS documentation and user guides.
