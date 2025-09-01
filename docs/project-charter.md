# Project Charter — Cloud PM Demo

> **How to use this document:**
>
> * Replace every `{{placeholder}}` with your project-specific values.
> * Keep the document concise — stakeholders read one page. Use the appendices for details.

---

## 1. Project Overview

**Project Title:** {{Project Title}}

**Project Sponsor:** {{Sponsor name & role}}

**Project Manager (Owner):** {{Your name}}

**Start Date:** {{YYYY-MM-DD}}    **Target End Date:** {{YYYY-MM-DD}}

**Purpose / Summary (1–2 sentences):**

> Example: Demonstrate a full migration of a simple Node static frontend from local Docker to AWS (ECS Fargate), with CI/CD, monitoring, and resilience tests to produce a reproducible case study for hiring and thought leadership.

---

## 2. Business Goals & Objectives

* **Primary business goal:** {{e.g., show measurable improvements in reliability, deploy frequency, and observability that hiring managers can verify}}
* **Objectives (SMART):**

  * O1: Deploy the containerized frontend to AWS (ECS Fargate) and expose via ALB by {{date}}.
  * O2: Implement CI/CD that completes a build → deploy cycle in < 5 minutes.
  * O3: Implement basic observability (logs + metrics + simple dashboard) and run one GameDay with a documented postmortem.

---

## 3. Scope

**In scope:**

* Containerize frontend (Node + static assets).
* Publish image to ECR and deploy to ECS Fargate behind ALB.
* Create a CI workflow (GitHub Actions) that builds + pushes image, triggers deploy.
* Add basic monitoring (CloudWatch logs + simple dashboard) and a single GameDay (pod/task failure simulation).
* Produce a public repo, case study, demo video (3–6 min) and 3 LinkedIn posts.

**Out of scope:**

* Backend/data migrations involving customer data.
* Multi-region production-grade HA.
* Long-term managed support or billing commitments beyond demonstration.

---

## 4. Deliverables (what we will hand over)

1. `repo` with all code, manifests, and documentation.
2. Docker image in ECR and ECS service running behind ALB.
3. CI/CD workflow (GitHub Actions) configured with secrets guidance.
4. Observability evidence: logs, simple dashboard screenshot, SLOs doc.
5. GameDay timeline + blameless postmortem with 3 actions.
6. Case study (3–6 pages), 1-page exec summary PDF, demo video (3–6 min).

---

## 5. Success Criteria (KPIs — measurable)

Fill metrics during baseline and after migration.

* **Accessibility:** App reachable at `http://<IP-or-DNS>` before and after migration.
* **Performance:** p95 latency after migration ≤ baseline p95 × 0.9 (10% improvement) OR deploy frequency ≥ 2× baseline during test window.
* **Reliability (GameDay):** Mean Time To Detect (MTTD) ≤ 5 minutes; mitigation executed within 10 minutes.
* **CI/CD:** Build → Deploy cycle completes in < 5 minutes in CI.
* **Evidence:** baseline-k6.json and post-mig-k6.json saved in `docs/media/`; dashboard screenshots and postmortem in `docs/`.

---

## 6. Roles & Responsibilities

| Role                     |                    Person / Owner | Responsibilities                                                       |
| ------------------------ | --------------------------------: | ---------------------------------------------------------------------- |
| Project Sponsor          |                       {{Sponsor}} | Approve charter, review final case study                               |
| Project Manager          |                           {{You}} | Own charter, timeline, stakeholder comms, acceptance                   |
| Technical Exec (Dev/Ops) | ChatGPT/Executor (tasks provided) | Provide IaC, manifests, scripts; produce artifacts for you to validate |
| QA/Tester                |                  {{You / Tester}} | Run baseline/post-mig tests and save artifacts                         |
| Technical Writer         | ChatGPT (drafts) / You (finalize) | Draft case study, exec summary, LinkedIn copy                          |

> **Note:** For this demo, many technical deliverables will be prepared as runnable artifacts. As PM you will *approve* and *validate* them, capture evidence, and own the public narrative.

---

## 7. Timeline & Milestones (high level)

* **M1 – Init (Days 0–2):** Charter, repo skeleton, success criteria.
* **M2 – Baseline (Days 3–5):** Local Docker run + baseline k6 run.
* **M3 – Target infra (Days 6–12):** ECR image push, ECS cluster & service, ALB, deploy.
* **M4 – Observability & CI (Days 13–18):** CI workflow, CloudWatch logs, dashboard.
* **M5 – GameDay & Cost analysis (Days 19–22):** Run GameDay, postmortem, cost modeling.
* **M6 – Closure (Days 23–30):** Case study, video, LinkedIn publishing.

---

## 8. Communication Plan

* **Weekly status email** to sponsor (one paragraph + 3 bullets: done, doing, blockers).
* **Daily quick check** (5–10 mins): update `status.md` in repo with 3 lines.
* **Incident reporting:** For GameDay or failures, use `gameday/postmortem.md` template.
* **Repository:** All artifacts & evidence live in the repo under `docs/`.

---

## 9. Risk Register (top risks - attach detailed spreadsheet in appendix)

| ID | Risk                           | Likelihood | Impact | Mitigation                                                  | Owner |
| -- | ------------------------------ | ---------: | -----: | ----------------------------------------------------------- | ----- |
| R1 | AWS account/credential issues  |     Medium |   High | Use local `kind` fallback; pre-check credentials            | PM    |
| R2 | Secrets accidentally published |        Low |   High | Use .env templates; sanitize history; do not commit secrets | PM    |
| R3 | Time constraints               |       High | Medium | Trim scope to essential deliverables; extend timeline       | PM    |

---

## 10. Acceptance & Sign-off

**Acceptance Criteria:** All deliverables completed; evidence in repo; exec summary + demo video published.

**Approver:** {{Sponsor name}} — Signature / Approval Date: \_\_\_\_\_\_\_\_\_\_

---

## Appendix: Quick actions for the PM (copy into your `status.md` or checklist)

1. Confirm AWS CLI credentials: `aws sts get-caller-identity`
2. Confirm local baseline: `docker compose up` + `curl http://localhost:3000/health`
3. After push to ECR & ECS deploy: capture ALB DNS and `curl http://$ALB_DNS/health`
4. Run k6 baseline and post-mig scripts; save JSON in `docs/media/`
5. Run GameDay script and fill `gameday/timeline.csv` and `postmortem.md`
6. Finalize case study and schedule LinkedIn posts

---

*End of Project Charter template.*

