# Architecture - Cloud PM Demo App (simple)

## Baseline (local)
User -> Node frontend (Express) served from Docker Compose

## Target (example)
User -> Ingress -> Kubernetes service -> frontend pods
Add-ons: observability (Prometheus + Grafana), CI/CD pipeline, load test runner, GameDay scripts.

(Use a quick diagram tool - Excalidraw or draw.io - to create a visual and upload to docs/media/architecture.png)
