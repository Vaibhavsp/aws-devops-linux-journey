## *IAM Cross-Account Access CLI Setup (Step-by-Step)*

This file contains **all required AWS CLI commands** to set up **Cross Account Access** between **Account A (Trusting)** and **Account B (Trusted)**.

---

### 🎯 Goal

Allow a user from **Account B** to assume a role in **Account A** using CLI.

---

### 🧱 Account Structure

| Element               | Account A                        | Account B                        |
|-----------------------|----------------------------------|----------------------------------|
| Account Purpose       | Resource Owner (Trusting)       | IAM User Owner (Trusted)        |
| IAM Role              | `CrossAccountAccessRole`        | N/A                              |
| IAM User              | N/A                              | `cross-user`                    |

---

### 🔧 Step-by-Step CLI Setup

---

#### ✅ Step 1: Create IAM Role in Account A (Trusting Account)

```bash
aws iam create-role \
  --role-name CrossAccountAccessRole \
  --assume-role-policy-document file://trust-policy.json
```

🗂️ `trust-policy.json` example:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::<Account-B-ID>:root"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

---

#### ✅ Step 2: Attach Permission Policy to Role in Account A

```bash
aws iam attach-role-policy \
  --role-name CrossAccountAccessRole \
  --policy-arn arn:aws:iam::aws:policy/ReadOnlyAccess
```

---

#### ✅ Step 3: (Optional) Create User in Account B

```bash
aws iam create-user --user-name cross-user
```

Then generate access keys:

```bash
aws iam create-access-key --user-name cross-user
```

---

#### ✅ Step 4: Configure AWS CLI on User's Machine (Account B)

```bash
aws configure --profile account-b-user
```

Set:
- AWS Access Key
- Secret Key
- Region

---

#### ✅ Step 5: Assume Role from Account B (CLI)

```bash
aws sts assume-role \
  --role-arn arn:aws:iam::<Account-A-ID>:role/CrossAccountAccessRole \
  --role-session-name crosssession \
  --profile account-b-user
```

➡️ This returns temporary security credentials:  
- AccessKeyId  
- SecretAccessKey  
- SessionToken  

---

#### ✅ Step 6: Use Temporary Credentials in a New CLI Profile

```bash
aws configure --profile cross-access
```

Fill in the values from `Step 5` output (AccessKeyId, SecretAccessKey, SessionToken)

---

#### ✅ Step 7: Perform Actions in Account A using `cross-access` profile

```bash
aws s3 ls --profile cross-access
```

---

### 🔐 Bonus: Automate CLI Switching (Using `export`)

```bash
export AWS_ACCESS_KEY_ID="TempKeyHere"
export AWS_SECRET_ACCESS_KEY="TempSecretKeyHere"
export AWS_SESSION_TOKEN="TempTokenHere"
```

---
