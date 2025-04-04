# IAM Users – GUI Hands-on (AWS Console)

## 👣 Step-by-Step to Create IAM User (Console)

1. **Login to AWS Console** → IAM Service  
2. Click on **Users > Add users**
3. Enter a **user name**: `DemoUser`
4. Select **Access type**:
   - ✅ Programmatic access (CLI/SDK)
   - ✅ AWS Management Console access (Web)
5. Set password options (auto or custom password)
6. Click **Next: Permissions**
7. Attach existing policies like `AmazonS3ReadOnlyAccess` or `AdministratorAccess`
8. Add tags (optional)
9. Review and **Create User**

---

## 📸 Post-Creation:
- Note the **Access key ID** and **Secret** (only visible once!)
- Test user login from the AWS sign-in link using the assigned credentials

---

## 🔐 MFA Setup (GUI):
1. Go to **Users > [UserName]**
2. Choose **Security Credentials**
3. Click on **Manage MFA**
4. Select **Virtual MFA device** → Use Authenticator App
5. Scan QR Code → Enter both OTPs → ✅ Done!
