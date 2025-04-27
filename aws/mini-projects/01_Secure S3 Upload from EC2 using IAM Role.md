# Secure S3 Upload from EC2 using IAM Role

This is a simple hands-on project to demonstrate the use of **IAM Roles** for granting an EC2 instance access to an S3 bucket — **without using access keys**. We’ll use **AWS CLI** to upload a file to S3 directly from EC2.

---

## 🛠 **Project Overview**

This project involves the following services:
- **IAM** (Identity and Access Management)
- **EC2** (Elastic Compute Cloud)
- **S3** (Simple Storage Service)

The key goal of this project is to:
1. Attach an **IAM Role** to an EC2 instance.
2. Grant **S3 permissions** to the IAM Role.
3. Upload a test file from the EC2 instance to an S3 bucket using **AWS CLI** without using **AWS access keys**.

---

## 🔧 **Hands-On Steps**

### Step 1: **Create IAM Role for EC2 (with S3 Access)**

1. Navigate to **IAM → Roles → Create Role**.
2. Select **AWS service** as the trusted entity, and choose **EC2**.
3. Attach the **AmazonS3FullAccess** policy (or create a custom policy if needed).
4. Name the role: **EC2-S3UploadRole**.
5. Review and create the role.

![01](https://github.com/user-attachments/assets/aee7e80e-786f-44e5-859d-4e0ebabbcd8b)

**Important Notes:**  
- The IAM role grants EC2 permissions to access S3 without needing static AWS keys.

---

### Step 2: **Launch EC2 Instance and Attach IAM Role**

1. Go to **EC2 → Launch Instance**.
2. Choose **Amazon Linux 2 AMI** (or any other suitable AMI).
3. Select **t2.micro** instance type (free-tier eligible).
4. In **Advanced Settings**, under **IAM Role**, choose **EC2-S3UploadRole** (the IAM role created in Step 1).

![02](https://github.com/user-attachments/assets/160e9e5e-1a8b-4fd1-ba9e-e42784a0b106)

5. Add a **Security Group** to allow **SSH access** (port 22).
6. Launch the instance.
   
![03](https://github.com/user-attachments/assets/c6faab5b-346d-42e9-a302-20f375c9e8b7)

---

### Step 3: **SSH into EC2**

1. In the EC2 console, locate your instance and **copy the public IP**.
2. Use your **SSH key pair** to connect to the instance:
   ```bash
   ssh -i "your-key.pem" ec2-user@<your-ec2-public-ip>
   ```

---

### Step 4: **Install AWS CLI on EC2 (if not already installed)**

```bash
sudo yum update -y
sudo yum install aws-cli -y
aws --version
```

This will install the AWS CLI on your EC2 instance.

![04](https://github.com/user-attachments/assets/7e795647-b1a6-4785-a762-d748ad56a45c)

---

### Step 5: **Create a Test File on EC2**

1. Create a simple text file using the `echo` command:
   ```bash
   echo "Hello, this is a test upload to S3" > testfile.txt
   ```
2. Check that the file has been created:
   ```bash
   ls -l testfile.txt
   ```

---

### Step 6: **Upload the File to S3 Using AWS CLI**

1. Use the AWS CLI command to upload the file to your S3 bucket:
   ```bash
   aws s3 cp testfile.txt s3://your-bucket-name/
   ```

2. Verify that the file has been uploaded successfully.

![05](https://github.com/user-attachments/assets/ceac1451-45c3-4020-9400-febb25059ea6)

---

### Step 7: **Validate the File Upload in S3 Console**

1. Go to **S3 → Your Bucket → Objects**.
2. Ensure that **testfile.txt** appears in your S3 bucket.

![06](https://github.com/user-attachments/assets/8fcf7102-4773-45cb-a5eb-6bba4e250d6c)

---

## 🔑 **Important Notes**

- **IAM Role** attached to EC2 instance ensures access to S3 without needing to configure **AWS keys** on the EC2 instance.
- No need to manually configure `aws configure` on EC2.
- This setup uses **IAM Role + EC2 + S3** for secure and automated access management.
- **Best Practice**: **Never hardcode AWS credentials** — always use **IAM roles** to assign permissions to your instances.

---

## 📚 **What You’ve Learned:**

- IAM Role creation and attachment to EC2
- Using **AWS CLI** to manage files between EC2 and S3
- Best practices for securely interacting with AWS resources (no access keys)
