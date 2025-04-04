### 🧪 **Hands-On: Cross Account Access Setup**

We’ll simulate a **real-world scenario** with:

- **Account A** (User Account): Wants to access a resource (S3 bucket) in Account B  
- **Account B** (Resource Account): Owns the resource and defines access via IAM Role

We'll cover both **GUI** and **CLI** side-by-side. Let's begin! 👇

---

## 🧩 Step-by-Step Setup

---

### ✅ Step 1: Create a Role in **Account B** (Resource Owner)

#### 🔹 GUI Steps:

1. Login to **Account B (Resource Account)**.
2. Go to **IAM > Roles > Create Role**.
3. **Select Trusted Entity Type**: Another AWS Account
4. Enter **Account A ID** in the field.
5. Attach a policy (e.g., `AmazonS3ReadOnlyAccess` for S3).
6. Name the Role (e.g., `CrossAccountS3ReadRole`)
7. Create the Role ✅

#### 🔹 Trust Policy (Auto-created):
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::111111111111:root"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

Replace `111111111111` with **Account A's AWS Account ID**

---

### ✅ Step 2: Create a User in **Account A**

#### GUI:

1. Login to **Account A (User Account)**
2. Go to **IAM > Users > Add User**
3. Create a user (e.g., `crossaccount-user`)
4. Attach permissions like this:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "sts:AssumeRole",
      "Resource": "arn:aws:iam::222222222222:role/CrossAccountS3ReadRole"
    }
  ]
}
```

Replace `222222222222` with **Account B’s AWS Account ID**

---

### ✅ Step 3: Assume the Role from **Account A**

#### 🔸 CLI Commands:

```bash
aws sts assume-role \
  --role-arn arn:aws:iam::222222222222:role/CrossAccountS3ReadRole \
  --role-session-name DemoSession
```

This gives temporary credentials:
- Access Key ID
- Secret Access Key
- Session Token

You can now use these credentials to access Account B’s S3.

---

### ✅ Step 4: Use Temporary Credentials (Optional)

Configure them in CLI:

```bash
aws configure --profile crossaccount
```

Add the temporary credentials manually. Now run:

```bash
aws s3 ls --profile crossaccount
```

You can now access Account B’s S3 from Account A 🎯

---
