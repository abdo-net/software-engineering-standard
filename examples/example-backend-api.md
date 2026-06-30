# Example: SES Application to a Backend API Project

> **NON-NORMATIVE.** This document is a worked example for illustrative purposes only. It does not introduce new rules or extend the architecture of the SES. All authority rests with the SDD.
> **Domain:** Backend APIs [Ref: §4.2]
> **Standard Version:** SES SDD v0.4.0

---

## 1. Mission (using Mission Template)

| Field | Value |
|---|---|
| **Artifact ID** | MIS-BEAPI-001 |
| **Artifact Type** | Mission |
| **Authority Class** | Authoritative |
| **Owner** | Backend Team Lead |
| **Version** | 1.0.0 |
| **Status** | Active |
| **Standard Version** | SES v0.4.0 |
| **Created** | 2025-01-15 |

### 1.1 Objective

Implement a RESTful API for customer order management with CRUD operations, authentication, and rate limiting. The API must support 1000 concurrent users with p99 latency under 200ms.

### 1.2 Scope

- **In scope:** Customer endpoints (CRUD), order endpoints (CRUD), authentication middleware, rate limiting, database schema, API documentation (OpenAPI), integration tests.
- **Out of scope:** Frontend UI, mobile clients, payment processing, third-party integrations, admin dashboard.

### 1.3 Constraints

- Must use existing PostgreSQL 15 database cluster (organizational standard).
- Must deploy to existing Kubernetes cluster (organizational standard).
- Must comply with organizational security policy (OAuth 2.0 + JWT).
- Development timeline: 8 weeks.
- Must maintain backward compatibility with existing v1 API clients during transition.

### 1.4 Expected Deliverables

| Deliverable | Authority Class | Location |
|---|---|---|
| API Design Document (this artifact) | Authoritative | `docs/design/api-design.md` |
| ADR-001: Framework Selection | Authoritative | `adr/ADR-001-framework-selection.md` |
| ADR-002: Database Schema Design | Authoritative | `adr/ADR-002-database-schema.md` |
| OpenAPI Specification | Authoritative | `spec/openapi.yaml` |
| Source Code | Authoritative | `src/` |
| Integration Tests | Authoritative | `tests/integration/` |
| API Documentation (rendered) | Generated | `docs/generated/` |
| Dependency Graph | Generated | `docs/generated/dependencies/` |

### 1.5 Success Criteria

| ID | Criterion | Verification Method |
|---|---|---|
| SC-1 | All CRUD endpoints return correct HTTP status codes per RFC 9110 | Test |
| SC-2 | p99 latency under 200ms at 1000 concurrent users | Demonstration |
| SC-3 | 100% of endpoints documented in OpenAPI spec | Inspection |
| SC-4 | Integration test coverage >= 80% | Analysis |
| SC-5 | Security scan passes with zero critical findings | Analysis |
| SC-6 | All ADRs approved and traceable to implementation | Inspection |

### 1.6 Allowed Operations

| Operation | Included? | Notes |
|---|---|---|
| **DISCOVER** | Yes | Discover existing API patterns, DB schema |
| **ANALYZE** | Yes | Analyze dependencies, performance characteristics |
| **TRACE** | Yes | Trace requirements to implementation |
| **VERIFY** | Yes | Verify against OpenAPI spec |
| **DOCUMENT** | Yes | Produce OpenAPI spec, design doc |
| **COMPARE** | Yes | Compare implementation against spec |
| **PLAN** | Yes | Create ADRs, design documents |
| **IMPLEMENT** | Yes | Implement API endpoints |
| **VALIDATE** | Yes | Run integration tests, performance tests |
| **REVIEW** | Yes | Technical review of design, code review of implementation |

### 1.7 Forbidden Operations

- **No production deployment** without explicit Management Review approval.
- **No database migration** without separate database impact analysis Mission.
- **No breaking changes** to existing v1 API contract.
- **No modification** of the SES core standard.

### 1.8 Evidence Requirements

| Evidence Item | Required? | Confidence Level | Storage Location |
|---|---|---|---|
| OpenAPI specification validated | Yes | B (source code) | `spec/openapi.yaml` |
| Integration test results | Yes | A (runtime) | `tests/results/` |
| Performance benchmark results | Yes | A (runtime) | `tests/perf/results/` |
| Security scan report | Yes | B (static analysis) | `tests/security/` |
| Code review records | Yes | B (source review) | `reviews/` |
| ADR approval records | Yes | B (documentation) | `adr/` |

---

## 2. Discovery (using Discovery Specification)

> Discovery is governed by §25. An unknown system SHALL pass through Discovery before any modification per DSC-1. [Ref: §25.4, DSC-1]

### 2.1 Discovery Summary

| Layer | Activity | Findings | Confidence |
|---|---|---|---|
| **Inventory** | Technology detection | Python 3.11, FastAPI 0.104, PostgreSQL 15, Docker, Kubernetes | B |
| **Inventory** | Build system detection | Docker multi-stage builds, GitHub Actions CI | B |
| **Inventory** | Repository inventory | Monorepo: `src/`, `tests/`, `adr/`, `spec/`, `docs/` | B |
| **Structure** | Dependency discovery | 47 Python packages, 3 external services (auth, payment, notification) | B |
| **Structure** | API discovery | 12 existing v1 endpoints at `/api/v1/*` | A (runtime confirmed) |
| **Structure** | Database discovery | 8 tables: customers, orders, order_items, products, categories, users, roles, audit_log | B |
| **Security** | Authentication discovery | OAuth 2.0 + JWT via external auth service | B |
| **Security** | Authorization discovery | RBAC with roles: admin, user, readonly | B |
| **Behavior** | Workflow discovery | Order lifecycle: created -> paid -> fulfilled -> shipped -> delivered | C (documented) |

### 2.2 Key Discovery Findings

| Finding ID | Description | Impact | Confidence |
|---|---|---|---|
| F-001 | Existing v1 API uses synchronous SQLAlchemy; v2 should use async for performance | Architecture decision | B |
| F-002 | No existing rate limiting implementation | Must be designed from scratch | B |
| F-003 | Customer table lacks `updated_at` timestamp | Schema migration required | B |
| F-004 | Auth service deprecating legacy token format in 90 days | Must use new token format | C |

---

## 3. Key Decisions (using Decision Record)

> Every engineering decision MUST be recorded with all nine fields per DEC-1. [Ref: §35.3, DEC-1]

### ADR-001: API Framework Selection

| Field | Value |
|---|---|
| **Decision** | Use FastAPI (async mode) for the v2 API implementation |
| **Decision Context** | Team has existing FastAPI experience; async requirement from performance criteria; existing v1 uses Flask (sync) which cannot meet latency targets |
| **Alternatives** | Flask + async extensions (rejected: immature ecosystem); Django REST Framework (rejected: too heavy, sync-first); Go/Gin (rejected: team expertise gap) |
| **Evidence** | SC-2 (p99 < 200ms); F-001 (sync SQLAlchemy bottleneck); team skills inventory |
| **Impact** | All v2 endpoints use async SQLAlchemy + FastAPI; migration guide needed for v1 -> v2 transition; training budget for junior devs |
| **Dependencies** | ADR-002 (database schema); async PostgreSQL driver (asyncpg) |
| **Approval** | Backend Team Lead, Architecture Board |
| **Status** | Approved |
| **Superseded By** | -- |

### ADR-002: Database Access Pattern

| Field | Value |
|---|---|
| **Decision** | Use async SQLAlchemy 2.0 with repository pattern and explicit transaction boundaries |
| **Decision Context** | ADR-001 chose FastAPI async; need database layer that supports async; repository pattern provides testability and separation of concerns |
| **Alternatives** | Raw asyncpg (rejected: too low-level, error-prone); Django ORM (rejected: coupled to Django); Prisma (rejected: new dependency, team unfamiliar) |
| **Evidence** | ADR-001; F-001; industry practice for FastAPI applications |
| **Impact** | All DB access goes through repository classes; unit tests use in-memory SQLite; integration tests use test PostgreSQL container |
| **Dependencies** | ADR-001; PostgreSQL 15 cluster availability |
| **Approval** | Backend Team Lead |
| **Status** | Approved |
| **Superseded By** | -- |

---

## 4. Impact Analysis (using Impact Analysis Model)

> Every Implementation MUST begin with an impact analysis spanning all dimensions per IMP-1. [Ref: §36.3, IMP-1]

| Dimension | Affected? | Impact Description | Mitigation |
|---|---|---|---|
| **Affected Components** | Yes | New `v2/` module in `src/`; new router registration in main app | Modular design, no changes to v1 |
| **Dependencies** | Yes | Adds asyncpg, pydantic v2, httpx (testing) | Pin versions; update SBOM |
| **Execution Flow** | Yes | Request -> FastAPI router -> Service -> Repository -> asyncpg -> PostgreSQL | Repository pattern isolates changes |
| **Database** | Yes | Add `updated_at` to customers; create order_items if not exists | Migration scripts with rollback |
| **API** | Yes | New `/api/v2/*` prefix; OpenAPI spec v2 | Maintain v1 compatibility per constraints |
| **Security** | Yes | New endpoints need auth middleware, rate limiting config | Reuse existing auth service; rate limiter per endpoint |
| **Tests** | Yes | New integration test suite; performance tests | Parallel test execution in CI |
| **Documentation** | Yes | New OpenAPI spec; README update; migration guide | Auto-generated docs from spec |
| **Deployment** | Yes | New container image tag; K8s service route for v2 | Blue-green deployment |
| **Validation** | Yes | Integration tests, performance tests, security scan | Automated in CI pipeline |

---

## 5. Conformance Assertion

| Field | Value |
|---|---|
| **Artifact ID** | CA-BEAPI-001 |
| **Artifact Type** | Conformance Assertion |
| **Authority Class** | Authoritative |
| **Project Name** | Customer Order Management API |
| **SES Version** | v0.4.0 |
| **Assertion Date** | 2025-03-15 |
| **Asserting Party** | Backend Team Lead |
| **Valid Until** | 2025-09-15 |

### Requirements Satisfied

| Requirement Class | SDD Reference | Verification Method | Status | Evidence |
|---|---|---|---|---|
| Engineering Lifecycle | §12 | Inspection | Pass | Design doc follows lifecycle phases |
| Stage Model | §13 | Inspection | Pass | All stages define entry/exit criteria |
| Knowledge Model | §14 | Inspection | Pass | ADRs have provenance; facts have confidence |
| Review Model | §15 | Inspection | Pass | Code reviews recorded; technical review completed |
| Validation Model | §16 | Test | Pass | Integration tests pass; performance criteria met |
| Artifact Architecture | §11 | Inspection | Pass | Authority classes correctly assigned |
| Mission Model | §32 | Inspection | Pass | All 8 mission elements defined |
| Decision Model | §35 | Inspection | Pass | ADRs have all 9 fields; immutable once approved |
| Impact Analysis | §36 | Inspection | Pass | All 10 dimensions analyzed |
| Integrity Rules | §40 | Analysis | Pass | No INT violations detected |

### Verdict

| Field | Value |
|---|---|
| **Overall Verdict** | **Pass** |
| **Conformance Statement** | The Customer Order Management API project satisfies the applicable SES v0.4.0 requirements. |
| **Conditions** | None |

---

> **SDD sections cited in this example:** §4.2 (domain), §11 (artifact authority), §12 (lifecycle), §13 (stage model), §14 (knowledge model), §15 (review model), §16 (validation), §25 (discovery), §26 (confidence), §32 (mission model), §35 (decision model), §36 (impact analysis), §40 (integrity rules).
