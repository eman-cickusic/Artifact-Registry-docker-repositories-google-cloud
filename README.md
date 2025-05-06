# Artifact Registry: Qwik Start

This repository provides a step-by-step guide for getting started with Google Cloud Artifact Registry, focusing on Docker repositories. It demonstrates how to create a private Docker repository, configure authentication, and push/pull Docker images.

## Overview

Artifact Registry is a secure, scalable, and fully managed service for storing, managing, and securing your build artifacts and dependencies. This project shows you how to:

- Create a private Docker repository in Artifact Registry
- Set up authentication
- Push an image to the repository
- Pull the image from the repository

## Video solution

https://www.youtube.com/watch?v=CgiuLYfL_3A


## Prerequisites

- Google Cloud account with a project
- Basic knowledge of Docker (recommended)
- Google Cloud SDK installed (if running locally)

## Project Structure

```
├── README.md              # This file
├── setup-repository.sh    # Script to create Docker repository
├── authentication-setup.sh # Script to configure authentication
├── docker-commands.sh     # Script with Docker commands
└── .gitignore             # Git ignore file
```

## Step-by-Step Guide

### 1. Create a Docker Repository

Use the `setup-repository.sh` script to create a new Docker repository:

```bash
# Make script executable
chmod +x setup-repository.sh

# Run the script
./setup-repository.sh
```

This creates a repository named `example-docker-repo` in your specified region.

### 2. Configure Authentication

Configure Docker to authenticate with Artifact Registry:

```bash
# Make script executable
chmod +x authentication-setup.sh

# Run the script
./authentication-setup.sh
```

### 3. Pull and Push Docker Images

The `docker-commands.sh` script shows how to:
- Pull a sample image from a public repository
- Tag it for your private repository
- Push it to your private repository
- Pull it back from your private repository

```bash
# Make script executable
chmod +x docker-commands.sh

# Run the script
./docker-commands.sh
```

## Detailed Instructions

### Creating a Docker Repository

```bash
# Set your project ID
export PROJECT_ID=$(gcloud config get-value project)

# Create the repository
gcloud artifacts repositories create example-docker-repo \
    --repository-format=docker \
    --location=REGION \
    --description="Docker repository" \
    --project=$PROJECT_ID

# Verify repository creation
gcloud artifacts repositories list --project=$PROJECT_ID
```

### Configuring Authentication

```bash
# Configure Docker authentication
gcloud auth configure-docker REGION-docker.pkg.dev
```

### Working with Docker Images

```bash
# Pull a sample image
docker pull us-docker.pkg.dev/google-samples/containers/gke/hello-app:1.0

# Tag the image for your repository
docker tag us-docker.pkg.dev/google-samples/containers/gke/hello-app:1.0 \
    REGION-docker.pkg.dev/$PROJECT_ID/example-docker-repo/sample-image:tag1

# Push the image to your repository
docker push REGION-docker.pkg.dev/$PROJECT_ID/example-docker-repo/sample-image:tag1

# Pull the image from your repository
docker pull REGION-docker.pkg.dev/$PROJECT_ID/example-docker-repo/sample-image:tag1
```

## Notes

- Replace `REGION` with your desired Google Cloud region (e.g., `us-central1`)
- The scripts in this repository use environment variables where possible to make them reusable

## Resources

- [Artifact Registry Documentation](https://cloud.google.com/artifact-registry/docs)
- [Docker Documentation](https://docs.docker.com/)
- [Google Cloud CLI Documentation](https://cloud.google.com/sdk/docs)
