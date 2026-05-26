# 90-Day DevOps Learning Plan

## Who I Am

**Level:** Working professional — 8 years backend web development experience.
I know Linux basics, Git, and can write code, but I have never deployed anything
to production on AWS alone, never configured a CI/CD pipeline end-to-end, and have zero
hands-on Kubernetes experience. My foundation is decent; my DevOps execution is
close to zero. This plan changes that.

---

## 3 Goals for the Next 90 Days

1. **Deploy a production-grade application on Kubernetes** — containerised,
   with Helm charts, health probes, ConfigMaps, and Secrets properly managed.
   Not a tutorial copy-paste. My own project, my own decisions.

2. **Build and own a complete CI/CD pipeline** — GitHub Actions (or Jenkins)
   that runs tests, builds a Docker image, pushes to a registry, and
   auto-deploys to a Kubernetes cluster or ECS. Zero manual deploy steps.

3. **Be confident in AWS core services** — VPC, EC2, ECS/EKS, RDS, S3,
   IAM, CloudWatch — well enough to architect a 3-tier application and
   explain every security group rule in an interview.

---

## 3 Core DevOps Skills I Am Building

| # | Skill | Why it matters to me |
|---|-------|----------------------|
| 1 | **Linux troubleshooting & shell scripting** | I use Linux daily but avoid anything outside basic commands. I need to be fluent in scripting, SSH, and system debugging. |
| 2 | **CI/CD pipelines (GitHub Actions + Jenkins)** | I have never built a pipeline from scratch. This is the gap that blocks every senior role I want. |
| 3 | **Kubernetes operation & debugging** | K8s is non-negotiable at PayPay, Rakuten, and every MNC I want to target. I need hands-on confidence, not just theory. |

---

## Weekly Time Budget

| Day | Hours | Activity |
|-----|-------|----------|
| Mon – Fri | 2 hours/day | Syllabus modules + hands-on practice |
| Saturday | 4 hours | Project work + deploy something real |
| Sunday | 2 hours | Review week, write notes, fix what broke |
| **Total** | **~18 hrs/week** | **~90 hours per phase** |

> Rule: if I miss a weekday, I do not skip it — I carry it to Saturday.
> Consistency over perfection.

---

## 90-Day Roadmap (Aligned to UDAAN Syllabus)

### Phase 1 — Foundation (Weeks 1–3)
| Week | Topic | My commitment |
|------|-------|---------------|
| 1 | Linux Essentials: OS concepts, VMs, file system, package managers, permissions, CLI | Set up Ubuntu VM. Do every command by hand. No copy-paste. |
| 2 | Linux Advanced: Shell scripting, SSH, networking (IP, CIDR, firewall) | Write 3 real shell scripts: backup, log cleaner, health checker. |
| 3 | Git Fundamentals + Advanced: branching, rebase, merge conflicts, hooks | Resolve at least 2 real merge conflicts. Write a pre-commit hook. |

### Phase 2 — DevOps Core Tools (Weeks 4–8)
| Week | Topic | My commitment |
|------|-------|---------------|
| 4 | Docker: containers, Dockerfile, Compose, volumes, networking | Dockerise my URL shortener project. Multi-stage build, under 20MB. |
| 5 | Jenkins: pipelines, integrations, credentials, Groovy basics | Build a working Jenkinsfile that runs tests + builds Docker image. |
| 6 | GitHub Actions CI/CD + Advanced Dockerfile | Replace Jenkins pipeline with GitHub Actions. OIDC → AWS, no static keys. |
| 7 | Kubernetes Fundamentals: architecture, YAML, pods, deployments, services | Deploy my app to a local Kind cluster. Write every YAML manually. |
| 8 | Kubernetes Advanced + ArgoCD/GitOps: Ingress, Helm, StatefulSets, GitOps | Set up ArgoCD. Any push to main auto-syncs to cluster. |

### Phase 3 — Advanced Concepts (Weeks 9–12)
| Week | Topic | My commitment |
|------|-------|---------------|
| 9 | Ansible + Terraform + DevSecOps | Provision a VPC + EC2 with Terraform. Configure it with Ansible. |
| 10 | AWS Core (VPC, ECS, RDS, IAM, S3) + Azure basics | Deploy full 3-tier app on AWS: ALB → ECS Fargate → RDS in private subnet. |
| 11 | Monitoring: Prometheus, Grafana, CloudWatch, alerting | Add a dashboard and one real alert to my deployed app. |
| 12 | Agentic AI for DevOps + Career Accelerator | Polish GitHub, write 2 ADRs, do 2 mock interviews. |

---

## My Non-Negotiable Rules

- I build something every week — reading without deploying does not count.
- I write down what broke and why after every session (even one line).
- I do not use AI to write my scripts for me — I use it to review them after.
- I treat my Sunday review as seriously as any workday.

---

*Started: ___________*
*Target completion: 90 days from start*
*GitHub repo for all work: github.com/___________/90-days-devops*