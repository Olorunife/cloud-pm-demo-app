# Cloud PM Demo App
Public demo used for a Reference Migration proof asset.
This repo contains a small static frontend served by Node (Express), dockerized and runnable via docker compose.


# 1) create project skeleton
```bash
mkdir -p ~/cloud-pm-demo-app/app/frontend ~/cloud-pm-demo-app/docs ~/cloud-pm-demo-app/docs/media
cd ~/cloud-pm-demo-app
git init
```



# 2) create README
```bash
cat > README.md <<'EOF'
# Cloud PM Demo App
Public demo used for a Reference Migration proof asset.
This repo contains a small static frontend served by Node (Express), dockerized and runnable via docker compose.
EOF
```



# 3) .gitignore

```bash
cat > .gitignore <<'EOF'
node_modules/
docs/media/
.env
EOF
```

# 4) frontend package.json
```bash
cat > app/frontend/package.json <<'EOF'
{
  "name": "cloud-pm-demo-frontend",
  "version": "1.0.0",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^4.18.2"
  }
}
EOF
```

# 5) simple Express server with health endpoint
```bash
cat > app/frontend/server.js <<'EOF'
const express = require('express');
const path = require('path');
const app = express();
const PORT = process.env.PORT || 3000;

app.use(express.static(path.join(__dirname, 'public')));

app.get('/health', (req, res) => {
  res.json({ status: 'ok', ts: new Date().toISOString() });
});

app.listen(PORT, () => {
  console.log(`Frontend demo listening on port ${PORT}`);
});
EOF
```

# 6) index.html
```bash
mkdir -p app/frontend/public
cat > app/frontend/public/index.html <<'EOF'
<!doctype html>
<html>
  <head>
    <meta charset="utf-8"/>
    <title>Cloud PM Demo</title>
    <style>
      body { font-family: Arial, sans-serif; padding: 40px; text-align:center; }
      .card { max-width:700px; margin:0 auto; border-radius:12px; padding:24px; box-shadow:0 6px 18px rgba(0,0,0,0.08); }
      h1 { margin-bottom:8px }
      p { color:#444 }
      .status { margin-top:18px; font-weight:600; color: #0b6623; }
    </style>
  </head>
  <body>
    <div class="card">
      <h1>Cloud PM Demo App</h1>
      <p>This is a small static + Node frontend used for the Reference Migration flagship case.</p>
      <p class="status" id="status">Checking health...</p>
      <script>
        fetch('/health').then(r=>r.json()).then(d=>{
          document.getElementById('status').innerText = 'Health: ' + d.status + ' — ' + new Date(d.ts).toLocaleString();
        }).catch(()=>{ document.getElementById('status').innerText = 'Health: unreachable'; });
      </script>
    </div>
  </body>
</html>
EOF
```

# 7) Dockerfile
```bash
cat > app/frontend/Dockerfile <<'EOF'
FROM node:18-alpine
WORKDIR /app
COPY package.json ./
RUN npm install --production
COPY . .
ENV PORT=3000
EXPOSE 3000
CMD ["npm", "start"]
EOF
```

# 8) root docker-compose.yml
```bash
cat > docker-compose.yml <<'EOF'
version: "3.8"
services:
  frontend:
    build: ./app/frontend
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
EOF
```


# 9) docs/success-criteria.md
```bash
mkdir -p docs
cat > docs/success-criteria.md <<'EOF'
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
EOF
```


# 10) docs/architecture.md
```bash
cat > docs/architecture.md <<'EOF'
# Architecture - Cloud PM Demo App (simple)

## Baseline (local)
User -> Node frontend (Express) served from Docker Compose

## Target (example)
User -> Ingress -> Kubernetes service -> frontend pods
Add-ons: observability (Prometheus + Grafana), CI/CD pipeline, load test runner, GameDay scripts.

(Use a quick diagram tool - Excalidraw or draw.io - to create a visual and upload to docs/media/architecture.png)
EOF
```


# 11) initial commit
```bash
git add .
git commit -m "scaffold: frontend demo, docker, docs, success criteria"
```
