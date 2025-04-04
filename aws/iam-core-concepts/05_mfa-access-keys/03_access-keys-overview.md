## 🔑 What are AWS Access Keys?

---

### 🔹 What:

Access Keys in AWS are a combination of:

- `Access Key ID` → like a username  
- `Secret Access Key` → like a password

They are used by **programmatic access** to AWS services (CLI, SDKs, APIs).

---

### 🔹 Why:

- IAM Users need Access Keys to interact with AWS **outside the Console**
- Required for:
  - AWS CLI
  - SDKs (Python `boto3`, JavaScript `aws-sdk`)
  - CI/CD automation
  - Terraform / Ansible integrations

---

### 🔹 How:

You can **generate**, **view**, and **rotate** access keys from:

#### ✅ 1. AWS Console (GUI)

**Steps:**

1. Go to: `IAM → Users → [Select user] → Security Credentials tab`
2. Click: `Create Access Key`
3. Choose: `Application running outside AWS` → Click **Next**
4. Click **Create access key**
5. Store it securely (you won’t see it again)!

📸 Screenshot to capture:  
_"Access Key ID and Secret Access Key generated"_ ✅

#### ✅ 2. CLI

```bash
# Create access key for user
aws iam create-access-key --user-name my-user
```

```bash
# Output example
{
    "AccessKey": {
        "AccessKeyId": "AKIAIOSFODNN7EXAMPLE",
        "SecretAccessKey": "wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY"
    }
}
```

📌 You must store this **immediately** — the secret is shown **only once**.

---

### ⚠️ Important Notes:

- Max 2 access keys per user
- Always rotate access keys regularly
- NEVER hardcode them in code
- Use **environment variables** or **AWS credentials file**

---

### 🧼 Clean-up Tip (CLI):

```bash
# List all access keys
aws iam list-access-keys --user-name my-user

# Delete an old one
aws iam delete-access-key \
  --user-name my-user \
  --access-key-id AKIAIOSFODNN7EXAMPLE
```

---
