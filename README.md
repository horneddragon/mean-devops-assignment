MEAN DEVOPS ASSIGNMENT


PROJECT OVERVIEW
----------------
This project is a full-stack MEAN CRUD application deployed using Docker, Docker Compose, Nginx, GitHub Actions CI/CD, and Google Cloud VM.

Frontend: Angular 15
Backend: Node.js + Express
Database: MongoDB
Reverse Proxy: Nginx
CI/CD: GitHub Actions
Cloud: Google Cloud Compute Engine
Containers: Docker + Docker Compose

The application allows users to:
- Create tutorials
- View tutorials
- Update tutorials
- Delete tutorials
- Search tutorials by title


ARCHITECTURE
------------
Browser -> Nginx (Port 80)
Nginx -> Angular Frontend
Nginx /api -> Node Backend -> MongoDB

All services run as Docker containers using docker-compose.


REPOSITORY STRUCTURE
--------------------
backend/
frontend/
nginx/
docker-compose.yml
.github/workflows/docker-ci.yml


LOCAL SETUP
-----------
Backend:
cd backend
npm install
node server.js
Runs on port 8080

Frontend:
cd frontend
npm install
ng serve
Runs on port 4200


DOCKER BUILD (LOCAL)
-------------------
docker build ./backend -t mean-backend
docker build ./frontend -t mean-frontend


DOCKER COMPOSE DEPLOYMENT
------------------------
docker compose up -d

This starts:
- MongoDB
- Backend
- Frontend
- Nginx reverse proxy

Application becomes accessible at:

http://<VM_PUBLIC_IP>


NGINX REVERSE PROXY
------------------
Configured in nginx/default.conf

Routing:
 /      -> Angular frontend
 /api   -> Node backend


CI/CD PIPELINE
--------------
Implemented using GitHub Actions.

Pipeline file:
.github/workflows/docker-ci.yml

On every push to main:

1. Checkout repository
2. Login to Docker Hub
3. Build backend Docker image
4. Push backend image to Docker Hub
5. Build frontend Docker image
6. Push frontend image to Docker Hub

Docker Hub credentials are stored in GitHub Actions secrets:

DOCKERHUB_USERNAME
DOCKERHUB_TOKEN


CLOUD DEPLOYMENT (GCP)
---------------------
Steps followed:

1. Created Ubuntu VM on Google Cloud
2. Installed Docker and Docker Compose
3. Cloned GitHub repository on VM
4. Pulled Docker images from Docker Hub
5. Deployed using docker-compose
6. Enabled firewall rule for port 80
7. Verified application using public IP

The VM can be stopped and restarted.
External IP is ephemeral and may change after restart.


SCREENSHOTS 
--------------------------------
screenshots/ci.png        -> <img width="1707" height="824" alt="image" src="https://github.com/user-attachments/assets/6d729163-e6cf-4ac6-8286-5090e7d130d7" />
screenshots/dockerhub.png -> <img width="1697" height="843" alt="image" src="https://github.com/user-attachments/assets/ce883435-0237-4d9c-b29c-0c4063a20128" />
screenshots/ui.png        -> <img width="1709" height="919" alt="image" src="https://github.com/user-attachments/assets/c51024c0-2e36-450e-9f59-c3c2cd5f078d" />
                             <img width="1706" height="825" alt="image" src="https://github.com/user-attachments/assets/443aa4d6-4236-45b2-a012-c4338cecff56" />
screenshots/vm.png        -> <img width="1363" height="826" alt="image" src="https://github.com/user-attachments/assets/c4d2d0b1-b2b6-4fc1-b226-ebf021dc313b" />
screenshots/dockerps.png -> <img width="1363" height="831" alt="image" src="https://github.com/user-attachments/assets/7091356b-5589-4eac-8be7-3733c62b0205" />



NOTES
-----
- MongoDB runs as Docker container
- Nginx exposes application on port 80
- CI/CD automatically builds and pushes images
- Deployment uses docker-compose on GCP VM
- Images are pulled from Docker Hub during deployment


END OF README
