# GitOps Demo for BITS Dissertation

## Mid-Term Status
This project has reached a functional mid-term milestone for the dissertation titled:

> Design and Evaluation of a Secure GitOps CI/CD Pipeline with Automated Rollback using ArgoCD and Prometheus

The prototype currently demonstrates a working local GitOps pipeline using Docker, Kubernetes, ArgoCD, GitHub Actions, and Prometheus/Grafana. The system is suitable for mid-term evaluation and further extension toward automated rollback and formal comparative analysis.

## Core Technologies

- Docker for containerization
- Kubernetes for orchestration
- GitHub Actions for CI
- ArgoCD for GitOps reconciliation
- Prometheus and Grafana for monitoring
- Nginx health probes for availability checks

## Architecture Summary

The pipeline follows a GitOps model:

1. Code changes are committed to GitHub.
2. GitHub Actions builds the application image.
3. Kubernetes manifests define the desired cluster state.
4. ArgoCD detects drift and syncs the environment.
5. Monitoring and health probes provide operational visibility.
6. The design supports future rollback automation.

## Local Run

Build and run locally:

```bash
docker build -t gitops-demo .
docker run -p 8080:80 gitops-demo
```

Then open:

```text
http://localhost:8080
```

## Kubernetes Setup

Create the local cluster and deploy the app:

```bash
kind create cluster --name gitops-demo
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

## Monitoring Setup

```bash
kubectl create namespace monitoring
kubectl apply -f monitoring/prometheus-config.yaml
kubectl apply -f monitoring/prometheus-deployment.yaml
kubectl apply -f monitoring/grafana-deployment.yaml
```

## ArgoCD Setup

ArgoCD is installed in the cluster and the application manifest is available in the repository:

```bash
kubectl apply -f argocd/application.yaml
```

Update the GitHub URL in the ArgoCD manifest before using it in a real Git repository workflow.

## Documentation

The mid-term dissertation draft is available in:

- [MIDTERM_REPORT.md](MIDTERM_REPORT.md)

## Verification Notes
The prototype was validated with these checks:

- `kubectl rollout status deployment/gitops-demo --timeout=120s`
- `curl.exe -sSf http://localhost:8080/health`
- `kubectl get pods -n argocd`

These checks confirm the application and core GitOps control plane are functioning.
