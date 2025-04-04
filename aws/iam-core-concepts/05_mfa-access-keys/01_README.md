#### 🔹 What is MFA?
**Multi-Factor Authentication (MFA)** is an additional layer of security used to verify a user’s identity when signing in to an AWS account. It requires two types of authentication:
- Something you **know** (password)
- Something you **have** (a physical or virtual MFA device)

---

#### 🔹 Why Use MFA?
- Protects against compromised passwords.
- Adds an extra layer of protection for critical operations.
- Essential for root users and highly privileged IAM users.
- Required in many compliance standards (e.g., CIS benchmarks, PCI-DSS).

---

#### 🔹 Types of MFA Devices in AWS:
| Device Type                | Description                                         |
|---------------------------|-----------------------------------------------------|
| Virtual MFA device         | Apps like Google Authenticator, Authy, etc.        |
| U2F security key (FIDO)    | Hardware device like YubiKey                       |
| Hardware MFA (Gemalto, etc.) | Physical token with 6-digit code                |

---

#### 🔹 Where MFA is Used?
- **Root account protection**
- **IAM user sign-in**
- **CLI operations with session tokens**
- **Securing AWS services via IAM policies**

---

#### 🔹 Example Scenario:
> You're using the AWS root user to manage billing. Enabling MFA on this account ensures that even if your password is leaked, an attacker can't access your billing dashboard unless they have your MFA device.

---
