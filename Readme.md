# Hello World Frontend Application on GKE

This project demonstrates the deployment of a simple "Hello, World!" frontend application on Google Kubernetes Engine (GKE). The frontend application is containerized using Docker and deployed to GKE for scalability and ease of management.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
- [Deployment](#deployment)
- [Accessing the Application](#accessing-the-application)
- [Cleaning Up](#cleaning-up)
- [License](#license)

## Prerequisites

Before you begin, ensure you have the following:

- Google Cloud Platform (GCP) account
- Google Cloud SDK installed locally
- Docker installed on your local machine

## Getting Started

1. Build and push the Docker image to Artifact Registry:

   ```bash
   docker build .
   docker tag IMAGE NAME REGION-docker.pkg.dev/PROJECT ID/REPO NAME/IMAGE:TAG
   docker push REGION-docker.pkg.dev/PROJECT ID/REPO NAME/IMAGE:TAG
   ```

   Replace the placeholder with your details.

## Cluster Creation

2. Create the kubernetes cluster where the image will be deployed

   ```
   gcloud container clusters create CLUSTER NAME --num-nodes=3 --zone=PREFERRED-ZONE
   ```

3. Authenticate kubectl with the GKE cluster 

   ```
   gcloud container clusters get-credentials CLUSTER NAME --zone=PREFERRED-ZONE

   ```    

4. Install the GKE container plugin for gcloud

   ```
   gcloud components install gke-gcloud-auth-plugin

   ```

## Deployment

5. Apply the Kubernetes deployment and service configurations:

   ```bash
   kubectl apply -f my-app-deployment.yaml
   kubectl apply -f my-app-service.yaml
   ```

6. Wait for the external IP to be assigned:

   ```bash
   kubectl get services -o wide
   ```

## Accessing the Application

5. Open your browser and navigate to the external IP to see the "Hello, World!" application.

## Cleaning Up

6. To delete the deployed resources, run:

   ```bash
   kubectl delete deployment frontend-deployment
   kubectl delete service frontend-service
   ```

7. Optionally, delete the GKE cluster:

   ```bash
   gcloud container clusters delete [CLUSTER_NAME] --zone [ZONE]
   ```

   Replace `[CLUSTER_NAME]` and `[ZONE]` with your GKE cluster name and zone.