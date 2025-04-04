## 🔐 How to Set Up MFA for IAM Users (GUI + CLI)

---

## 🔹 1. Setup via AWS Management Console (GUI)

### ✅ Step-by-Step (Virtual MFA using Google Authenticator or Authy)

1. **Login to AWS Console** as root or an IAM user with admin privileges.
2. Go to **IAM → Users → [Select User] → Security credentials tab**.
3. Click **"Manage"** next to **Multi-factor authentication (MFA)**.
4. Choose **"Virtual MFA device"** and click **Continue**.
5. Open your **MFA app** (Google Authenticator / Authy) and **scan the QR code**.
6. Enter the two consecutive **6-digit codes** shown in your app.
7. Click **Assign MFA**.

📸 Screenshot it for portfolio:
> _"MFA successfully assigned to IAM user"_ ✅

---

## 🔹 2. Setup via CLI (AWS CLI v2)

### ✅ Prerequisites:
- AWS CLI installed
- IAM user access key configured

### ✅ Step-by-Step:

```bash
# Step 1: Create virtual MFA device
aws iam create-virtual-mfa-device \
  --virtual-mfa-device-name my-virtual-mfa \
  --outfile QRCode.png \
  --bootstrap-method QRCodePNG \
  --output text

# Open QRCode.png and scan with Google Authenticator

# Step 2: Enable MFA for user
aws iam enable-mfa-device \
  --user-name my-user \
  --serial-number arn:aws:iam::123456789012:mfa/my-virtual-mfa \
  --authentication-code1 123456 \
  --authentication-code2 654321
```

✅ Replace `my-user`, `serial-number`, and the codes accordingly.

---

## 🔹 3. Enable MFA for Root User

Highly recommended!

Follow the same GUI steps for the root user. Navigate to the root user security credentials via the **“My Security Credentials”** section from the user menu in the AWS Console.

---

## 🔐 How to Test MFA is Working?

Log in as the IAM user with MFA enabled → You’ll be prompted for the MFA token after entering your password.

---
