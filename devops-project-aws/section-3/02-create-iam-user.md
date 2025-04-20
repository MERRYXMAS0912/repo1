# **AWS IAM User Creation Guide for Beginners**

## **Step-by-Step IAM User Creation**

### **Step 1: Log in to AWS Console**
- Go to [AWS Management Console](https://aws.amazon.com/console/)
- Sign in with your **Root Account**
- Navigate to **IAM Dashboard**

### **Step 2: Open IAM Users Section**
- Click on **Users** in the left navigation pane
- Click **Add User**

### **Step 3: Enter User Details**
- Provide a **User Name** (e.g., `devops-user`)
- Select **AWS Credential Type**:
  - **Access Key – Programmatic Access** (for CLI, SDKs, API access)
  - **Password – AWS Management Console Access** (for GUI access)
- Click **Next**

### **Step 4: Assign Permissions**
- Choose how to set permissions:
  - **Attach Existing Policies Directly** (e.g., `AdministratorAccess`, `PowerUserAccess`, `ReadOnlyAccess`)
  - **Add to a Group** (recommended for better management)
  - **Copy from Another User**
- Click **Next**

### **Step 5: Add Tags (Optional)**
- Assign metadata like `Department: DevOps`, `Project: E-Commerce`
- Click **Next**

### **Step 6: Review and Create User**
- Review all details carefully
- Click **Create User**

### **Step 7: Download Credentials**
- Download the **Access Key ID & Secret Access Key** (if programmatic access is enabled)
- Save these credentials securely (they won’t be shown again)
- Click **Close**