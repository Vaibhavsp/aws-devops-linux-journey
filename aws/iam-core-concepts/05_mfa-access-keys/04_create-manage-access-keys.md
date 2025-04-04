## 🔐 Create & Manage Access Keys for IAM Users – Step-by-Step

---

### ✅ What are Access Keys?

Access Keys =  
🔑 `Access Key ID` +  
🔐 `Secret Access Key`

Used to make **programmatic access** to AWS services via:
- AWS CLI
- SDKs
- APIs

⚠️ **Access Keys are like passwords** for your CLI/API access. Handle them securely!

---

## 🧰 Step-by-Step: Create Access Key (GUI)

1. Login to **AWS Console**
2. Navigate to **IAM > Users**
3. Click on the **username**
4. Go to **"Security Credentials"**
5. Scroll to **"Access Keys"**
6. Click on **"Create Access Key"**
7. Choose use-case:  
   - For CLI, SDK, or API
8. Download or copy the:
   - Access Key ID
   - Secret Access Key

⚠️ Secret Access Key is shown **only once**. Store it securely!

---

## 🧰 Step-by-Step: Create Access Key (CLI)

```bash
aws iam create-access-key --user-name <your-iam-username>
```

Output will be:

```json
{
    "AccessKey": {
        "AccessKeyId": "AKIA...",
        "SecretAccessKey": "wJalrXUtnFEMI/K7MDENG/bPxRfiCYz...",
        ...
    }
}
```

---

## 🛑 Limitations

- Only **2 access keys per user** allowed.
- If both are active, one must be deleted or deactivated before creating a new one.

---

## 🔄 Rotate Access Keys (Best Practice)

1. **Create new access key**
2. **Update your CLI/environment with new key**
3. **Test the new key**
4. **Deactivate the old access key**
5. **Delete the old access key once confirmed**

---

## 🔧 Manage Access Keys (CLI)

### List Access Keys

```bash
aws iam list-access-keys --user-name <username>
```

### Deactivate Access Key

```bash
aws iam update-access-key \
  --access-key-id <key-id> \
  --status Inactive \
  --user-name <username>
```

### Delete Access Key

```bash
aws iam delete-access-key \
  --access-key-id <key-id> \
  --user-name <username>
```

---

## 🧠 Things to Remember

- Never hardcode access keys in your code!
- Use **IAM roles** wherever possible.
- Use **AWS Secrets Manager** or environment variables if needed.
- Always enable **MFA** with access key usage.
- Use **CloudTrail** to track access key usage.

---
