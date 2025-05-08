# Basic Cloud Hosting POC - AWS EC2 Apache Web Server

---

## 1. Tech Stack Used:
- AWS EC2 (Amazon Linux 2)
- AWS VPC
- AWS Security Groups
- Apache Web Server
- SSH (PuTTY/Terminal)

---

## 2. Concept Summary:
We hosted a basic website by launching an EC2 instance in AWS inside a default VPC, securing it with security groups, installing an Apache server, and uploading a custom website page. Security hardening and professional best practices were applied.

---

## 3. Detailed Flow:

| Step | Action |
|:-----|:-------|
| 1 | Launch EC2 in Default VPC |
| 2 | Configure Security Group (HTTP, SSH) |
| 3 | SSH into EC2 Instance |
| 4 | Update Packages |
| 5 | Install Apache Web Server |
| 6 | Start Apache Service |
| 7 | Create & Upload Custom Website (index.html) |
| 8 | Harden Server (Hide Tokens) |
| 9 | Restrict SSH to My IP |
| 10 | Website Live on Public IP |

---

## 4. Real World Impact:
- Quick hosting of websites for small businesses or startups
- Development/testing environment deployment
- Educational platforms and hackathon submissions

---

## 5. Corporate Impact:
- Fast project setup for MVP (Minimum Viable Products)
- Low cost, highly flexible cloud hosting
- Secure, controlled environment for applications

---

## 6. Future Scope:
- Attach Load Balancer (ELB)
- Set up Auto Scaling Groups
- Implement SSL Certificates for HTTPS
- Infrastructure as Code using Terraform

---

## 7. Key AWS Services Involved:
- EC2 (Elastic Compute Cloud)
- VPC (Virtual Private Cloud)
- Security Groups
- IAM (for key management)

---

## 8. Architecture Diagram:

![Thumbnail](https://github.com/user-attachments/assets/f87c4351-cd9a-45c6-b801-e60fd5ea1042)

---

## 9. Screenshots:
- ### EC2 launch success

![5](https://github.com/user-attachments/assets/690a294f-a53c-4256-af90-f1dab5f11797)

---

- ### - Connect to Server & Install Apache Web Server

![6](https://github.com/user-attachments/assets/15cfa5d5-cb3e-44ef-bf26-556f97ce39f4)

![7](https://github.com/user-attachments/assets/b53afd42-5747-422a-8331-9921148baa59)

---

### - Website Script

![8](https://github.com/user-attachments/assets/ad51ec5d-e911-4961-896a-5df4d685cdfa)

---

### - Custom website page live

![9](https://github.com/user-attachments/assets/84e7c683-d39a-4ac5-8d26-2a721f2554c0)

---

### - Secure EC2 & Apply Best Practices

![13](https://github.com/user-attachments/assets/532295d2-3d89-48de-a371-fa80739c4a65)

---

![14](https://github.com/user-attachments/assets/0c2729fc-89b5-42b6-898c-81a793ddf5b4)

---

![15](https://github.com/user-attachments/assets/c5dc2293-e7a6-49ae-ae86-278316099306)

---

# Conclusion
This project lays the foundation for scalable, secure, and cost-effective cloud architectures on AWS. It is the first essential step towards building complex, enterprise-grade infrastructures.
