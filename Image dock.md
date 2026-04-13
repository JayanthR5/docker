Experiment No: 6

Title: Create and Configure Jenkins Workflow to Build Python Application and Push Image

---

🎯 Aim

To create and configure Jenkins workflow to build a Python application and push the Docker image.

---

🧰 Requirements

- Jenkins 2.375.1 LTS (Windows)
- Python 3.x
- GitHub Account
- Docker Installed
- Python Program (simple.py)

---

📥 Installation Steps for Jenkins

Step 1: Download Jenkins

- Download Jenkins 2.375.1 LTS for Windows.
- Install Python 3.x.
- Install Docker Desktop.

---

Step 2: Configure Jenkins Setup

1. Select:

Run service as Local System

Click Next

2. Select:

Test Port → Click Next

3. Install required tools.

4. Select:

Firewall Exception → Click Next

5. Click Install

---

Step 3: Open Jenkins

Open browser and type:

http://localhost:8080

Enter:

Admin Password (given in Jenkins setup)

Create:

Admin Account

---

🐍 Python Program (simple.py)

Create file:

simple.py

print("Hello Jenkins Build Successful using Python!")

---

📤 Push Python Program to GitHub

Steps:

1. Create GitHub repository.
2. Upload simple.py file.
3. Copy repository URL.

Example:

https://github.com/username/simple-python.git

---

⚙️ Jenkins Freestyle Build Configuration

Step 1: Create New Item

Go to:

New Item → Enter Name → Select Freestyle Project

Click OK

---

Step 2: Configure GitHub Project

✔ Check:

GitHub Project

Paste:

Repository URL

---

Step 3: Source Code Management

Select:

Git

Paste:

GitHub Repository URL

---

Step 4: Build Section

Select:

Execute Windows Batch Command

Write:

python simple.py

Click:

Save

---

Step 5: Run Build

Click:

Build Now

---

🐳 Dockerfile (For Python)

Create file:

Dockerfile

FROM python:3.10

WORKDIR /app

COPY . .

CMD ["python", "simple.py"]

---

📄 Jenkinsfile (Pipeline Script)

pipeline {

    agent any

    environment {
        registry = 'your-dockerhub-username/simple-python'
        registryCredential = 'jenkin_docker_token'
        dockerImage = ''
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/username/simple-python.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build(registry)
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push('latest')
                    }
                }
            }
        }

    }

}

---

📊 Output

- Jenkins successfully runs Python program.
- Docker image is created.
- Docker image is pushed to Docker Hub.
- Build status shows SUCCESS.

---

✅ Result

Successfully created and configured Jenkins workflow to build Python application and push Docker image.

---

❓ Viva Questions

1. What is Jenkins?
Jenkins is an automation tool used for Continuous Integration and Deployment.

2. What is Docker used for?
Docker is used to create containers to run applications.

3. What is a Dockerfile?
Dockerfile contains instructions to build Docker images.

4. What is GitHub used for?
GitHub is used to store and manage source code.

5. What is Jenkinsfile?
Jenkinsfile defines pipeline stages for Jenkins automation.

---
