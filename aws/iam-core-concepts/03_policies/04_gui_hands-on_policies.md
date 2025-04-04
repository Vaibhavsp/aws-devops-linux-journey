# 🛠️ IAM Policy Hands-On Guide (GUI + CLI)

This file walks you through creating and attaching **custom IAM policies** using **both AWS Console (GUI)** and **AWS CLI**.

---

## 🎯 Objective

Create a custom policy that allows:
- Listing S3 buckets
- Uploading objects to a specific bucket

Then attach this policy to a user.

---

## 📍 Step-by-Step via AWS Console (GUI)

### ✅ 1. Go to IAM → Policies → **Create Policy**
1. Click **Create policy**
2. Switch to **JSON tab**
3. Paste this JSON:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:ListBucket",
        "s3:PutObject"
      ],
      "Resource": [
        "arn:aws:s3:::my-bucket",
        "arn:aws:s3:::my-bucket/*"
      ]
    }
  ]
}

```

4. Click **Next** → Add Tags (Optional) → Next

5. Name it: `S3BucketUploaderPolicy`

6. Review & **Create policy**

---

### ✅ 2. Attach Policy to User

1. Go to **IAM → Users**
2. Select the target user
3. Click **Add permissions**
4. Choose **Attach existing policies**
5. Search for `S3BucketUploaderPolicy`
6. Select it → Click **Next** → **Add permissions**

---


## ✅ Output

- ✔️ Custom policy created successfully
- ✔️ User has correct permissions
- ✔️ Real-world S3 use-case setup

---
