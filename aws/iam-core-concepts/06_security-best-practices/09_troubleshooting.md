# 🛠️ Troubleshooting: MFA & Access Keys

Here are common issues and their fixes related to **MFA** and **Access Keys** in AWS IAM.

---

### 🔸 Issue 1: MFA Not Prompting for Console Login

**Cause**: MFA not enforced or not configured for user.

**Fix**:
- Go to **IAM → Users → Security Credentials → Assign MFA**.
- Enforce using IAM policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Deny",
    "Action": "*",
    "Resource": "*",
    "Condition": {
      "BoolIfExists": {
        "aws:MultiFactorAuthPresent": "false"
      }
    }
  }]
}
```

---

### 🔸 Issue 2: Access Key Not Working in CLI

**Causes**:
- Key deactivated
- Key not correctly exported
- Expired session token (for temporary credentials)

**Fix**:
- Check key status: `aws iam list-access-keys`
- Export variables correctly:

```bash
export AWS_ACCESS_KEY_ID="your-access-key"
export AWS_SECRET_ACCESS_KEY="your-secret"
```

- If using STS:
```bash
export AWS_SESSION_TOKEN="your-session-token"
```

---

### 🔸 Issue 3: User Forgot MFA Device

**Fix**:
- As Admin, **deactivate the MFA device**.
- Provide temporary access.
- Reassign a new MFA via console.

---

### 🔸 Issue 4: “Access Denied” Even After MFA Enabled

**Cause**: Session not using MFA-authenticated token.

**Fix**:
- Use `sts get-session-token` or `assume-role` with MFA serial and token:

```bash
aws sts get-session-token \
 --serial-number arn:aws:iam::111122223333:mfa/your-user \
 --token-code 123456
```

---

### 🔸 Issue 5: Too Many Access Keys

**Cause**: Each user can have only 2 access keys.

**Fix**:
- Rotate keys:
  - Create new → Test → Deactivate old → Delete after verification.

---

### 🔸 Issue 6: Credential Report Not Accessible

**Fix**:
- Run:

```bash
aws iam generate-credential-report
aws iam get-credential-report --output text --query 'Content' | base64 -d
```

---

## 🔍 Diagnostic Tips:

- Check IAM **CloudTrail logs** to trace access key usage.
- Monitor **IAM Analyzer** for misconfigurations.
- Use **AWS Config** for compliance rules (e.g., unused keys, MFA not enabled).

---
