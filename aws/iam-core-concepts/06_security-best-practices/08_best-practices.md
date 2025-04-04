# ✅ Best Practices: IAM MFA & Access Keys

Follow these best practices to secure IAM identities and their access credentials using **MFA** and **Access Keys**.

---

## 🔐 Multi-Factor Authentication (MFA)

### 🔸 What is MFA?
MFA adds a second layer of protection by requiring a time-based one-time password (TOTP) in addition to username and password.

---

### ✅ MFA Best Practices

1. **Enforce MFA for All Users**
   - Especially Admin and root users.
   - Use Service Control Policies (SCPs) in Organizations to enforce.

2. **Use Virtual MFA Devices**
   - Avoid hardware unless enterprise-grade required.
   - Apps: Google Authenticator, Authy, Duo Mobile.

3. **Avoid Sharing MFA Devices**
   - One user → one device → one MFA setup.

4. **Backup Device or Setup**
   - Store QR or backup codes securely to avoid lockouts.

5. **MFA for Console & CLI**
   - Use STS for CLI with session tokens when MFA required.

---

## 🔑 IAM Access Keys

### 🔸 What are Access Keys?
A pair of credentials (`AccessKeyId` + `SecretAccessKey`) used for programmatic access (CLI, SDKs).

---

### ✅ Access Key Best Practices

1. **Do Not Use Root Account Keys**
   - Disable root access keys if enabled.
   - Use IAM users/roles instead.

2. **Rotate Keys Regularly**
   - Set reminders every 90 days.
   - Automate detection using AWS Config Rules.

3. **Monitor with Credential Reports**
   - Regularly review for unused or old access keys.

4. **Use Temporary Credentials**
   - Prefer STS AssumeRole or IAM Roles over static keys.
   - Especially in EC2, Lambda, or ECS.

5. **Limit Key Permissions**
   - Use least privilege IAM policies.
   - Avoid `"Action": "*"` and `"Resource": "*"`.

6. **Deactivate Instead of Deleting**
   - When rotating, deactivate old keys first, test, then delete.

---

## 🧠 Additional Security Best Practices

- Enable CloudTrail to track access key usage.
- Use IAM Access Analyzer to validate permissions.
- Alert on unused or misused keys using AWS Config or GuardDuty.
- Apply Service Control Policies to restrict IAM use across orgs.

---

## 🧪 Project Integration Tip

In your Disaster Management project:
- Enforce MFA for all on-call engineers.
- Ensure EC2 access is through IAM roles, not hardcoded keys.
- Store MFA enablement status in IAM reports and alert if missing.

---

## 📝 Pro Tip:

Run this to find unused keys via Credential Report:

```bash
aws iam generate-credential-report
aws iam get-credential-report --output text --query 'Content' | base64 -d
```

Review `access_key_1_last_used_date` and rotate if needed.
```

✅ Done: `05_mfa-access-keys/08_best-practices.md`

---
