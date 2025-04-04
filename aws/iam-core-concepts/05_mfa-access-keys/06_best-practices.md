## 🔐 IAM MFA & Access Keys – Best Practices

---

### 🔑 Access Keys Best Practices

| ✅ Recommendation | 💡 Description |
|------------------|----------------|
| **Avoid root account usage** | Never use root user access keys. Disable them if already created. |
| **Use IAM roles wherever possible** | Use IAM roles instead of access keys for services like EC2, Lambda, etc. |
| **Rotate access keys regularly** | Regularly rotate keys to minimize exposure. Use automation scripts or AWS Secrets Manager for this. |
| **Keep only 1 active key per user** | Helps with easier key management and tracking. |
| **Do not embed access keys in code** | Store securely in environment variables, parameter store, or secrets manager. |
| **Enable CloudTrail logging** | Monitor key usage to detect suspicious behavior. |
| **Use different profiles for access** | Organize access using named CLI profiles. |

---

### 🔐 MFA (Multi-Factor Authentication) Best Practices

| ✅ Recommendation | 💡 Description |
|------------------|----------------|
| **Enforce MFA for all users** | Add an IAM policy to enforce MFA on all users. |
| **Enable MFA on the root account** | This is mandatory. Root account is the most sensitive. |
| **Use Virtual MFA Devices** | Google Authenticator, Authy, or Duo Mobile work great. |
| **Use MFA with sensitive actions** | Use IAM policies to restrict sensitive actions unless MFA is used. |
| **Track MFA enablement** | Use AWS Config or custom Lambda rules to check who doesn't have MFA. |
| **Revalidate MFA regularly** | Periodically review and update MFA devices, especially when changing phones. |

---

### 📌 Pro Tips

- Use **AWS Organizations** SCPs to restrict accounts to require MFA globally.
- Combine MFA with **IAM Conditions** for enhanced security like below:

```json
"Condition": {
  "BoolIfExists": {
    "aws:MultiFactorAuthPresent": "true"
  }
}
```

- Use the `aws sts get-caller-identity` command to validate which credentials are currently being used.

---

✅ This file helps reinforce secure practices while using IAM credentials.  
