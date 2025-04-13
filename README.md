
```markdown
# ✈️ **TravelMemory** 🌍 - MERN Stack Deployment Project

![Live](![image](https://github.com/user-attachments/assets/db98f8d7-4d61-4efb-9b94-4912d1cba322)
)
![EC2](https://img.shields.io/badge/Infrastructure-AWS%20EC2%20Cloud%20Power-F7A800)
![Performance](https://img.shields.io/badge/Performance-Optimized%20for%20Scalability-F9A825)
![Security](https://img.shields.io/badge/Security-HTTPS%20via%20Cloudflare-00C8FF)
![Version](https://img.shields.io/badge/Version-v1.0%20Release-6A4E92)

> A fully functional and scalable MERN stack application deployed on AWS EC2 with load balancing and domain mapping via Cloudflare. 💻🌐

---

## 📖 **Project Overview**

**TravelMemory** lets users capture and store their favorite travel moments, built using the **MERN stack**:

- 🧠 **MongoDB**
- 🛠️ **Express.js**
- ⚛️ **React.js**
- 🚀 **Node.js**

The challenge? Deploy the app on AWS, set up a reverse proxy, load balancing, and connect a custom domain using **Cloudflare**. Ready? Let’s fly! 🚁

---

## 🎯 **Objectives**

- ⚙️ Deploy backend (Node.js) to EC2
- 🎨 Configure frontend (React) for production
- 🔁 Enable frontend-backend communication
- 📦 Setup Nginx as a reverse proxy
- 📈 Enable load balancing across instances
- 🌐 Connect to a custom domain via Cloudflare
- 📘 Document every step with clarity & screenshots
- 🗺️ Create a deployment architecture diagram

---

## 🧱 **Project Structure**

```bash
TravelMemory/
│
├── backend/         # Node.js + Express API
│
├── frontend/        # React App
│
└── README.md        # 📚 You are here!
```

---

## 🛠️ **Backend Setup**

### 🔁 **Clone and Navigate**

```bash
git clone https://github.com/UnpredictablePrashant/TravelMemory.git
cd TravelMemory/backend
```

### 📦 **Install Dependencies**

```bash
npm install
```

### 🔐 **Configure `.env`**

```env
PORT=3000
MONGO_URI=your_mongodb_connection_string
```

### 🚀 **Run Backend**

```bash
node index.js
```

### 🌐 **Nginx Reverse Proxy**

Install and configure Nginx:

```bash
sudo apt install nginx
```

Edit `/etc/nginx/sites-available/default`:

```nginx
server {
  listen 80;
  location / {
    proxy_pass http://localhost:3000;
    ...
  }
}
```

Restart:

```bash
sudo systemctl restart nginx
```

📸 **[Screenshot: Backend running with Nginx]**

---

## 💻 **Frontend Setup**

### 🛤️ **Navigate to Frontend**

```bash
cd ../frontend
```

### 🧭 **Update API Base URL**

In `src/api/urls.js`:

```js
export const BASE_URL = "http://your-ec2-ip-or-domain.com";
```

### 📦 **Install and Build**

```bash
npm install
npm run build
```

### 🌍 **Serve with Nginx**

```bash
sudo mv build /var/www/travelmemory
```

Update Nginx:

```nginx
root /var/www/travelmemory;
location / {
  try_files $uri /index.html;
}
```

📸 **[Screenshot: Frontend live]**

---

## 📊 **Load Balancing with Auto Scaling**

1. ✅ **Create Launch Template**
2. 🟢 **Add Target Group**
3. ⚖️ **Configure Load Balancer**
4. 🔁 **Setup Auto Scaling Group**

📸 **[Screenshot: Load Balancer and Instances]**

---

## 🌐 **Domain Setup with Cloudflare**

1. 🔗 **Point your domain to Cloudflare**
2. 🟠 **Create A record (for EC2 IP)**
3. 🟣 **Create CNAME record (for Load Balancer endpoint)**

📸 **[Screenshot: Cloudflare DNS Settings]**

---

## 🗺️ **Architecture Diagram**

> Visualize the infrastructure flow from user to backend!

📌 **[Click to view full-size diagram]**
![Deployment Architecture](./architecture-diagram.png)

---

## 📂 **Final Output**

✅ **Live Site**: [http://yourdomain.com](http://yourdomain.com)  
✅ **Database connected**  
✅ **Fully scalable with load balancing**  
✅ **Domain mapped with HTTPS via Cloudflare**

📸 **[Screenshot: Final App Running]**

---

## 🧾 **Documentation Includes**

- ✅ **Step-by-step terminal commands**
- ✅ **Full `.env` and nginx config examples**
- ✅ **Screenshots at every critical step**
- ✅ **Architecture diagram (draw.io style)**

![image](https://github.com/user-attachments/assets/f374b793-1202-41fb-9344-ea7fc6c89aca)

---

## 👨‍💻 **Author**

Made with 💙 by [UnpredictablePrashant](https://github.com/UnpredictablePrashant)

---

## 📜 **License**

This project is licensed under the MIT License.

---
```

### Key Changes:
- Updated badges with a fresh, creative design that focuses on status, performance, security, and version.
- Cleaned up the content to fit well with the new badges and ensure the README stays visually appealing.
- Incorporated **screenshots** and **interactive content** suggestions (like architecture diagrams and clickable links).
  
This should make your README look both professional and engaging. Let me know how you like this version!
