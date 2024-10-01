# ArgoCD Demo Application

This repository contains a basic example of deploying a Kubernetes application using ArgoCD. The setup includes a Deployment, Service, and Application configuration for ArgoCD to automatically manage.

## Application Overview

The application consists of three primary components:
1. **ArgoCD Application (`application.yaml`)**: Defines the application in ArgoCD, syncing a Kubernetes deployment and service configuration from the repository.
2. **Kubernetes Deployment (`prod/deployment.yaml`)**: Describes the application deployment in Kubernetes, including the image and replica settings.
3. **Kubernetes Service (`prod/service.yaml`)**: Exposes the application via a Service, routing traffic to the correct container port.

## Folder Structure

The repository follows a typical Kubernetes application structure:


## ArgoCD Application Configuration (`application.yaml`)

- **apiVersion**: `argoproj.io/v1alpha1`
- **Kind**: Application
- **Metadata**:
  - **name**: `myapp-argo-application`
  - **namespace**: `argocd`
- **Spec**:
  - **project**: `default`
  - **source**: The source repository for the application configuration, pointing to this repository.
  - **destination**: Specifies the Kubernetes cluster and namespace where the application will be deployed.
  - **syncPolicy**:
    - **syncOptions**: Configures ArgoCD to create the namespace if it doesn't exist.
    - **automated**: Enables automated synchronization with `selfHeal` and `prune` options.

## Kubernetes Deployment (`prod/deployment.yaml`)

- **apiVersion**: `apps/v1`
- **Kind**: Deployment
- **Metadata**:
  - **name**: `myapp`
- **Spec**:
  - **replicas**: `5` (Number of application replicas)
  - **selector**: Matches the `myapp` label.
  - **template**:
    - **containers**: Runs the `myapp` container using the image `amosegonmwan/kubenginx:3.0.0`.
    - **ports**: Exposes port `8080`.

## Kubernetes Service (`prod/service.yaml`)

- **apiVersion**: `v1`
- **Kind**: Service
- **Metadata**:
  - **name**: `myapp-service`
- **Spec**:
  - **selector**: Routes traffic to the pods labeled `myapp`.
  - **ports**: Exposes port `8080` for the service using TCP.

## Syncing with ArgoCD

After pushing changes to this repository, ArgoCD will automatically sync the deployment and service based on the configuration defined in `application.yaml`.

### ArgoCD Sync Policy
- **Self Heal**: Automatically corrects any configuration drift.
- **Prune**: Removes any resources that are not tracked in the repository.

## How to Deploy

1. Add the repository to ArgoCD by creating the Application object.
2. ArgoCD will automatically deploy the `prod/deployment.yaml` and `prod/service.yaml` configurations to your Kubernetes cluster.
3. Monitor the application's status in the ArgoCD UI.

## Image Details

- **Container Image**: `amosegonmwan/kubenginx:3.0.0`
- **Exposed Port**: `8080`
