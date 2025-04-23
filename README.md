# workshop-code



# 🚀 Deploying `workshop-code` on an Amazon Linux 2 EC2 Instance with Apache HTTPD

Follow this concise, battle‑tested guide to serve the contents of **[`Ekangaki/workshop-code`](https://github.com/Ekangaki/workshop-code.git)** from an EC2 instance running Amazon Linux 2 and Apache.

---

## Prerequisites
| Requirement | Details |
|-------------|---------|
| **AWS Account** | Permission to create EC2 instances, security groups, and key pairs. |
| **SSH Key Pair** | `.pem` file to access the instance. |
| **Security Group** | Inbound **TCP 22** (SSH) & **TCP 80** (HTTP) open to your IP / world. |
| **GitHub Repo** | `https://github.com/Ekangaki/workshop-code.git` |

---

## 1  Launch an Amazon Linux 2 Instance
1. **AWS Console → EC2 → Launch Instance**  
2. Choose **Amazon Linux 2 AMI** (x86_64 or arm64).  
3. Select instance type (e.g., **t2.micro** for demo).  
4. Attach your **SSH key pair**.  
5. **Security Group** → allow **22** & **80**.  
6. Click **Launch** and note the **public IP**.

---

## 2  SSH Into the Instance
```bash
ssh -i /path/to/key.pem ec2-user@<PUBLIC_IP>


3  Update OS & Install Packages
# Update package index and apply patches
sudo yum update -y

# Install Apache HTTPD and Git
sudo yum install -y httpd git

# Install Apache HTTPD and Git
sudo yum install -y httpd git

## 4  Start & Enable Apache
sudo systemctl start httpd
sudo systemctl enable httpd   # auto‑start on reboot

## 5  Clone & Deploy the Code
# Clean the default docroot
sudo rm -f /var/www/html/*

# Clone repo to /tmp
cd /tmp
git clone https://github.com/Ekangaki/workshop-code.git

# Copy site content into Apache docroot
sudo cp -r workshop-code/* /var/www/html/

## 6  Set Correct Permissions (Optional)
sudo chown -R ec2-user:ec2-user /var/www/html
sudo find /var/www/html -type d -exec chmod 755 {} \;
sudo find /var/www/html -type f -exec chmod 644 {} \;

## 7  Verify in Browser
Open http://<PUBLIC_IP>/ — you should now see your workshop‑code site live!

