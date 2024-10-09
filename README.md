# Deploy Nginx to Google Kubernetes Engine (GKE) with GitHub Actions

This project demonstrates an automated deployment pipeline for an Nginx web server to Google Kubernetes Engine (GKE) using GitHub Actions. The configuration includes a multi-step CI/CD pipeline that builds and pushes a Docker image to Google Container Registry (GCR) and deploys it to GKE. This setup leverages Kubernetes YAML files to define the deployment and service resources and ensures an efficient and streamlined deployment process.

## Project Files Overview

- **Dockerfile**: Builds a simple Nginx server with a custom "Hello World" message.
- **resources.yml**: Defines the Kubernetes deployment and service configuration for Nginx in GKE.
- **build.yaml**: GitHub Actions workflow file responsible for building and pushing the Nginx Docker image to GCR.
- **build-and-deploy.yaml**: GitHub Actions workflow file that builds, pushes the Docker image to GCR, and deploys it to GKE using `resources.yml`.

## Setup Instructions

### 1. Google Cloud Platform (GCP) Setup
- **Enable GKE and Container Registry APIs**: Go to GCP Console and enable Google Kubernetes Engine and Container Registry APIs.
- **Create GKE Cluster**: Set up a GKE cluster and note the cluster name, region, and project ID.
- **Create Service Account**:
  - Create a service account with roles `Kubernetes Engine Admin` and `Storage Admin`.
  - Download the service account key JSON file.
- **Configure Permissions**:
  - Store the service account JSON key file securely.
  
### 2. GitHub Repository Setup
- **Create Secrets** in your GitHub repository:
  - `GOOGLE_PROJECT`: GCP Project ID
  - `GOOGLE_APPLICATION_CREDENTIALS`: Paste the contents of your service account JSON key file.

### 3. GitHub Actions
- Add `build.yaml` and `build-and-deploy.yaml` to your `.github/workflows` directory.
- These workflows will build the Docker image, push it to GCR, and deploy it to your GKE cluster when changes are pushed to the `main` branch.

## How the CI/CD Pipeline Works

1. **Docker Image Build**:
   - The GitHub Actions workflow uses the Dockerfile to create an image for the Nginx server.
   - The image includes a basic "Hello World" message on the main page.

2. **Push to GCR**:
   - The image is pushed to the Google Container Registry under your specified GCP project.

3. **Deploy to GKE**:
   - The `resources.yml` file is applied to create a Kubernetes deployment and service on GKE.
   - The LoadBalancer service exposes Nginx to the internet.

## Conclusion

This project provides an automated solution for deploying containerized applications to GKE using Docker and GitHub Actions. By implementing this CI/CD pipeline, you can reduce manual intervention, achieve consistency, and enable rapid updates to applications with minimized risk of error.
