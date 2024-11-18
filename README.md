# Graded Assignment on MERN application using Kubernetes

## Step 1: Set Up Google Cloud Shell Environment:
- Go to the GCP console: https://console.cloud.google.com

![alt text](README_Images/image.png)

- Click on the terminal icon (Google Cloud Shell) at the top-right corner:

![alt text](README_Images/image-1.png)

## 2. Set the GCP project:

- gcloud config set project [PROJECT_ID]

![alt text](README_Images/image-2.png)

![alt text](README_Images/image-3.png)

## 3. Enable required APIs: Enable the Google Kubernetes Engine (GKE) and Google 
- Container Registry (GCR) APIs: gcloud services enable container.googleapis.com
- gcloud services enable containerregistry.googleapis.com

![alt text](README_Images/image-4.png)

- Step 2: Create a GKE Cluster:
- Create the GKE cluster: Run the following command in Cloud Shell to create a 3-node GKE cluster in the specified zone: 

gcloud container clusters create mern-cluster --zone us-central1-a --num-nodes=3

![alt text](README_Images/image-5.png)

![alt text](README_Images/image-6.png)

## 2. Get cluster credentials: Fetch the credentials for your newly created cluster:
gcloud container clusters get-credentials mern-cluster --zone us-central1-c

![alt text](README_Images/image-7.png)

## Step 3: Clone the MERN Application Repository:
Clone the Sample MERN application: In Cloud Shell, clone the GitHub repository:

![alt text](README_Images/image-8.png)

## Step 4: Build and Push Docker README_Images/images to Google Container Registry (GCR)

Authenticate with GCR:

gcloud auth configure-docker

![alt text](README_Images/image-9.png)

## Build and tag Docker README_Images/images: You need to build and tag Docker README_Images/images for the backend (helloService, profileService) and frontend.

## Backend (helloService):

cd backend/helloService
docker build -t gcr.io/[PROJECT_ID]/helloservice:v1 .

![alt text](README_Images/image-10.png)

## Backend (profileService):

![alt text](README_Images/image-11.png)

## Frontend:

![alt text](README_Images/image-12.png)

- 3. Push the Docker README_Images/images to GCR:
docker push gcr.io/[PROJECT_ID]/helloservice:v1

![alt text](README_Images/image-13.png)

- For profileService:
docker push gcr.io/[PROJECT_ID]/profileservice:v1

![alt text](README_Images/image-14.png)

- For mernfrontend:

![alt text](README_Images/image-15.png)

- Step 5: Create Kubernetes Deployment and Service Files:

![alt text](README_Images/image-16.png)

- In Cloud Shell, create Kubernetes YAML files for each microservice.

- 1. Create helloservice-deployment.yaml:

![alt text](README_Images/image-17.png)

- 2. Create profileservice-deployment.yaml:

![alt text](README_Images/image-18.png)

![alt text](README_Images/image-19.png)

- 3. mernfrontend-service.yaml:

![alt text](README_Images/image-20.png)

## 4. Create Service files for each microservice:

- helloservice-service.yaml:

![alt text](README_Images/image-21.png)

- profileservice-service.yaml:

![alt text](README_Images/image-22.png)

- mernfrontend-service.yaml:

![alt text](README_Images/image-23.png)

## Step 6: Deploy the Services to GKE:

- 1. Apply the deployments and services:
kubectl apply -f helloservice-deployment.yaml

![alt text](README_Images/image-24.png)

- kubectl apply -f profileservice-deployment.yaml

![alt text](README_Images/image-25.png)

- kubectl apply -f mernfrontend-deployment.yaml

![alt text](README_Images/image-26.png)

- kubectl apply -f helloservice-service.yaml

![alt text](README_Images/image-27.png)

- kubectl apply -f profileservice-service.yaml

![alt text](README_Images/image-28.png)

- kubectl apply -f mernfrontend-service.yaml

![alt text](README_Images/image-29.png)

- 2.Verify that the services are running:
- kubectl get services

![alt text](README_Images/image-30.png)

- Take note of the external IP addresses for each service. These IPs can be used to access the application in a browser. 
- Verify once if all the microservices pods are in running state:
- Kubectl get pods

![alt text](README_Images/image-31.png)

- Step 9: Push to GitHub

![alt text](README_Images/image-32.png)












