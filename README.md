# Table of Contents

1. [📌 Introduction](#introduction)  
2. [☁️ Cloud Providers](#cloud-providers)  
3. [🐳 Dockerizing Application](#dockerizing-application)  
    - [🖼️ Built Images](#built-images)  
    - [🚀 Running Containers on Server](#running-containers-on-server)  
4. [🌐 NGINX Configuration](#nginx-configuration)  
5. [⚙️ Jenkins CI/CD](#jenkins-cicd)  
    - [🔁 Workflow for Frontend and Backend](#workflow-for-frontend-and-backend)  
    - [🚀 Deploying the Application for Frontend and Backend](#deploying-the-application-for-frontend-and-backend)  

---

## 📌 Introduction

The application is deployed on [whisper.webredirect.org](https://whisper.webredirect.org/).  

**Note:** The application server is currently turned off.  

You can find the work on the front end and back end in the respective repositories and branches:  

- **Front End**:  
  - Repository: [Front End Repository](https://github.com/GramBelleg/Whisper_FrontEnd)  
  - Branch: `production`  

- **Back End**:  
  - Repository: [Back End Repository](https://github.com/GramBelleg/Whisper_BackEnd.git)  
  - Branch: `production`  

**Note:** The files in this repository are the same as those in the other repositories. They are included here for easy access.

---

## ☁️ Cloud Providers

The application utilizes two Azure VMs:  
- One dedicated to the application.  
- One dedicated to Jenkins for continuous integration and continuous deployment (CI/CD).  

---

## 🐳 Dockerizing Application

This project is fully containerized using Docker, with Docker Compose simplifying the deployment process.

### 🖼️ Built Images

- **Frontend**: Handles the user interface and client-side logic.  
- **Backend**: Manages the server-side logic and database interactions.  
- **Jenkins**: Manages the continuous integration and continuous deployment (CI/CD) process.  

All these images are pushed to Docker Hub for easy access and deployment. You can find them here: [Docker Hub](https://hub.docker.com/u/grambell003).  

### 🚀 Running Containers on Server

Below is the list of containers running on the application server:  

- **Frontend**: The built image for handling the user interface and client-side logic.  
- **Backend**: The built image for managing server-side logic and database interactions.  
- **Redis**: Utilized for caching to enhance application performance.  
- **Fluentd**: Responsible for collecting and managing logs.  

Below is the list of containers running on the Jenkins server:  

- **Jenkins**: The built image for handling the CI/CD process.  

---

## 🌐 NGINX Configuration

NGINX acts as a reverse proxy and web server for the application. It handles incoming requests and routes them as follows:  
- Requests starting with `/api` or `/socket.io` are routed to the **backend container**.  
- All other requests are served by the **frontend container**.  

This setup ensures seamless communication between the frontend and backend while serving static assets efficiently.

---

## ⚙️ Jenkins CI/CD

### 🔁 Workflow for Frontend and Backend

1. **Pull Request Creation**:  
   - A pull request is created to merge changes into the `production` branch.  
   - This triggers a workflow that builds the application and runs automated tests to ensure functionality and stability.  

   ![image](https://github.com/user-attachments/assets/2d0dc4c6-7781-4aaf-acdb-7e49a0fbc31a)  

2. **Merge and Deployment**:  
   - Once the pull request is approved and merged into the `production` branch:  
     - The pipeline pushes the updated application image to Docker Hub.  
     - A deployment script is triggered, which deploys the new image to the application server.  

   ![image](https://github.com/user-attachments/assets/60ed01fc-b834-4d86-99e4-493fb0b165b6)  

### 🚀 Deploying the Application for Frontend and Backend

Both the frontend and backend have two scripts for deployment:  

- **Deploy Script**: This script runs on the Jenkins machine and SSHs into the application server.  
- **Remote Deploy Script**: This script runs on the application server to pull the updated image and restart the service.  

---
