# IAM Users – AWS CLI Hands-on

## 🧰 Prerequisites:
- AWS CLI installed
- User configured with `aws configure`

---

## 👤 Create IAM User

```bash
aws iam create-user --user-name DemoUser
```

## 🔒 Attach Policy to IAM User
```bash
aws iam attach-user-policy \
  --user-name DemoUser \
  --policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess
```

## 🔑 Create Access Key for User
```bash
aws iam create-access-key --user-name DemoUser
```

## 👮‍♂️ List Users
```bash 
aws iam list-users
```

## 🗑️ Delete IAM User
```bash
aws iam delete-user --user-name DemoUser
```



