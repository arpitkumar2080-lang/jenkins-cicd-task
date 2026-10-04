# jenkins-cicd-task


AWS DevOps CI/CD Pipeline (Jenkins, Docker & Nginx)
This repository contains a complete automated CI/CD pipeline built for deploying a web application on an AWS EC2 instance using Jenkins, Docker, and Nginx.

Author: ARPIT KUMAR

Target Role: AWS Cloud Support Engineer

🚀 Project Overview
The goal of this project is to automate the software release process. Whenever code is pushed to this GitHub repository, Jenkins automatically checks out the code, builds a custom Docker image containing the application, and deploys it as a running container on an AWS EC2 instance.

🛠️ Architecture & Tech Stack
Cloud Provider: AWS EC2 (Ubuntu / Linux)

CI/CD Orchestrator: Jenkins (Running on port 8080)

Containerization: Docker & Dockerfile

Web Server: Nginx (Alpine-based container)

Version Control: GitHub

📁 Project Structure
Plaintext
jenkins-cicd-task/
├── Jenkinsfile         # Declarative pipeline script defining CI/CD stages
├── Dockerfile          # Instructions to build the custom Nginx Docker image
└── index.html          # Source web page displaying deployment details
⚙️ Configuration Files
1. Jenkinsfile
The declarative pipeline script automates the checkout, build, and deployment phases:

Groovy
pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/arpitkumar2080-lang/jenkins-cicd-task.git'
            }
        }
        stage('Build Image') {
            steps {
                sh 'docker build -t my-devops-app .'
            }
        }
        stage('Deploy App') {
            steps {
                sh 'docker rm -f my-app-container || true'
                sh 'docker run -d -p 80:80 --name my-app-container my-devops-app'
            }
        }
    }
}
2. Dockerfile
The Docker configuration uses a lightweight Nginx web server to serve the HTML file:

Dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/
EXPOSE 80
3. index.html
The deployment verification web page:

HTML



    CI/CD Deployment

CI/CD Pipeline Successfully Deployed! This automated deployment was set up by ARPIT KUMAR. Target Role: AWS Cloud Support Engineer

🔄 CI/CD Pipeline Workflow
Trigger: The build is initiated manually via Jenkins ("Build Now") or automatically via GitHub Webhooks.

Checkout SCM: Jenkins pulls the latest source code from the GitHub repository.

Docker Build: Executes docker build to package index.html inside the Nginx alpine image (my-devops-app).

Docker Deploy: Stops and removes any existing container (my-app-container) and launches a new container mapping port 80 to host port 80.

🔧 Troubleshooting & Performance Tuning (AWS Free-Tier EC2)
During the setup on an AWS Free-Tier EC2 instance, resource constraints (such as disk/temp space warnings) caused Jenkins built-in nodes to go temporarily offline.

Fix Applied: Configured Jenkins Node Monitoring (Manage Jenkins -> Nodes -> Configure Monitors) by enabling "Don't mark agents temporarily offline" for disk and temp space. This ensures uninterrupted pipeline execution on lightweight instances.

📸 Deployment Proof
Pipeline Status: SUCCESS (Verified in Jenkins Console Output)

Live Access: Accessible via the AWS EC2 Public IP (http://)
