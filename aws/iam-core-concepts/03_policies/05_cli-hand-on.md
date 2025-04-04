## 📍 Step-by-Step via AWS CLI

### ✅ 1. Create Policy Document (locally)

Save this JSON to a file named `s3-policy.json`

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

---

### ✅ 2. Create the Policy using CLI

```bash
aws iam create-policy \
  --policy-name S3BucketUploaderPolicy \
  --policy-document file://s3-policy.json
```

📌 Note the `Arn` from the output — you'll need it to attach to the user.

---

### ✅ 3. Attach Policy to IAM User

```bash
aws iam attach-user-policy \
  --user-name your-iam-username \
  --policy-arn arn:aws:iam::account-id:policy/S3BucketUploaderPolicy
```

---

## 🧪 Test It

1. Login with the IAM user credentials.
2. Try to upload an object using AWS CLI or Console.
3. Confirm they can upload to `my-bucket` but not delete objects or access other buckets.

---

## ✅ Output

- ✔️ Custom policy created successfully
- ✔️ User has correct permissions
- ✔️ Real-world S3 use-case setup

---
