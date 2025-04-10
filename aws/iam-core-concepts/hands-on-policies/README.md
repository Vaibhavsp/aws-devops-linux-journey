# 🔐 IAM Policies – Hands-On with Managed & Inline Policies (S3 + EC2 Use Case)

This hands-on demonstrates how to create and apply both **Managed** and **Inline** IAM policies, attach them to EC2 roles, and validate permissions using the AWS CLI.


## 📌 Use Case

✅ Give EC2 instance **read-only access to all S3 buckets** using a **Managed Policy**  
✅ Then, restrict access to **only one S3 bucket** using an **Inline Policy**


## 🧱 1. Create Managed IAM Policy

1. Go to → **IAM → Policies → Create Policy**
2. Use Visual Editor:
   - Service: `S3`
   - Actions: `ListBucket`, `GetObject`
   - Resources: `All`
3. Name: `S3ReadOnlyCustomPolicy`
4. Click **Create Policy**

![9](https://github.com/user-attachments/assets/535c37aa-aa3c-4361-8ab0-a3fc74fd1619)


![8](https://github.com/user-attachments/assets/b69b5f04-6b20-44ad-9e10-d0167b28a097)


## 🔧 2. Attach Policy to Role

1. IAM → Roles → Select EC2 Role  
2. Go to **Permissions → Add permissions**  
3. Choose: **Attach policies directly**  
4. Select `S3ReadOnlyCustomPolicy`  
5. Click **Add permissions**

![16](https://github.com/user-attachments/assets/5cbdb04a-af0b-4d43-9124-ca9e26b186d8)


## 💻 3. Attach Role to EC2 Instance

1. EC2 → Select Instance  
2. Actions → Security → Modify IAM Role  
3. Attach the role used above


## 🧪 4. Validate Access from EC2 (via CLI)

```bash
aws s3 ls
```


✅ Lists buckets if policy is correct.

![17](https://github.com/user-attachments/assets/dbf93bc9-c207-411c-8a39-11b6652dc3fe)


## ✳️ 5. Add Inline Policy to Restrict Access

1. IAM → Roles → Select same EC2 role  
2. Go to **Permissions → Add inline policy**  
3. Use Visual Editor:
   - Actions: `ListBucket`, `GetObject`
   - Resource:
     - `arn:aws:s3:::your-bucket-name`
     - `arn:aws:s3:::your-bucket-name/*`
4. Name: `InlineS3AccessPolicy` → Create Policy

![5](https://github.com/user-attachments/assets/f9d00618-1158-4198-8901-756d61fbd97f)


## 🚀 6. Re-Test from EC2 (Bucket-Specific)

```bash
aws s3 ls s3://your-bucket-name
aws s3 cp s3://your-bucket-name/sample.txt .
```

✅ Only this bucket is accessible  
❌ All others denied

![7](https://github.com/user-attachments/assets/bab4557a-dabe-4876-b536-8890d31490b0)

---

## 🔗 Blog + Repo

📝 Blog: [medium.com/@vaibhavparekh097](https://medium.com/@vaibhavparekh097)  
📁 Repo: [github.com/Vaibhavsp](https://github.com/Vaibhavsp)
