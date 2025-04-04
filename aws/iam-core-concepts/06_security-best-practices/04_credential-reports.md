# 📊 IAM Credential Reports

Credential reports are essential for auditing **IAM users and their credentials** (passwords, access keys, MFA status, etc.) across your AWS account. It gives a complete picture of user security hygiene.

---

## ✅ What is a Credential Report?

An IAM **Credential Report** is a downloadable `.csv` file that contains the **status of IAM users' credentials**. It includes:
- Password enabled or not
- Password last used
- MFA enabled
- Access key rotation
- Access key last used
- Whether credentials are unused or stale

---

## 🎯 Why Use It?

| Purpose | Benefit |
|--------|---------|
| **Security Audit** | Identify users with weak security settings |
| **Key Rotation Checks** | Detect stale access keys |
| **MFA Monitoring** | Find users without MFA enabled |
| **Compliance Reporting** | Helpful in audits & reviews |

---

## 🧪 How to Generate Credential Report

### 📌 GUI (AWS Console):

1. Navigate to **IAM Dashboard**
2. In the left pane, click **"Credential Report"**
3. Click **"Download Report"**
4. Open the `.csv` file in Excel or Google Sheets

### 📌 CLI:

```bash
# Generate the report (AWS takes a few seconds to prepare it)
aws iam generate-credential-report

# Download the report
aws iam get-credential-report --query Content --output text | base64 -d > credential-report.csv
```

> ✅ `base64 -d` is used to decode the base64 encoded report to human-readable `.csv` file.

---

## 📝 Sample Output Fields

| Field | Description |
|-------|-------------|
| `user` | IAM username |
| `password_enabled` | true/false |
| `password_last_used` | Timestamp |
| `mfa_active` | true/false |
| `access_key_1_active` | true/false |
| `access_key_1_last_used_date` | Timestamp or N/A |
| `access_key_1_last_rotated` | Date of last key rotation |

---

## 🔒 Best Practices

- Rotate access keys every 90 days
- Disable unused access keys
- Enforce MFA for all users
- Regularly review and download credential reports
- Use automation to notify stale credentials

---

## 🔍 Troubleshooting

| Issue | Fix |
|-------|-----|
| **Report not ready** | Wait a few seconds and re-run the `get-credential-report` |
| **Permission denied** | Ensure your user has `iam:GenerateCredentialReport` and `iam:GetCredentialReport` permissions |

---

## 📁 Real Project Use Case

Use credential reports during security reviews in your Disaster Management project:
- Ensure all automated EC2 IAM roles use access keys with proper rotation
- Make sure ops team users have MFA enforced
- Flag users with unused credentials

---

✅ Add this report to your repository under:
```
📁 05_mfa-access-keys/
   └── 04_credential-reports.md
```
