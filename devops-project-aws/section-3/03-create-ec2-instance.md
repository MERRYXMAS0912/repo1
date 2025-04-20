# **AWS EC2 Instance Setup Guide for Beginners**

## **Introduction**
Amazon EC2 (Elastic Compute Cloud) provides resizable compute capacity in the cloud. This guide will help beginners launch an EC2 instance and tackle common challenges they might face.

---

## **Step-by-Step EC2 Instance Setup**

### **Step 1: Log in to AWS Console**
- Go to [AWS Management Console](https://aws.amazon.com/console/)
- Sign in with your AWS account credentials
- Navigate to **EC2 Dashboard**

### **Step 2: Launch a New EC2 Instance**
- Click **Launch Instance**
- Enter an instance name

### **Step 3: Choose an Amazon Machine Image (AMI)**
- Select an OS
- Click **Select**

### **Step 4: Choose an Instance Type**
- Select a suitable instance type:
  - **t3.xlarge+** (For heavier workloads)
- Click **Next**

### **Step 5: Configure Instance Details**
- Keep the default **VPC & Subnet** (unless customizing networking)
- Enable **Auto-assign Public IP** (for internet access)
- Click **Next**

### **Step 6: Add Storage**
- Default storage: 8GB but you can change that to 30 GB as we will download a lot of container images related to the project.
- Click **Next**

### **Step 7: Configure Security Group**
- Create a new security group or use an existing one
- Allow **SSH (port 22)** for Linux instances

### **Step 8: Generate or Select a Key Pair**
- Select **Create a new key pair**
- Choose **RSA** format and download the `.pem` file
- **Store the key securely** (You will need it to access your instance)
- Click **Launch Instance**

### **Step 9: Connect to Your EC2 Instance**
- Navigate to **EC2 Dashboard** → **Instances**
- Select the instance and click **Connect**

#### **For Linux Instances:**
- Use SSH from terminal:
  ```bash
  ssh -i /path/to/your-key.pem ec2-user@your-instance-public-ip
  ```

---

## **Common Challenges & How to Overcome Them**

### **1. Key Pair Issues**
- If you lose your `.pem` file, you **cannot recover it**
- Create a new key pair and manually update the instance’s key (requires console access)

### **2. SSH Connection Problems**
- Ensure **Port 22** is open in the security group
- Use `chmod 400 your-key.pem` to set the correct permissions for the key file
- Verify the correct **public IP address** is used

### **3. EC2 Instance Not Accessible via Internet**
- Ensure **Auto-assign Public IP** was enabled
- Check **Security Group & NACL rules**
- Consider using **Elastic IP** for a static IP address

### **4. High Costs Due to Running Instances**
- Stop or terminate unused instances
- Use **AWS Billing Dashboard** to monitor usage
- Set up **AWS Budgets & Alerts**
