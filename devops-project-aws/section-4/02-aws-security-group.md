# Expose project on EC2 instance

- In this lecture we will expose the port 8080 in inbound rules of security group to allow ingress traffic to the ec2 instance.

### **Step 1: Log in to AWS Console**
- Go to [AWS Management Console](https://aws.amazon.com/console/)
- Navigate to **EC2 Dashboard**
- Click on **Security Groups** under **Network & Security**

### **Step 2: Select the Security Group**
- Identify and select the Security Group associated with your EC2 instance
- Click on the **Inbound rules** tab
- Click **Edit inbound rules**

### **Step 3: Add a New Inbound Rule**
- Click **Add Rule**
- Select **Type** (Choose a predefined rule like HTTP, SSH, or Custom)
- Select **Protocol** (Automatically populated based on Type)
- Enter **Port Range** (e.g., `80` for HTTP, `22` for SSH, `8080` for custom apps)
- Select **Source**:
  - `My IP` (restrict access to your IP)
  - `Custom` (specify a range like `192.168.1.0/24`)
  - `Anywhere (0.0.0.0/0)` (allows access from any IP, not recommended for production)
- Click **Save rules**

### **Step 4: Verify the Changes**
- Ensure the rule appears in the **Inbound Rules** list
- Test connectivity by accessing the instance on the exposed port

