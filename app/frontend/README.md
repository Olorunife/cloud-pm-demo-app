# Frontend App (Static + Node)

This is the frontend component of the Cloud Migration Demo.  
It serves static content using **Node.js + Express**.

## Run Locally (with Docker)
```bash
docker build -t demo-frontend .
docker run -p 3000:3000 demo-frontend
```

App should be accessible at:
👉 http://localhost:3000



---

#### `docs/success-criteria.md`
```markdown
```
# Success Criteria for Cloud Migration Demo

## Baseline vs. Final Targets

- **Accessibility**
  - App is accessible at `http://<ip-or-url>` before and after migration.

- **Performance**
  - Post-migration: p95 latency ≤ baseline p95 * 0.9  
    _(10% improvement in response time)_

- **Deployment Frequency**
  - Post-migration: Deployments per week increased by 2×

- **Reliability (GameDay Simulation)**
  - Mean Time to Detect (MTTD) ≤ 5 minutes  
  - Mitigation steps documented and executed successfully
