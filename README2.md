# 🚀 Manual Deployment of Node.js Application on AWS EC2

## 📌 Project Overview

This project demonstrates the **manual deployment of a Node.js web application** on an AWS EC2 instance. The goal is to understand the core concepts of cloud deployment, server configuration, and reverse proxy setup without using automation tools.

The application includes a **file upload feature** built using Express.js and Multer, and is exposed to the internet securely using Nginx.

---

## 🧰 Tech Stack

* Cloud Platform: Amazon Web Services (AWS)
* Compute Service: EC2 (Ubuntu)
* Backend: Node.js (Express.js)
* File Upload Middleware: Multer
* Web Server: Nginx
* Version Control: Git & GitHub

---

## ⚙️ Steps Performed

### 1. EC2 Instance Setup

* Launched Ubuntu EC2 instance
* Configured security group:

  * Port 22 (SSH) → My IP
  * Port 80 (HTTP) → Anywhere
  * Port 3000 (Temporary for testing)

---

### 2. Connect to EC2

```bash
ssh -i your-key.pem ubuntu@your-public-ip
```

---

### 3. Install Dependencies

```bash
sudo apt update
sudo apt install nginx -y
sudo apt install git -y
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install nodejs -y
```

---

### 4. Clone Repository

```bash
git clone https://github.com/DevOpsInstituteMumbai-wq/AWS-EC2-instance.git
cd AWS-EC2-instance
```

---

### 5. Install & Run Application

```bash
npm install
node index.js
```

Access:

```
http://<EC2-Public-IP>:3000
```

---

### 6. Configure Nginx (Reverse Proxy)

Edit config:

```bash
sudo nano /etc/nginx/sites-available/default
```

Update:

```nginx
location / {
    proxy_pass http://localhost:3000;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
}
```

Restart Nginx:

```bash
sudo systemctl restart nginx
```

Access:

```
http://<EC2-Public-IP>
```

---

### 7. Process Management (PM2)

```bash
sudo npm install -g pm2
pm2 start index.js
pm2 save
```

---

## 📂 Application Features

* File upload functionality
* File type validation (jpg, png, pdf, gif)
* File size restriction (1MB)
* Files stored in `/uploads` directory

---

## 🔐 Security Best Practices

* Restricted SSH access to specific IP
* Used Nginx reverse proxy instead of exposing Node.js directly
* Removed port 3000 access after setup
* Implemented file validation and size limits

---

## 🧠 Key Learnings

* EC2 instance provisioning
* Linux server management
* Node.js deployment
* Reverse proxy using Nginx
* Handling file uploads securely
* Git & GitHub workflow

---

## 📸 Screenshots

(Add your screenshots here)

* EC2 instance running
* SSH connection
* Application running on port 3000
* File upload success
* Nginx working (port 80)

---

## 💬 Interview Explanation

"I deployed a Node.js application on an AWS EC2 instance, configured Nginx as a reverse proxy to expose the application securely, and implemented file upload functionality using Multer. I also ensured proper security practices by restricting ports and managing processes using PM2."

---

## 🔗 GitHub Repository

https://github.com/MustafaBalasinorwala91/ec2-nodejs-deployment

---

## 👨‍💻 Author

Mustafa Balasinorwala

---

