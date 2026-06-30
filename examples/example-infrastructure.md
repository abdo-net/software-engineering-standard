# Example: SES Application to an Infrastructure Project

> **NON-NORMATIVE.** This document is a worked example for illustrative purposes only. It does not introduce new rules or extend the architecture of the SES. All authority rests with the SDD.
> **Domain:** Infrastructure projects [Ref: §4.2]
> **Standard Version:** SES SDD v0.4.0

---

## 1. Mission (using Mission Template)

| Field | Value |
|---|---|
| **Artifact ID** | MIS-INFRA-001 |
| **Artifact Type** | Mission |
| **Authority Class** | Authoritative |
| **Owner** | Platform Engineering Lead |
| **Version** | 1.0.0 |
| **Status** | Active |
| **Standard Version** | SES v0.4.0 |
| **Created** | 2025-01-20 |

### 1.1 Objective

Provision and configure a Kubernetes cluster environment for the customer order management API and frontend dashboard, including monitoring, logging, secret management, and automated deployment pipelines. Must achieve 99.9% uptime SLA and support zero-downtime deployments.

### 1.2 Scope

- **In scope:** Kubernetes cluster provisioning (staging + production), namespace configuration, ingress controller with TLS, horizontal pod autoscaling, monitoring stack (Prometheus + Grafana), centralized logging (Fluent Bit + Loki), secret management (external-secrets operator), CI/CD pipeline (GitHub Actions -> ArgoCD), network policies, pod security policies.
- **Out of scope:** Application code changes, database provisioning (managed service), DNS management (handled by central IT), physical hardware procurement.

### 1.3 Constraints

- Must use organization's approved cloud provider and region.
- Must comply with organizational security baseline (CIS Kubernetes Benchmark v1.8).
- Must integrate with existing identity provider for cluster access (SSO).
- All infrastructure MUST be defined as code (Terraform + Helm).
- No privileged containers in application workloads.
- Development timeline: 10 weeks.

### 1.4 Expected Deliverables

| Deliverable | Authority Class | Location |
|---|---|---|
| Infrastructure Design Document | Authoritative | `docs/design/infrastructure-design.md` |
| ADR-005: Cluster Architecture | Authoritative | `adr/ADR-005-cluster-architecture.md` |
| ADR-006: Secret Management Strategy | Authoritative | `adr/ADR-006-secret-management.md` |
| ADR-007: Monitoring and Alerting Design | Authoritative | `adr/ADR-007-monitoring-alerting.md` |
| Terraform Modules | Authoritative | `terraform/` |
| Helm Charts | Authoritative | `helm/` |
| CI/CD Pipeline Definitions | Authoritative | `.github/workflows/`, `argocd/` |
| Network Policy Definitions | Authoritative | `policies/network/` |
| Runbooks | Authoritative | `docs/runbooks/` |
| Architecture Diagrams | Authoritative | `docs/diagrams/` |
| Terraform Plan Output | Generated | `terraform/plans/` |
| Dependency Graph | Generated | `docs/generated/dependencies/` |

### 1.5 Success Criteria

| ID | Criterion | Verification Method |
|---|---|---|
| SC-1 | Kubernetes cluster provisioned and healthy (all control plane components Ready) | Test |
| SC-2 | 99.9% uptime SLA over 30-day measurement period | Demonstration |
| SC-3 | Zero-downtime deployment verified (no failed requests during 10 rollouts) | Test |
| SC-4 | All secrets externalized (no secrets in Git, no secrets in pod env vars) | Analysis |
| SC-5 | Monitoring covers all workloads (CPU, memory, disk, custom business metrics) | Inspection |
| SC-6 | CIS Kubernetes Benchmark >= 80% compliance | Analysis (kube-bench) |
| SC-7 | Network policies enforce least-privilege pod-to-pod communication | Inspection |

### 1.6 Allowed Operations

| Operation | Included? | Notes |
|---|---|---|
| **DISCOVER** | Yes | Discover existing infrastructure, network topology, IAM policies |
| **ANALYZE** | Yes | Analyze resource requirements, security posture, cost estimates |
| **TRACE** | Yes | Trace infrastructure changes to requirements |
| **VERIFY** | Yes | Verify Terraform plans, security scan results |
| **DOCUMENT** | Yes | Document architecture, runbooks, incident response procedures |
| **COMPARE** | Yes | Compare actual state vs desired state (Terraform drift detection) |
| **PLAN** | Yes | ADRs for architecture, capacity planning |
| **IMPLEMENT** | Yes | Implement Terraform modules, Helm charts, pipelines |
| **VALIDATE** | Yes | Validate deployments, run chaos experiments |
| **REVIEW** | Yes | Security review of infrastructure; code review for IaC |

### 1.7 Forbidden Operations

- **No manual changes to infrastructure** -- all changes via Terraform/Helm + GitOps.
- **No secrets in version control** -- all secrets via external-secrets operator.
- **No privileged containers** in application workloads.
- **No modification** of the SES core standard.

### 1.8 Evidence Requirements

| Evidence Item | Required? | Confidence Level | Storage Location |
|---|---|---|---|
| Terraform plan/apply output | Yes | B (source code) | `terraform/plans/` |
| kube-bench security scan | Yes | B (static analysis) | `scans/kube-bench/` |
| Deployment verification logs | Yes | A (runtime) | `logs/deployments/` |
| Uptime monitoring data | Yes | A (runtime) | Grafana dashboards |
| Network policy validation | Yes | B (static analysis) | `scans/network/` |
| Code review records | Yes | B (source review) | `reviews/` |
| ADR approval records | Yes | B (documentation) | `adr/` |

---

## 2. Discovery (using Discovery Specification)

> Discovery is complete only when the "Discovery Complete" criteria are objectively met per DSC-5. [Ref: §25.4, DSC-5]

### 2.1 Discovery Summary

| Layer | Activity | Findings | Confidence |
|---|---|---|---|
| **Inventory** | Technology detection | Kubernetes 1.29, Terraform 1.7, Helm 3.14, ArgoCD 2.9, GitHub Actions | B |
| **Inventory** | Build system detection | Terraform + Helm + ArgoCD GitOps pipeline | B |
| **Inventory** | Repository inventory | `terraform/`, `helm/`, `policies/`, `docs/`, `argocd/` | B |
| **Inventory** | Runtime environment detection | Managed Kubernetes service, 3 AZs, VPC with private subnets | B |
| **Structure** | Dependency discovery | 12 Terraform modules, 8 Helm charts, 2 ArgoCD app-of-apps | B |
| **Security** | Authentication discovery | SSO via OIDC for cluster access; no static kubeconfig | B |
| **Security** | Authorization discovery | RBAC with namespace-level roles; no cluster-admin for apps | B |
| **Behavior** | Workflow discovery | PR -> Terraform Plan -> Review -> Merge -> ArgoCD Sync -> Validate | C (documented) |

### 2.2 Key Discovery Findings

| Finding ID | Description | Impact | Confidence |
|---|---|---|---|
| F-009 | Existing cluster uses Kubernetes 1.27 (2 versions behind) | Upgrade plan needed | B |
| F-010 | No pod security standards enforced at namespace level | Must add PSS labels | B |
| F-011 | Network policies missing in 60% of namespaces | Security gap | B |
| F-012 | Monitoring stack covers only node-level metrics | Must add workload and custom metrics | C |

---

## 3. Key Decisions (using Decision Record)

> A Decision is immutable once Approved; change occurs only by superseding per DEC-3. [Ref: §35.3, DEC-3]

### ADR-005: Cluster Architecture

| Field | Value |
|---|---|
| **Decision** | Use managed Kubernetes with 3 availability zones; separate node pools for system workloads and application workloads |
| **Decision Context** | Need high availability; cost optimization via right-sized node pools; organizational preference for managed control plane |
| **Alternatives** | Self-managed control plane (rejected: operational overhead); single AZ (rejected: no HA); uniform node pool (rejected: noisy neighbor risk) |
| **Evidence** | 99.9% SLA requirement; cost analysis; organizational infrastructure policy |
| **Impact** | Two node pools: `system` (monitoring, ingress, ArgoCD) and `apps` (API, frontend); taints/tolerations for separation |
| **Dependencies** | Cloud provider account; VPC with 3 AZs; IAM roles for cluster |
| **Approval** | Platform Engineering Lead, Security Team |
| **Status** | Approved |
| **Superseded By** | -- |

### ADR-006: Secret Management Strategy

| Field | Value |
|---|---|
| **Decision** | Use external-secrets operator with cloud provider secret manager; no secrets in Git or environment variables |
| **Decision Context** | Security constraint mandates no secrets in version control; need centralized secret rotation; multiple environments |
| **Alternatives** | Sealed Secrets (rejected: key management complexity); Vault (rejected: additional infrastructure overhead); SOPS (rejected: less integration with secret manager) |
| **Evidence** | Security baseline requirement; team operational capacity; existing secret manager availability |
| **Impact** | All workloads use `ExternalSecret` CRDs; secrets managed in central secret manager; automatic rotation supported |
| **Dependencies** | Cloud secret manager provisioned; external-secrets operator installed |
| **Approval** | Platform Engineering Lead, Security Team |
| **Status** | Approved |
| **Superseded By** | -- |

### ADR-007: Monitoring and Alerting Design

| Field | Value |
|---|---|
| **Decision** | Prometheus + Grafana for metrics; Fluent Bit + Loki for logs; PagerDuty for alerting; SLO-based alerting |
| **Decision Context** | Need comprehensive observability; existing organizational PagerDuty subscription; SLOs defined in Mission |
| **Alternatives** | Datadog (rejected: cost, vendor lock-in per PR-3); CloudWatch only (rejected: limited dashboarding); ELK stack (rejected: resource overhead) |
| **Evidence** | Cost comparison; resource requirements; team expertise |
| **Impact** | Prometheus deployed in `system` node pool; Grafana dashboards as code; alert rules in Git; SLO burn rate alerts |
| **Dependencies** | ADR-005 (node pool for monitoring); ingress for Grafana access |
| **Approval** | Platform Engineering Lead |
| **Status** | Approved |
| **Superseded By** | -- |

---

## 4. Impact Analysis (using Impact Analysis Model)

> Identified impacts MUST be recorded as evidence and MUST feed the authorizing Decision per IMP-3. [Ref: §36.3, IMP-3]

| Dimension | Affected? | Impact Description | Mitigation |
|---|---|---|---|
| **Affected Components** | Yes | New Terraform modules (12), Helm charts (8), ArgoCD apps; existing cluster upgrade | Staged rollout: staging first, production after validation |
| **Dependencies** | Yes | Managed K8s provider API; secret manager; IAM policies; container registry | Module-level dependency management; explicit provider versions |
| **Execution Flow** | Yes | GitOps workflow: PR -> plan -> review -> merge -> ArgoCD auto-sync | Branch protection rules; required reviewers; ArgoCD sync windows |
| **Database** | No | Infrastructure project has no direct database | N/A |
| **API** | Yes | Ingress rules for API endpoints; cert-manager for TLS | OpenAPI spec referenced for route configuration |
| **Security** | Yes | PSS labels, network policies, RBAC, secret management | Security review gate; kube-bench in CI |
| **Tests** | Yes | Terraform validate/plan, Helm lint, conftest (OPA), deployment verification | Automated in CI; conftest for policy-as-code |
| **Documentation** | Yes | Architecture diagrams, runbooks, incident response procedures | Runbook template per service; diagrams as code (Mermaid) |
| **Deployment** | Yes | ArgoCD GitOps pipeline; blue-green via Helm values; canary via Flagger | Progressive delivery; automatic rollback on health check failure |
| **Validation** | Yes | Terraform plan validation, security scanning, deployment verification, chaos testing | CI pipeline gates; kube-bench; pod-security standards check |

---

## 5. Conformance Assertion

| Field | Value |
|---|---|
| **Artifact ID** | CA-INFRA-001 |
| **Artifact Type** | Conformance Assertion |
| **Authority Class** | Authoritative |
| **Project Name** | Customer Platform Infrastructure |
| **SES Version** | v0.4.0 |
| **Assertion Date** | 2025-04-01 |
| **Asserting Party** | Platform Engineering Lead |
| **Valid Until** | 2025-10-01 |

### Requirements Satisfied

| Requirement Class | SDD Reference | Verification Method | Status | Evidence |
|---|---|---|---|---|
| Engineering Lifecycle | §12 | Inspection | Pass | Follows full lifecycle: discovery -> analysis -> planning -> implementation -> validation |
| Stage Model | §13 | Inspection | Pass | Each stage defined with entry/exit criteria; SG-1 through SG-4 satisfied |
| Knowledge Model | §14 | Inspection | Pass | All ADRs have provenance; findings carry confidence levels A-C |
| Review Model | §15 | Inspection | Pass | Security review completed; technical review for architecture; code review for IaC |
| Validation Model | §16 | Test + Analysis | Pass | kube-bench scan pass; deployment verification pass; Terraform plan validation pass |
| Artifact Architecture | §11 | Inspection | Pass | Correct authority classification; Terraform plans and dependency graphs are Generated |
| Mission Model | §32 | Inspection | Pass | All 8 mission elements defined and verifiable |
| Decision Model | §35 | Inspection | Pass | 3 ADRs approved with all 9 required fields; immutable per DEC-3 |
| Impact Analysis | §36 | Inspection | Pass | All 10 dimensions analyzed; impacts fed decisions per IMP-3 |
| Integrity Rules | §40 | Analysis | Pass | All configurations documented (INT-6); security rules documented (INT-8); no undocumented dependencies (INT-3) |

### Verdict

| Field | Value |
|---|---|
| **Overall Verdict** | **Pass** |
| **Conformance Statement** | The Customer Platform Infrastructure project satisfies the applicable SES v0.4.0 requirements. |
| **Conditions** | Cluster upgrade from 1.27 to 1.29 tracked as separate follow-up Mission; kube-bench re-scan required quarterly |

---

> **SDD sections cited in this example:** §4.2 (domain), §11 (artifact authority), §12 (lifecycle), §13 (stage model), §14 (knowledge model), §15 (review model), §16 (validation), §25 (discovery), §26 (confidence), §32 (mission model), §35 (decision model), §36 (impact analysis), §40 (integrity rules).
