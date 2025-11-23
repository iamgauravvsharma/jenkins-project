Jenkins CI/CD Pipeline – Complete Guide (Beginner to Mid-Level)

This project demonstrates a complete CI/CD pipeline using Jenkins, covering code checkout, build, test, Docker image creation, and deployment. Suitable for freshers and DevOps beginners to showcase practical skills.


---

📌 Overview

This repository contains:

A sample application (Node.js/Java)

Jenkinsfile for CI/CD pipeline

Dockerfile for image creation

Deployment scripts (Ansible/Kubernetes optional)

Architecture diagrams


This project helps you understand how modern CI/CD pipelines are built and automated.


---

🎯 Key Features

Automated CI (Build + Test)

Automated CD (Docker build + push)

Webhook-based continuous integration

Notification steps

Supports containerized deployment

Reusable pipeline structure

Works with GitHub, DockerHub, AWS EC2, Kubernetes, etc.



---

🛠 Tools & Technologies Used

Jenkins (Pipeline + Webhooks)

GitHub

Docker

Node.js / Java application

DockerHub (registry)

Ansible / Kubernetes (optional deployment)



---

🧱 Project Structure

project/
│
├── app/
│   ├── src/
│   ├── package.json / pom.xml
│   └── index.js / Main.java
│
├── Jenkinsfile
├── Dockerfile
├── ansible/
│   └── deploy.yml (optional)
│
├── k8s/
│   ├── deployment.yaml (optional)
│   └── service.yaml
│
└── diagrams/
    ├── architecture.png
    └── pipeline-flow.png


---

🚀 Pipeline Architecture

1. Developer Pushes Code → GitHub


2. GitHub Webhook → Triggers Jenkins


3. Jenkins Pipeline Executes:

Clone repo

Install dependencies

Run tests

Build application

Build Docker image

Push to DockerHub

Deploy using Ansible/K8s





---

🧪 Sample Jenkinsfile (Declarative Pipeline)

pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/your/repo.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'   // For Node.js
                // sh 'mvn clean install'  // For Java
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t yourdockeruser/app:latest .'
            }
        }

        stage('Docker Push') {
            steps {
                sh 'docker push yourdockeruser/app:latest'
            }
        }

        stage('Deploy') {
            steps {
                sh 'ansible-playbook ansible/deploy.yml'
                // OR: sh 'kubectl apply -f k8s/'
            }
        }
    }

    post {
        success { echo 'Pipeline completed successfully!' }
        failure { echo 'Pipeline failed!' }
    }
}


---

🧱 Dockerfile

FROM node:18
WORKDIR /app
COPY . .
RUN npm install
CMD ["npm", "start"]


---

📦 Deployment (Ansible Example)

- hosts: webserver
  tasks:
    - name: Pull latest Docker image
      shell: docker pull yourdockeruser/app:latest

    - name: Stop old container
      shell: docker rm -f app || true

    - name: Run new container
      shell: docker run -d --name app -p 3000:3000 yourdockeruser/app:latest


---

📌 How to Run This Project

1. Clone Repo

git clone https://github.com/your/repo.git

2. Setup Jenkins

Install Pipeline plugin

Install Git plugin

Install Docker pipeline


3. Add Credentials

DockerHub username/password

SSH key for server (if deploying)


4. Add Webhook in GitHub

http://your-jenkins-server/github-webhook/

5. Run Pipeline

Create Pipeline job in Jenkins

Add Jenkinsfile from SCM

Build now



---

📚 What You Learn from This Project

Basics of CI/CD

Jenkins pipeline scripting

Docker-based build and deployment

GitHub webhooks

Production-like automation



---

⭐ This Project Helps You Crack Interviews

Recruiters look for: ✔ CI/CD automation ✔ Docker knowledge ✔ Jenkinsfile scripting ✔ Real-world deployment experience ✔ GitHub project quality


---

📞 Contact / Connect

If you want more Jenkins, Docker, Kubernetes full projects — you can connect anytime.
