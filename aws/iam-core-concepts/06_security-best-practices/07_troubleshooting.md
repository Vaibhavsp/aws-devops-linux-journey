# 🧰 Troubleshooting: IAM MFA & Access Keys

This guide covers common issues while managing **MFA (Multi-Factor Authentication)** and **Access Keys**, and how to resolve them effectively.

---

## 🔐 1. Access Denied When Enabling MFA

### Issue:
User tries to enable MFA but gets “Access Denied.”

### Cause:
The IAM policy attached to the user doesn’t allow `iam:EnableMFADevice`.

### Solution:
Ensure user or group has the following permissions:

```json
{
  "Effect": "Allow",
  "Action": [
    "iam:EnableMFADevice",
    "iam:ListMFADevices",
    "iam:ResyncMFADevice"
  ],
  "Resource": "*"
}
```

---

## 🔁 2. MFA Sync Fails or Token Rejected

### Issue:
User enters the right code, but it fails.

### Cause:
- Time not synced on the virtual MFA app (Google Authenticator)
- Device was reset or out of sync

### Solution:
- Use `ResyncMFADevice` via Console or CLI
- Re-enable MFA if resync fails

---

## ❌ 3. Access Keys Not Working

### Issue:
Access key & secret key pair shows `InvalidClientTokenId`.

### Cause:
- Keys are inactive
- Deleted or never rotated
- IAM user doesn’t exist

### Solution:
- Go to **IAM → Users → Security Credentials**
- Check if keys are **Active**
- Rotate or create new keys regularly

---

## 🔂 4. MFA-Required Actions Failing via CLI

### Issue:
Accessing a service like S3 or EC2 fails due to missing MFA context.

### Solution:
Use **session tokens** (STS) when MFA is enforced.

```bash
aws sts get-session-token \
  --serial-number arn:aws:iam::<account-id>:mfa/<username> \
  --token-code <code-from-MFA>
```

Use the returned `AccessKeyId`, `SecretAccessKey`, and `SessionToken` for session-based commands.

---

## 🔍 5. Trouble Creating Access Keys (Limit Exceeded)

### Issue:
Only 2 access keys are allowed per user.

### Solution:
- Deactivate or delete one key using Console or CLI:
```bash
aws iam delete-access-key --access-key-id ABCDEFG1234567890
```

---

## 🔧 6. Can't Reassign MFA Device

### Issue:
Old device is lost or reset, and new one can't be assigned.

### Solution:
Use the root user or another IAM admin to remove the MFA device from the IAM user.

---

## 📌 Bonus Tips

| Problem | Tip |
|--------|------|
| MFA doesn’t work after restore | Re-enable MFA from scratch |
| CLI fails with MFA | Always set temporary session creds |
| Forget to rotate keys | Use IAM Access Analyzer or Config to detect |

---

## 🚨 Real-Time Project Tip

For **Disaster Management Project**:
- Enforce MFA for all IAM users, especially incident responders
- Log failed login attempts and set alerts for key misuse
```

📁 `05_mfa-access-keys/07_troubleshooting.md` ✅ Done.

---
