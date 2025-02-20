# K8's Kadence Flask App

## Overview

This repository contains a simple Flask application designed to demonstrate the basics of containerization using Docker and orchestration using Kubernetes. The application greets users with a personalized message, "Hello {username} welcome to K8’s Kadence!", where the `{username}` is dynamically set through an environment variable. The goal of this project is to provide a hands-on experience for students learning about Docker, Kubernetes, and the principles of deploying applications in a containerized environment.

## Features

- **Personalized Greeting:** The application uses an environment variable to personalize the greeting message.
- **Containerization:** The Flask app is containerized using Docker, allowing for easy deployment and scalability.
- **Kubernetes Ready:** The application is designed to be deployed on a Kubernetes cluster, demonstrating basic Kubernetes concepts.
- **Styling:** The application features a simple styling with white text on a light blue background.

## Getting Started

### Prerequisites

- Docker installed on your machine.
- Access to a Docker Hub account.
- Access to a Kubernetes cluster (for Kubernetes deployment).

### Local Development and Testing

1. **Clone the Repository:**
    ```sh
    git clone https://github.com/pvass24/k8s-kadence.git
    ```

2. **Build the Docker Image:**
    ```sh
    docker build -t myflaskapp:v1 .
    ```

3. **Run the Docker Container:**
    Replace `<username>` with your desired username.
    ```sh
    docker run -p 5000:5000 -e USERNAME=<username> myflaskapp:v1
    ```

4. **Access the Application:**
    Open a web browser and navigate to `http://localhost:5000`.

5. **Stop the Container:**
    Enter `Control + C` to stop the container.

### Adding the Image to Docker Hub

1. **Log in to Docker Hub from Your Command Line:**
    ```sh
    docker login
    ```

2. **Tag Your Docker Image:**
    Replace `yourdockerhubusername` with your Docker Hub username and `tagname` with your desired tag.
    ```sh
    docker tag myflaskapp:v1 yourdockerhubusername/myflaskapp:v1
    ```

3. **Push the Image to Docker Hub:**
    ```sh
    docker push yourdockerhubusername/myflaskapp:v1
    ```

4. **Verify the Image on Docker Hub:**
    Check your Docker Hub account to see if the image is uploaded.

### Deploying on Kubernetes

1. **Create or Update the Kubernetes Deployment YAML:**
   Edit the `deployment.yaml` file to point to the image on your Docker Hub account (`yourdockerhubusername/myflaskapp:v1`).

2. **Apply the Deployment:**
   Apply the deployment to your Kubernetes cluster using the command:
   ```sh
   kubectl apply -f deployment.yaml

3. **View and Create the Service:**
   
   Since were using KinD, to access the deployment we need to create a service. I have created the service yaml file for you. Check it out. Its called myflaskapp-svc.yaml
   ```sh
   cat myflaskapp-svc.yaml
   ```
   You can see the service is exposing the flask app with a nodePort of 30000. This port has backend configurations that translate the nodePort to port `3000` locally which is in the cluster config. Also the pods in the deployment are "selected" due to the matching labels "app: myflaskapp".

   Lets create the service.
   ```sh
   kubectl create -f myflaskapp-svc.yaml
   ```
   Enter https://localhost:3000 to view your application.

4. **Clean UP:**
   Lets delete the Deployment to continue to the next session.
   ```sh
   kubectl delete deployment myflaskapp-deployment
   ```
Great work! Now lets navigate to myflaskapp-v2 folder.
