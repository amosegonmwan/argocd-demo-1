# MyApp Kubernetes Deployment with ArgoCD
This repository contains Kubernetes manifest files for deploying and managing the MyApp application using ArgoCD. The following files are included:

## Files
1. **prod/deployment.yaml** 
Defines the Kubernetes Deployment for `MyApp`.

2. **service.yaml**
Defines the Kubernetes Service to expose `MyApp`.

3. **application.yaml**
Defines the ArgoCD Application to deploy MyApp using the manifests from this repository.