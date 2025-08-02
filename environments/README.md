# GitOps Environment Deployments

This directory contains environment-specific deployment manifests that are automatically updated by the enhanced CI/CD pipeline.

## Structure
- `dev/` - Development environment (1 replica, ClusterIP)
- `staging/` - Staging environment (2 replicas, LoadBalancer)  
- `prod/` - Production environment (3 replicas, LoadBalancer, resource limits)

## How it works
1. Enhanced CI/CD pipeline builds and pushes images to ECR
2. Pipeline automatically updates the `image:` field in deployment.yaml files
3. ArgoCD detects changes and deploys to respective environments
4. Production deployments require manual approval

## Image Updates
The CI/CD pipeline updates the image tag in each deployment.yaml:
```yaml
image: 961248554445.dkr.ecr.us-west-2.amazonaws.com/guestbook-app:COMMIT_SHA
```