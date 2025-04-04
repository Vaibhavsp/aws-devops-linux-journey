# 🔐 Attaching IAM Policies (GUI + CLI)

In this guide, you’ll learn how to attach **Managed**, **Inline**, and **Custom IAM Policies** to:
- IAM Users
- IAM Groups
- IAM Roles

We'll cover both **Console (GUI)** and **Command Line Interface (CLI)** methods.

---

## ✅ 1. Attach Policy to IAM User

### 🖥️ Using AWS Console

1. Go to **IAM → Users**
2. Click on your **username**
3. Select the **Permissions** tab → Click **Add permissions**
4. Choose **Attach policies directly**
5. Search for the policy name (`AmazonS3ReadOnlyAccess` or your custom one)
6. Click **Next** → Review → **Add permissions**

---

### 💻 Using AWS CLI

```bash
aws iam attach-user-policy \
  --user-name your-user-name \
  --policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess
```

---

## ✅ 2. Attach Policy to IAM Group

### 🖥️ Console Method

1. Go to **IAM → Groups**
2. Select your group
3. Click **Attach policy**
4. Search and select the policy → **Attach**

### 💻 CLI Method

```bash
aws iam attach-group-policy \
  --group-name your-group-name \
  --policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess
```

---

## ✅ 3. Attach Policy to IAM Role

### 🖥️ Using AWS Console

1. Go to **IAM → Roles**
2. Choose the desired role
3. Click **Attach policies**
4. Search and select the policy → **Attach policy**

### 💻 Using AWS CLI

```bash
aws iam attach-role-policy \
  --role-name your-role-name \
  --policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess
```

---

## 💡 What’s the Difference?

| Type       | Scope       | Best For                          |
|------------|-------------|-----------------------------------|
| Managed    | Reusable    | Company-wide permissions sharing |
| Inline     | One-off     | Specific permissions per entity  |
| Custom     | Defined by you | Granular, specific needs       |

---

## 🧪 Bonus Tip

Use the following to **list all attached policies** for a user:

```bash
aws iam list-attached-user-policies --user-name your-user-name
```

---

## ✅ Output

- ✔️ Policy attached successfully to User/Group/Role
- ✔️ Proper permission mapping verified

---
