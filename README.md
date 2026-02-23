# MEAN DevOps Assignment – Full Stack Deployment

## 📌 Overview

This project demonstrates end-to-end DevOps implementation for a full-stack MEAN CRUD application using:

- MongoDB – Database  
- Express + Node.js – Backend REST API  
- Angular 15 – Frontend UI  
- Docker & Docker Compose – Containerization  
- Nginx – Reverse Proxy  
- GitHub + Docker Hub – Source & Image Registry  
- Google Cloud Platform (GCP) – Cloud Deployment  

The application manages Tutorials with full CRUD operations:
Create, Read, Update, Delete + Search by title.

Live deployment is hosted on a GCP VM.

---

## 🏗 Architecture

Browser  
↓  
Nginx (Port 80)  
↓  
Angular Frontend Container  
↓  
Node / Express Backend Container  
↓  
MongoDB Container  

All services run via Docker Compose on a GCP VM.

---

## ⚙️ Tech Stack

- Angular 15  
- Node.js + Express  
- MongoDB 6  
- Docker  
- Docker Compose  
- Nginx  
- GitHub  
- Docker Hub  
- Google Cloud Compute Engine  

---

## 📂 Repository Structure

.
├── backend  
│   ├── Dockerfile  
│   └── server.js  
├── frontend  
│   ├── Dockerfile  
│   └── src  
├── nginx  
│   └── default.conf  
├── docker-compose.yml  
└── README.md  

---

## 🚀 Local Setup

### Backend

cd backend  
npm install  
node server.js  

### Frontend

cd frontend  
npm install  
ng serve  

Open:

http://localhost:4200  

---

## 🐳 Docker Build

docker build -t mean-backend ./backend  
docker build -t mean-frontend ./frontend  

---

## 📦 Docker Hub

Images pushed:

- mean-backend  
- mean-frontend  

---

## 🧩 Docker Compose Deployment

docker-compose pull  
docker-compose up -d  

Verify:

docker ps  

---

## 🌐 Cloud Deployment (GCP)

Steps followed:

1. Created GCP VM (e2-medium)
2. Installed Docker + docker-compose
3. Cloned GitHub repo
4. Ran Docker Compose
5. Configured Nginx reverse proxy
6. Opened firewall for port 80
7. Accessed app publicly via VM External IP

Application available at:

http://<VM_EXTERNAL_IP>/tutorials  

---

## 🔁 Nginx Reverse Proxy

server {
  listen 80;

  location / {
    proxy_pass http://frontend:80;
  }

  location /api/ {
    proxy_pass http://backend:8080;
  }
}

Routes:

/ → Angular frontend  
/api → Node backend  

---

## 🧠 Challenges Faced & Solutions

### MongoDB connection refused
Cause: Mongo not running  
Fix: Added MongoDB container in Docker Compose  

---

### Angular dist folder not found
Cause: Wrong COPY path  
Fix:

COPY --from=build /app/dist/angular-15-crud /usr/share/nginx/html  

---

### Nginx API routing failed

Cause: Trailing slash stripped /api  

Fix:

proxy_pass http://backend:8080;  

---

### App not reachable publicly

Cause: GCP firewall blocking port 80  
Fix: Created ingress firewall rule allowing TCP 80  

---

### GitHub push authentication failed

Cause: Password auth deprecated  
Fix: Used GitHub Personal Access Token  

---

## ✅ Final Result

- Full MEAN stack deployed on cloud  
- Dockerized services  
- Nginx reverse proxy  
- Publicly accessible application  
- Code in GitHub  
- Images in Docker Hub  

---

## 📸 Screenshots (attach in repo)

- Application UI  
- docker ps  
- Docker Hub images  
- GitHub repository  
- GCP VM  
- Firewall rule  
- Nginx config  

---

## 👤 Author

Anirudha Puranic  
DevOps Intern Candidate  
GitHub: horneddragon
