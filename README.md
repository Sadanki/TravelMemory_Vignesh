Here’s the updated version of your setup based on the provided scripts:

---

# ✈️ **TravelMemory** – Fullstack Deployment on AWS

This project deploys a **MERN stack** travel memory application using **AWS** services like EC2, ALB, ASG, Target Groups, and **Cloudflare** for security and DNS.

---

## 📁 **Folder Structure**

```bash
TravelMemory/
│
├── backend/              # Node.js Express backend
├── frontend/             # Vite + React frontend
├── setup-backend.sh      # Backend provisioning script (Auto Scaling)
└── setup-frontend.sh     # Frontend EC2 static deployment script
```

---

## ⚙️ **Prerequisites**

Before deploying this application, ensure the following:

- ✅ **A valid AWS account** with permissions to create EC2, ALB, ASG, and Target Groups
- ✅ **Domain access** via Cloudflare (e.g., `frontend.mytravelapp.xyz` and `api.mytravelapp.xyz`)
- ✅ **MongoDB Atlas** cluster (URI needed in backend `.env`)
- ✅ **Security group rules** allowing HTTP (80), HTTPS (443), and backend port (3001)
- ✅ **Ubuntu-based EC2 AMI** with internet access for installing dependencies

---

## 🛠 **Installation Instructions**

### 📦 **Required Services**
Ensure the following packages are installed on your EC2 instances:

- **Nginx** – Reverse proxy for both backend and frontend
- **Node.js v22** – JavaScript runtime environment for backend and Vite frontend build
- **PM2** – Process manager for running the backend as a service

---

### 🧪 **PM2 Common Commands**

```bash
# Start your backend application using PM2
pm2 start index.js --name "travel-memory-backend"

# View all running PM2 processes
pm2 list

# View logs for a specific process
pm2 logs travel-memory-backend

# Restart a process by name
pm2 restart travel-memory-backend

# Stop a process
pm2 stop travel-memory-backend

# Delete a process from PM2
pm2 delete travel-memory-backend

# Save process list to start on reboot
pm2 save

# Re-generate startup script after reboot
pm2 startup
```

---

## 🔧 **Backend Setup Script**

```bash
#!/bin/bash

# === System Update ===
apt-get update -y

# === Install Node.js v22 ===
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
apt-get install -y nodejs

# === Install Nginx ===
apt-get install -y nginx git

# === Clone Backend Repo to /home/ubuntu ===
cd /home/ubuntu
chmod -R 775 /home/ubuntu/
git clone -b Backend https://github.com/Sadanki/TravelMemory_Vignesh.git
cd TravelMemory_Vignesh

# === Create .env File ===
echo "PORT=3001" > .env
echo "MONGO_URI=mongodb+srv://Sadankae:vhAAs6NPDdwRJG8r@vigneshcluster.i1j9i.mongodb.net/?retryWrites=true&w=majority&appName=VigneshCluster" >> .env

# === Install App Dependencies & PM2 ===
npm install -y
npm install -g pm2 -y
pm2 start index.js --name "travel-memory-backend"
pm2 startup
pm2 save

# === Configure Nginx ===
rm -f /etc/nginx/sites-enabled/default

bash -c 'cat > /etc/nginx/sites-available/travel-memory << EOF
server {
    listen 80;
    server_name api.mytravelapp.xyz;

    location / {
        proxy_pass http://localhost:3001;
        proxy_http_version 1.1;
        proxy_set_header Upgrade \$http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host \$host;
        proxy_cache_bypass \$http_upgrade;
    }
}
EOF'

ln -s /etc/nginx/sites-available/travel-memory /etc/nginx/sites-enabled/
nginx -t
systemctl restart nginx

echo "✅ TravelMemory backend is live at api.mytravelapp.xyz"
```

---

## 🧩 **Frontend Setup Script**

```bash
#!/bin/bash

# === System Update ===
apt-get update -y

# === Install Node.js v22 ===
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
apt-get install -y nodejs

# === Install Nginx & Git ===
apt-get install -y nginx git

# === Clone Frontend Repo to /home/ubuntu ===
cd /home/ubuntu
chmod -R 775 /home/ubuntu/
git clone -b Frontend https://github.com/Sadanki/TravelMemory_Vignesh.git
cd TravelMemory_Vignesh

# === Create .env for Vite ===
echo "VITE_API_BASE_URL=http://api.mytravelapp.xyz" > .env

# === Install Dependencies & Build ===
npm install -y
npm run build

# === Copy Build Output to /var/www/html ===
rm -rf /var/www/html/*
cp -r dist/* /var/www/html/

# === Configure Nginx for Static Site ===
rm -f /etc/nginx/sites-enabled/default

bash -c 'cat > /etc/nginx/sites-available/travel-memory-ui << EOF
server {
    listen 80;
    server_name frontend.mytravelapp.xyz;

    root /var/www/html;
    index index.html;

    location / {
        try_files \$uri \$uri/ /index.html;
    }
}
EOF'

ln -s /etc/nginx/sites-available/travel-memory-ui /etc/nginx/sites-enabled/
nginx -t
systemctl restart nginx

echo "✅ TravelMemory frontend is deployed at: frontend.mytravelapp.xyz"
```

---

## 🧱 **Deployment Architecture Diagram**

> **TravelMemory AWS Architecture**
> ![image](https://github.com/user-attachments/assets/b0f494f3-89ff-4e31-aec1-40718960529a)


### ⚙️ **Backend Deployment Flow (AWS)**

1. **Launch Templates**
   - Launch Template 1
   - Launch Template 2

2. **Target Groups**
   - Target Group 1
   - Target Group 2
   - Target Group 3

3. **Application Load Balancer (ALB)**
   - ALB 1
   - ALB 2
   - ALB 3
   - ALB 4
   - ALB 5

4. **Auto Scaling Groups (ASG)**
   - ASG 1
   - ASG 2
   - ASG 3

5. **Cloudflare – Add CNAME for api.mytravelapp.xyz**
   - Cloudflare CNAME

### 🌐 **Frontend Deployment Flow**

1. **EC2 Instance**
   - EC2 Frontend 1
   - EC2 Frontend 2

2. **Cloudflare – Add A Record**
   - Cloudflare A Record

3. **Application Running → frontend.mytravelapp.xyz**
   - Frontend Live
OutPut:
![image](https://github.com/user-attachments/assets/f4ce83ab-be20-4441-a153-d5ad822ccf57)

Json
![image](https://github.com/user-attachments/assets/392045ad-eaca-4089-8f84-a47c0eef4ec1)


---

## 📜 **License**

This project is open-source and available for educational, practice, and real-world development guidance. You are free to use, modify, and distribute this project for **non-commercial and commercial purposes**.

---

## 🙏 **Thank You**

We appreciate your interest in the **TravelMemory** project.

---

This updated README now includes your specific repository names, API URLs, and other setup details. It should work well for your TravelMemory deployment. Let me know if you need any further adjustments!
