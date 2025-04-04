# 📘 IAM Policy Types in AWS

In AWS, **IAM Policies** define permissions and access control for AWS resources. There are multiple types of policies available depending on use case and scope.

---

## ✅ 1. AWS Managed Policies

**What:**  
Predefined policies created and managed by AWS.

**Use Case:**  
Attach to users, groups, or roles for common permissions (like `AmazonS3ReadOnlyAccess`, `AdministratorAccess`, etc.).

**Example ARN:**  

```
arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess
```

**Pros:**
- Easy to use
- Maintained and updated by AWS
- Fewer chances of mistakes

**Cons:**
- Less control over exact permissions
- May include more permissions than you need

---

## ✅ 2. Customer Managed Policies

**What:**  
Policies created and managed by **you** (the user or organization).

**Use Case:**  
Use when you need custom, reusable permission sets tailored to your business.

**Example ARN:**

```
arn:aws:iam::123456789012:policy/MyCustomEC2Policy
```

**Pros:**
- Full control over permissions
- Reusable across multiple entities
- Can be version-controlled

**Cons:**
- Requires understanding of JSON and IAM policy grammar

---

## ✅ 3. Inline Policies

**What:**  
Policies directly **embedded** within a single IAM user, group, or role.

**Use Case:**  
Use when a specific permission should be tightly bound to **one** entity and not reused.

**Pros:**
- One-to-one strict binding
- Good for tight-coupled use cases (e.g., break-glass admin accounts)

**Cons:**
- Not reusable
- Harder to track and manage
- Deleted if the entity is deleted

---

## 🔍 Difference Between Inline vs Managed Policies

| Feature                  | Managed Policies                  | Inline Policies                      |
|--------------------------|-----------------------------------|--------------------------------------|
| **Reusability**          | ✅ Reusable across users/roles     | ❌ One-to-one entity binding          |
| **Management**           | Centralized & Easy                | Scattered & Bound to entity          |
| **Visibility**           | Listed in IAM policy dashboard    | Only visible via the attached entity |
| **Best Practice**        | ✅ Recommended for production use  | ⚠️ Only for unique, one-off cases     |
| **Deletion Behavior**    | Independent from entity           | Deleted with the entity              |

---

## ✅ Which One Should You Use?

- Use **Managed** policies when:
  - You want centralized management
  - You want reusable permission sets

- Use **Inline** policies when:
  - You want strict one-to-one binding
  - You want tighter control for temporary access
  - You need to override permissions temporarily

---
