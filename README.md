# Kubernetes Manifests for dwk-todo Application

This repository contains Kubernetes manifests for deploying the dwk-todo application with a PostgreSQL database and NATS broadcaster service. The setup uses Kustomize for environment-specific configurations and ArgoCD for GitOps-style continuous deployment.

## Components

- **dwk-todo Application**: Main application with health check probes and PostgreSQL connectivity
- **PostgreSQL Database**: Stateful database with persistent storage
- **NATS Broadcaster**: Service for broadcasting events with Discord webhook integration
- **ArgoCD**: Configuration for continuous deployment

## Environment Differences

### Production
- Uses specific image versions for stability
- Standard NATS broadcaster configuration

### Staging
- Different image versions for testing
- NATS broadcaster does not push status updates to Discord
- Modified resource configurations

## Deployment

This project is set up for automatic deployment using ArgoCD:

1. The application manifests are stored in GitHub
2. ArgoCD is configured to sync from the repository
3. Changes to the manifests trigger automatic updates in the respective environments

### Manual Deployment

To manually deploy using Kustomize:

```bash
# For staging
kubectl apply -k overlays/staging

# For production
kubectl apply -k overlays/prod
```