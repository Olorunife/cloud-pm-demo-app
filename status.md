Confirm AWS CLI credentials: aws sts get-caller-identity

Confirm local baseline: docker compose up + curl http://localhost:3000/health

After push to ECR & ECS deploy: capture ALB DNS and curl http://$ALB_DNS/health

Run k6 baseline and post-mig scripts; save JSON in docs/media/

Run GameDay script and fill gameday/timeline.csv and postmortem.md

Finalize case study and schedule LinkedIn posts
