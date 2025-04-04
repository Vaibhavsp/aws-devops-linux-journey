# 🏗️ IAM Policy Structure Deep Dive

IAM policies are JSON documents made up of key-value pairs. Let’s break down each component so you can **read, write, and troubleshoot policies** like a pro!

---

## 🧱 Basic Structure of a Policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::my-bucket"
    }
  ]
}

```

---

## 🔍 Key Elements Explained

| Key        | Description |
|------------|-------------|
| `Version`  | Defines policy language version. Always use `"2012-10-17"`. |
| `Statement`| One or more permission statements inside a policy. Can be a single object or an array. |

---

### 🔹 Inside the `Statement`

| Key        | Description |
|------------|-------------|
| `Effect`   | Can be `"Allow"` or `"Deny"` — Deny always takes priority. |
| `Action`   | AWS service actions like `ec2:StartInstances`, `s3:GetObject`. Use `"*"` to allow all actions. |
| `Resource` | Specifies AWS resources by ARN. `"*"` applies to all resources. |
| `Condition`| (Optional) Adds extra rules based on IP, time, MFA, etc. |

---

## 🧩 Example: Multiple Actions on Multiple Resources

```json
{
  "Effect": "Allow",
  "Action": [
    "s3:GetObject",
    "s3:PutObject"
  ],
  "Resource": [
    "arn:aws:s3:::my-bucket",
    "arn:aws:s3:::my-bucket/*"
  ]
}
```

---

## 🧩 Example with Condition

```json
{
  "Effect": "Allow",
  "Action": "s3:PutObject",
  "Resource": "arn:aws:s3:::my-bucket/*",
  "Condition": {
    "IpAddress": {
      "aws:SourceIp": "192.168.1.0/24"
    }
  }
}
```

🔒 Only allows uploads from a specific IP range.

---

## ⚠️ Best Practices

- Use **Least Privilege Principle** — only give required permissions.
- Avoid `"Action": "*"` unless absolutely necessary.
- Always test new policies with the **IAM Policy Simulator**.
- Use `Condition` for added security.

---

## 🛠️ Tools for Policy Writing

- ✅ [IAM Policy Generator](https://awspolicygen.s3.amazonaws.com/policygen.html)
- ✅ [IAM Policy Simulator](https://policysim.aws.amazon.com/)
- ✅ Visual Editor in AWS Console (GUI-based policy builder)

---

