# Table of Contents

1. [Introduction](#introduction)
2. [Cloud Providers](#cloud-providers)
3. [Dockerizing Application](#dockerizing-application)
    - [Built Images](#built-images)
    - [Running Containers on Server](#running-containers-on-server)
    - [Docker Commands](#docker-commands)
4. [Jenkins CICD](#jenkins-cicd)
    - [Workflow for Frontend and Backend](#workflow-for-frontend-and-backend)
    - [Deploying the Application for Frontend and Backend](#deploying-the-application-for-frontend-and-backend)
5. [References](#references)

## Introduction

The application is deployed on [whisper.webredirect.org](https://whisper.webredirect.org/). NOTE: this is a sample application and it is not done yet.
You can find my work on the front end and back end in the respective repositories and branches.

- **Front End**: [Front End Repository](https://github.com/GramBelleg/Whisper_FrontEnd) - Branch: `frontend-branch`
- **Back End**: [Back End Repository](https://github.com/GramBelleg/Whisper_BackEnd.git) - Branch: `backend-branch`

## Cloud Providers

The application utilizes two Azure VMs:
- One dedicated to the application.
- One dedicated to Jenkins for continuous integration and continuous deployment (CICD).

## Dockerizing Application

This project is fully containerized using Docker, with Docker Compose simplifying the deployment process.

### Built Images

- **Frontend**: Handles the user interface and client-side logic.
- **Backend**: To Manages the server-side logic and database interactions.

All these images are pushed to Docker Hub for easy access and deployment. You can find them here:[go to dockerhub](https://hub.docker.com/u/grambell003).


### Running Containers on Server

Below is the list of containers running on the application server:

- **Frontend**: The built image for handling the user interface and client-side logic.
- **Backend**: The built image for managing server-side logic and database interactions.
- **Redis**: Utilized for caching to enhance application performance.

Below is the list of containers running on the jenkins server:

- **jenkins**:The built image for handling CICD process.

### Docker Commands

To build, run, and push the Docker images for the services, use the following commands:

- **Build**: `docker-compose build <service>`
- **Run**: `docker-compose run <service>`
- **Push**: `docker-compose push <service>`

## Jenkins CICD

### Workflow for Frontend and Backend

1. A pull request to request merging on the production branch will trigger the workflow that will build the application and run tests.
2. Upon merging the pull request into the production branch, the pipeline pushes the updated application image to Docker Hub and triggers a deployment script, which deploys the new image to the application server.

### Deploying the Application for Frontend and Backend

both the frontend and backend have two scripts for deployment:

- `Deploy Script`: This script runs on the Jenkins machine and SSHs into the application server.
- `Remote Deploy Script`: This script runs on the application server to pull the updated image and restart the service.

## References:

For Jenkins with Docker, the Dockerfile found on the [official Jenkins Docker installation documentation](https://www.jenkins.io/doc/book/installing/docker/) is used to build the Jenkins Docker image.

For detailed instructions on installing Docker and Docker Compose, refered to this [guide](https://support.netfoundry.io/hc/en-us/articles/360057865692-Installing-Docker-and-docker-compose-for-Ubuntu-20-04).

To configure NGINX with SSL and set up Certbot for obtaining certificates, we used this [repository](https://github.com/dimzrio/docker-compose/tree/master/nginx-ssl-letsencrypted) as a reference guide.

