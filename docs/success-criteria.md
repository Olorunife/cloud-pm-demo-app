# Success Criteria - Cloud PM Demo App

## Baseline (local)
- App accessible at http://localhost:3000
- Health endpoint returns JSON: { "status": "ok", "ts": "<timestamp>" }
- Baseline load test artifacts saved (k6 JSON) in docs/media/

## After Migration (target - Kubernetes or cloud)
- App accessible at cloud URL (e.g., https://demo.example.com)
- p95 latency after migration <= baseline p95 * 0.9 (10% improvement)
  OR
  deployment frequency = baseline deploys * 2 during test window
- All post-migration test artifacts saved in docs/media/

## GameDay (resilience drill)
- Mean Time To Detect (MTTD) during simulated failures <= 5 minutes
- Mitigation executed and service restored within 10 minutes
- Postmortem created with at least 3 actionable items

## Evidence required
- Repo with code and manifests
- baseline-k6.json and post-mig-k6.json
- dashboard screenshots (observability)
- gameday/timeline.csv and postmortem.md
- demo video (3-6 minutes) saved to docs/media/
