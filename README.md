# Altschhol-2nd-Sem-Exam-Proj
A dynamic landing page hosted on AWS with Nginx.
# 🌾 The Future of Smart Agriculture Platforms

This repository contains the files and deployment documentation for a cloud-hosted dynamic web application. The app showcases a professional landing page and a Node.js backend, both hosted on an AWS EC2 Ubuntu instance using Nginx as a reverse proxy.

Author: Anighoro Gabriel Oghenetega  
Date: June 2025  
Role: Lead Cloud Engineer

We’re creating an intelligent ecosystem that empowers farmers with real-time crop insights, AI-driven forecasts, and cloud-based automation. Our platform is set to redefine how agriculture and technology connect across rural and urban landscapes.

---
## Technologies Used

- **AWS EC2 (Ubuntu 22.04)**
- **Nginx** (Reverse proxy + static file server)
- **Node.js + Express**
- **PM2** (Node.js process manager)
- **Tailwind CSS** (for UI styling)
- **HTML, CSS, JavaScript**

---
## Project Structure

├── index.html # Static landing page
├── app.js # Node.js backend server
├── nginx-site.conf # Nginx configuration
├── ecosystem.config.js # PM2 process config
├── screenshot.png # Screenshot of rendered page
└── README.md # This file

---

## Live Page

- **Public IP:** http://52.90.245.137

---

## Screenshot

![Screenshot of Hosted Page](./screenshot.png)

---

## Deployment Process

### Step 1 – Launch EC2 Instance
- Chose **Ubuntu 22.04** as the OS
- Allowed traffic on ports 22 (SSH), 80 (HTTP), and 443 (HTTPS)
- Connected using:
  ```bash
  ssh -i "your-key.pem" ubuntu@52.90.245.137
  Step 2 – Install Nginx

sudo apt update
sudo apt install nginx -y

Step 3 – Install Node.js and PM2

sudo apt install nodejs npm -y
sudo npm install -g pm2

Created a simple app.js backend:

const express = require('express');
const app = express();
app.get('/api', (req, res) => res.send('Hello from the backend!'));
app.listen(3000, () => console.log('Server running on port 3000'));

Started it with PM2:

pm2 start app.js
pm2 startup
pm2 save

Step 4 – Configure Nginx

Opened Nginx config:

sudo nano /etc/nginx/sites-available/default

Edited to add reverse proxy config:

location /api {
    proxy_pass http://localhost:3000;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
}

Saved and reloaded:

sudo systemctl reload nginx

Step 5 – Copy HTML Landing Page

Used a simple landing page with Tailwind CSS showing:

    Your name and title

    Project title and short pitch

    About Me bio

    “Connect with Me” button

Saved it as index.html and placed it in:

sudo cp index.html /var/www/html/index.html

Errors Made & Fixes
Error	Cause	Fix
Permission denied (publickey)	Forgot SSH key	Used correct .pem file with -i
Nginx 403 Forbidden	Wrong file path	Placed HTML file inside /var/www/html
Node.js stopped after logout	No process manager	Installed and configured PM2
Nginx not routing /api	Didn't reload after changes	Used sudo systemctl reload nginx
PM2 app not auto-starting	Didn't run startup config	Used pm2 startup and pm2 save
About Me

I'm a cloud-first engineer passionate about building secure, scalable web infrastructure. I’ve deployed production-ready apps using AWS EC2, S3 for static site hosting, Route 53 for DNS, and IAM for access management. My focus is combining automation and simplicity in solutions that solve real-world problems.
Contact

    GitHub: https://github.com/Gabriel15-dev

    Email: gabrielanighoro@gmail.com
