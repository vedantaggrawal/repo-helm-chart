# Generic Application Helm Chart (Repo 2)

A lightweight, generic Helm chart for deploying stateless 12-factor apps identically across distinct environments on Kubernetes/OpenShift.

## Features

- **Standard Deployment**: Ships a standard K8s Deployment normally.
- **Canary Rolling Updating**: By toggling `canary.enabled: true`, the chart omits the standard `Deployment` and utilizes an **Argo Rollout** parameter for robust weight-based traffic splitting.
- **Environment Configuration**: A simple Dictionary format translates directly into a ConfigMap mapping environment variables cleanly to the container runtime via `envFrom`. This aligns with the "config injected per environment via env vars mapping, not baked down" best practice.
- **Ingress / Route Support**: Automatically ships the application's external exposition definitions mapped cleanly to OpenShift's default routing architecture via generalized K8s `Ingress`.

## Usage Pattern Overview

In your GitOps / Platform Configuration mappings:

```yaml
replicaCount: 3
image:
  repository: ghcr.io/your-namespace/devops-test-webserver
  tag: 4a2b9f3
envVariables:
  APP_ENV: production
canary:
  enabled: true
```
