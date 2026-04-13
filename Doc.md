Experiment No: 6

Title: Create and Configure Jenkins Pipeline to Build Python Application and Push Docker Image

---

🎯 Aim

To create and configure Jenkins pipeline workflow to build a Python application and push the Docker image to Docker Hub.

---

🧰 Requirements

- Jenkins 2.375.1 LTS (Windows)
- Python 3.x
- Docker Desktop Installed
- GitHub Account
- Docker Hub Account

---

🐍 Step 1: Create Python Program

Create file:

simple.py

print("Hello Jenkins Pipeline using Python!")

---

🐳 Step 2: Create Dockerfile

Create file:

Dockerfile

FROM python:3.10

WORKDIR /app

COPY . .

CMD ["python", "simple.py"]

---

🔧 Step 3: Create Jenkinsfile (Pipeline Script)

Create file:

Jenkinsfile

pipeline {

    agent any

    environment {
        registry = 'your-dockerhub-username/simple-python'
        registryCredential = 'jenkin_docker_token'
        dockerImage = ''
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/your-username/simple-python.git'
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

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }

}

---

📤 Step 4: Push Files to GitHub

Upload these files:

- simple.py
- Dockerfile
- Jenkinsfile

Example Repository:

https://github.com/username/simple-python

Copy this URL.

---

⚙️ Step 5: Create Jenkins Pipeline Job

Open Jenkins:

http://localhost:8080

Steps:

1. Click New Item
2. Enter Name:

python-pipeline

3. Select:

Pipeline

Click OK

---

⚙️ Step 6: Configure Pipeline

Scroll to:

Pipeline Section

Select:

Pipeline script from SCM

SCM:

Git

Repository URL:

Paste GitHub URL

Branch:

main

Script Path:

Jenkinsfile

Click:

Save

---

▶️ Step 7: Run Pipeline

Click:

Build Now

Jenkins will:

- Pull code from GitHub
- Build Docker image
- Push Docker image
- Show SUCCESS message

---

📊 Expected Output

- Python program executed
- Docker image created
- Docker image pushed to Docker Hub
- Pipeline build SUCCESS

---

✅ Result

Successfully created and configured Jenkins pipeline workflow to build Python application and push Docker image using Docker.

---

❓ Viva Questions

1. What is Jenkins Pipeline?
Jenkins Pipeline is a set of automated steps used to build, test, and deploy applications.

2. What is Jenkinsfile?
Jenkinsfile is a script that defines the pipeline process.

3. What is Dockerfile?
Dockerfile contains instructions to create Docker image.

4. What is GitHub used for?
GitHub stores project files.

5. What is CI/CD?
CI/CD means Continuous Integration and Continuous Deployment.

---
