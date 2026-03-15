# app-infra

Centralized Kubernetes infrastructure repository with Helm charts.

## Structure

```
app-infra/
├── charts/
│   └── spring-service/        ← Reusable generic chart
│       ├── Chart.yaml          ← Chart identity
│       ├── values.yaml         ← Default values
│       └── templates/
│           ├── deployment.yaml ← K8s Deployment template
│           ├── service.yaml    ← K8s Service template
│           ├── configmap.yaml  ← ConfigMap template (optional)
│           ├── secret.yaml     ← Secrets template (optional)
│           └── namespace.yaml  ← Creates the namespace
└── releases/
    └── contact-service.yaml   ← contact-service specific values
```

## Usage

```bash
# Deploy contact-service
helm upgrade --install contact-service charts/spring-service -f releases/contact-service.yaml

# Deploy with specific tag
helm upgrade --install contact-service charts/spring-service -f releases/contact-service.yaml --set image.tag=5

# Rollback
helm rollback contact-service 1

# Delete
helm uninstall contact-service
```

## Add a new microservice

1. Create `releases/new-service.yaml` with the service values
2. Run: `helm upgrade --install new-service charts/spring-service -f releases/new-service.yaml`
