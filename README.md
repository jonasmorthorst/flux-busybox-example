# Flux BusyBox Example

This repository demonstrates how to deploy a simple BusyBox application using Flux GitOps.

## Contents

- `manifests/busybox-deployment.yaml` - Simple BusyBox deployment that sleeps for 1 hour

## Usage with Flux

1. Create GitRepository:
```bash
flux create source git busybox-app \
  --url=https://github.com/jonasmorthorst/flux-busybox-example \
  --branch=main \
  --interval=1m
```

2. Create Kustomization:
```bash
flux create kustomization busybox-app \
  --target-namespace=default \
  --source=busybox-app \
  --path="./manifests" \
  --prune=true \
  --interval=5m
```

3. Verify deployment:
```bash
kubectl get pods -l app=busybox-app
```