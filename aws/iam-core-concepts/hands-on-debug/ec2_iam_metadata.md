# EC2 IAM Role Metadata Access using IMDSv2

> **Category:** AWS IAM | EC2 | Metadata | Security
>
> **Tags:** IAM Role, EC2, Metadata Service, IMDSv2, AWS CLI, Token, Credential Access, Troubleshooting

---

## 📌 Objective
Access IAM Role credentials from an Amazon EC2 instance securely using **Instance Metadata Service v2 (IMDSv2)**.

This guide walks through a real-world troubleshooting scenario and final working solution using secure CLI methods.

---

## ⚠️ Problem Statement

While trying to retrieve IAM credentials using:
```bash
curl http://169.254.169.254/latest/meta-data/iam/security-credentials/
```
No output was returned. This usually indicates:

- IAM Role not attached to EC2
- Metadata service disabled
- IMDSv2 requirement not fulfilled

---

## 🛠 Troubleshooting Journey

### ✅ Step 1: Check IAM Role is attached
Check via EC2 Console → Instances → Select Instance → **IAM Role** column.

➡️ Role was attached correctly.

### ✅ Step 2: List Metadata Directories
```bash
curl -s http://169.254.169.254/latest/meta-data/ | grep -i "iam"
```
**No output.** Indicates possible IMDSv2 enforcement.

---

## 🔐 Switching to IMDSv2 (Token-based Access)

Amazon Linux 2023 (and other hardened AMIs) **require IMDSv2**.

### ✅ Step 3: Generate Metadata Token
```bash
TOKEN=`curl -X PUT "http://169.254.169.254/latest/api/token" \
-H "X-aws-ec2-metadata-token-ttl-seconds: 21600"`
```

### ✅ Step 4: List IAM Metadata
```bash
curl -H "X-aws-ec2-metadata-token: $TOKEN" \
http://169.254.169.254/latest/meta-data/iam/
```
**Output:** `security-credentials/`

### ✅ Step 5: Get Role Name
```bash
curl -H "X-aws-ec2-metadata-token: $TOKEN" \
http://169.254.169.254/latest/meta-data/iam/security-credentials/
```
**Output:** `<YourRoleName>`

### ✅ Step 6: Get Temporary IAM Credentials
```bash
curl -H "X-aws-ec2-metadata-token: $TOKEN" \
http://169.254.169.254/latest/meta-data/iam/security-credentials/<YourRoleName>
```
You will receive a JSON with temporary credentials: `AccessKeyId`, `SecretAccessKey`, and `Token`.

---

## 🎯 Summary of Commands Used

| Purpose             | Command                                                                 |
|---------------------|--------------------------------------------------------------------------|
| Generate Token      | `TOKEN=\curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"` |
| List IAM metadata   | `curl -H "X-aws-ec2-metadata-token: $TOKEN" http://169.254.169.254/latest/meta-data/iam/` |
| Get Role Name       | `curl -H "X-aws-ec2-metadata-token: $TOKEN" http://169.254.169.254/latest/meta-data/iam/security-credentials/` |
| Get Credentials     | `curl -H "X-aws-ec2-metadata-token: $TOKEN" http://169.254.169.254/latest/meta-data/iam/security-credentials/<role-name>` |

---

## 📂 Bonus: S3 Access Validation
After credentials were retrieved, validation was done using:
```bash
aws s3 ls
```
➡️ Verified that S3 access permissions were working via the IAM Role.

---

## 🧠 Key Learnings
- Always check if **IMDSv2** is enforced by the AMI.
- Use `curl` token-based access to safely interact with metadata.
- Always use role-based access over hardcoded credentials.
- Attach IAM policies allowing S3 or required service explicitly.

---

## ✅ Output Screenshots
> Available in `screenshots/` folder or stitched images in the blog.

---

## 📘 References
- [AWS IMDSv2 Docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/configuring-instance-metadata-service.html)
- [IAM Role Credentials on EC2](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-ec2.html)

---

**GitHub Repo:** [github.com/Vaibhavsp/aws-iam-core-concepts](https://github.com/Vaibhavsp/aws-iam-core-concepts)

**Written By:** *Vaibhav Parekh – AWS DevOps Learner | April 2025*

---

Feel free to ⭐ the repo and follow the journey!

