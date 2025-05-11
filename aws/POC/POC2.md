# 💡 POC Document: Jenkins Setup and Troubleshooting on AWS EC2

---

# 1. 🌟 POC Statement

> **Objective**: Deploy a fully operational Jenkins Continuous Integration server on an AWS EC2 instance (Amazon Linux 2), ensuring the system runs cleanly, securely, and resolving any issues encountered during setup.

---

# 2. 📚 Initial Setup Journey

## 2.1 Launching EC2 Instance

* **AMI**: Amazon Linux 2
* **Instance Type**: t2.medium (recommended)
* **Security Group Ports Opened**:

  * SSH (22) - for connecting via terminal
  * HTTP (80) - basic web access
  * Custom TCP (8080) - Jenkins web access

## 2.2 Connecting and Preparing Environment

* SSH into instance:

  ```bash
  ssh -i your-key.pem ec2-user@your-instance-public-ip
  ```
* Updated system packages:

  ```bash
  sudo yum update -y
  ```
![2](https://github.com/user-attachments/assets/9aecc04f-cb38-4b91-9e15-a7904ba5490d)

---

## 2.3 Java Installation

* Initially installed **Java 11**:

  ```bash
  sudo amazon-linux-extras enable corretto11
  sudo yum install java-11-amazon-corretto -y
  ```
* Verified Java version:

  ```bash
  java -version
  ```
![3](https://github.com/user-attachments/assets/eb52543f-ee12-4fc7-8369-a39963437129)

---

## 2.4 Jenkins Installation

* Added Jenkins repo and GPG key:

  ```bash
  sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
  sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
  ```

* Installed Jenkins:

  ```bash
  sudo yum install jenkins -y
  ```

* Attempted to start Jenkins:

  ```bash
  sudo systemctl start jenkins
  ```
![4](https://github.com/user-attachments/assets/91e3299d-3578-48a7-bbfb-21c431c6ec39)

---

# 3. 💣 Challenge Encountered

When starting Jenkins:

```
Job for jenkins.service failed because the control process exited with error code.
```

**Diagnosis:**

* Checked Jenkins service status:

  ```bash
  sudo systemctl status jenkins
  ```

* Observed repeated crashes.

* Checked detailed Jenkins logs:

  ```bash
  sudo journalctl -u jenkins -n 50 --no-pager
  ```
![5](https://github.com/user-attachments/assets/277c46f2-a39b-4453-9cd7-e3352bb22a5e)

---

**Root Cause Found:**

* Jenkins version **required Java 17 or higher**, but our system had **Java 11**.
* Error observed:

  > "Running with Java 11 ... older than the minimum required version (Java 17)."

---

# 4. 👩‍💻👨‍💻 Troubleshooting and Team Resolution

* Together, we realized the Java version mismatch.
* Planned to upgrade Java to Amazon Corretto 17.

## 4.1 Java Upgrade Steps

* Installed Java 17:

  ```bash
  sudo yum install java-17-amazon-corretto-devel -y
  ```
* Switched default Java version:

  ```bash
  sudo alternatives --config java
  ```
* Verified Java 17:

  ```bash
  java -version
  ```
  
![6](https://github.com/user-attachments/assets/1f2fac59-a23f-4226-9b2d-07af4432f151)

---

## 4.2 Restarting Jenkins

* Reloaded daemon and restarted Jenkins:

  ```bash
  sudo systemctl daemon-reexec
  sudo systemctl restart jenkins
  ```
* Checked Jenkins status:

  ```bash
  sudo systemctl status jenkins
  ```

![7](https://github.com/user-attachments/assets/b919df5a-bcc4-4c3c-80f3-7e47a4e514d5)

---

**Result:**

* Jenkins service started successfully! 🚀

---

# 5. ✅ Final Setup

* Jenkins accessible at:

  ```
  http://your-ec2-public-ip:8080
  ```
  
![20](https://github.com/user-attachments/assets/673ee4d4-3a1f-40fb-9d50-bc0f93aa2af3)

* Retrieved initial admin password:

  ```bash
  sudo cat /var/lib/jenkins/secrets/initialAdminPassword
  ```
  
![21](https://github.com/user-attachments/assets/b7038de2-810b-4ee5-bcef-3ecf462b6c3d)

* Installed suggested plugins and created the first admin user.

---

# 6. 📊 Architecture Diagram

```plaintext
          +---------------------------+
          |         AWS EC2            |
          |---------------------------|
          | OS: Amazon Linux 2         |
          | Installed:                 |
          |  - Java 17 (Corretto)       |
          |  - Jenkins Server (8080)    |
          +---------------------------+
                    |
             [Inbound Rules]
             (Port 22: SSH)
             (Port 80: HTTP)
             (Port 8080: Jenkins)
                    |
               User Access
```

---

# 7. 👌 Conclusion

* Together, we **successfully built a Jenkins Server** from scratch on AWS EC2.
* We **faced real-world problems** (Java version mismatch) and **solved them smartly**.
* Final system is **running cleanly, securely, and ready for CI/CD pipelines**.

> This POC shows not just technical skill but strong troubleshooting and team collaboration.

---

## Medium : [medium.com/@vaibhavparekh097](https://medium.com/@vaibhavparekh097)
### X : [x.com/awswithvibes](https://x.com/awswithvibes)
### LinkedIn : [linkedin.com/in/vaibhav-parekh08](https://www.linkedin.com/in/vaibhav-parekh08/)


