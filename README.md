# wisecow-task
# Wisecow-Project
<img width="1920" height="1080" alt="Screenshot (529)" src="https://github.com/user-attachments/assets/5127eb1e-d98c-42bf-9bca-d7193382b933" />

<img width="1920" height="1080" alt="Screenshot (531)" src="https://github.com/user-attachments/assets/f3e73ca7-16ca-4f03-8ae3-d8bf1db7f6df" />

<img width="1920" height="1080" alt="Screenshot (534)" src="https://github.com/user-attachments/assets/68f86a59-c480-49dd-9250-2d74498e30c3" />


Wisecow Project Deployment Guide
Overview

Wisecow is a web application deployed using a modern DevOps workflow. The deployment pipeline automates build, Docker image creation, artifact storage, and Kubernetes deployment using Minikube.




Prerequisites

Before starting, ensure you have the following installed:

Git

git --version


Jenkins
Set up Jenkins with required plugins for Git, Docker, and Kubernetes.

Docker & Docker Hub Account

docker --version


Make sure you are logged in to Docker Hub:

docker login


Kubernetes & Minikube

kubectl version --client
minikube version


Shell environment (bash or zsh) for running scripts.

Step 1: Clone the Repository

Jenkins or your local machine should pull the latest code:

git clone https://github.com/rateshivakuma/Wisecow-Project.git
cd Wisecow-Project

Step 2: Build the Application

Install dependencies and build the project (depends on project type, e.g., Java, Node.js):

# Example for a generic shell build script
./wisecow.sh build


Verify that the build is successful.

Step 3: Archive Artifacts

Archive key project files in Jenkins or locally for traceability:

Dockerfile

wisecow.sh

Any build artifacts (e.g., .jar or .war files if Java)

Step 4: Docker Build & Push
Build Docker Image
docker build -t rateshivakumar/wisecow:<BUILD_NUMBER> .

Push to Docker Hub
docker push rateshivakumar/wisecow:<BUILD_NUMBER>
docker push rateshivakumar/wisecow:latest

Step 5: Deploy Locally (Optional)

Test the Docker container locally:

docker rm -f wisecow || true
docker run -d --name wisecow -p 4499:4499 rateshivakumar/wisecow:<BUILD_NUMBER>


Check logs if needed:

docker logs -f wisecow

Step 6: Deploy on Kubernetes (Minikube)

Apply the Kubernetes manifest:

kubectl apply -f wisecow-deploy.yaml


Check pods and service:

kubectl get pods
kubectl get svc


Access the application:

minikube service wisecow

Step 7: Technologies Used

CI/CD: Jenkins

Containerization: Docker, Docker Hub

Orchestration: Kubernetes, Minikube

Scripting: Shell scripts (wisecow.sh, deployment scripts)

Version Control: GitHub
