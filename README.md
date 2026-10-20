
# Automated CI/CD Pipeline Using Jenkins, Docker and Kubernetes

## Project Overview
This project demonstrates a CI/CD pipeline for a Python Flask web application using Jenkins, Docker, Docker Hub, AWS EC2 and Kubernetes (Minikube).

The pipeline fetches source code from GitHub, builds a Docker image, checks Python syntax, pushes the image to Docker Hub and deploys the application on AWS EC2. The published image is also deployed separately on a local Minikube Kubernetes cluster.

## Technologies Used
- Git and GitHub
- Jenkins
- Docker and Docker Hub
- AWS EC2
- Python and Flask
- Kubernetes and Minikube

## Application
The Flask application displays:

`Hello! Automatic CI/CD deployment is working.`

## CI/CD Pipeline Stages
1. **Clone:** Fetches the source code from GitHub.
2. **Build:** Builds the Docker image.
3. **Test:** Checks Python syntax using `py_compile`.
4. **Push to Docker Hub:** Publishes the image to Docker Hub.
5. **Deploy on EC2:** Runs the updated Docker container and verifies the application using `curl`.

## Docker Hub Image
Repository: https://hub.docker.com/r/sukhmeet123/cloud-app

Image: `sukhmeet123/cloud-app:latest`

## Kubernetes Deployment
The Kubernetes configuration files are:
- `deployment.yaml` — defines the application Deployment.
- `service.yaml` — exposes the application using a NodePort Service.

The application runs on a local Minikube cluster with one replica.

### Deploy on Minikube
Apply the configuration files:

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

Check the deployment, pods and Service:

```bash
kubectl get deployments
kubectl get pods
kubectl get services
```

Access the application locally using port forwarding:

```bash
kubectl port-forward service/cloud-app-k8s 8081:5000
```

Open http://localhost:8081 in a browser.

## Project Structure
- `app.py` — Flask application
- `requirements.txt` — Python dependencies
- `Dockerfile` — instructions for building the Docker image
- `Jenkinsfile` — CI/CD pipeline definition
- `deployment.yaml` — Kubernetes Deployment configuration
- `service.yaml` — Kubernetes Service configuration
- `README.md` — project documentation

## Result
The Jenkins pipeline completed successfully. The Docker image was pushed to Docker Hub, the application was deployed and verified on AWS EC2, and the same published image was successfully deployed and accessed on local Minikube.

## Author
Sukhmeet Singh Muchhal
