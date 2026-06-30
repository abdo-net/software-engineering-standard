# Example: SES Application to a Frontend Application Project

> **NON-NORMATIVE.** This document is a worked example for illustrative purposes only. It does not introduce new rules or extend the architecture of the SES. All authority rests with the SDD.
> **Domain:** Frontend applications [Ref: §4.2]
> **Standard Version:** SES SDD v0.4.0

---

## 1. Mission (using Mission Template)

| Field | Value |
|---|---|
| **Artifact ID** | MIS-FE-001 |
| **Artifact Type** | Mission |
| **Authority Class** | Authoritative |
| **Owner** | Frontend Team Lead |
| **Version** | 1.0.0 |
| **Status** | Active |
| **Standard Version** | SES v0.4.0 |
| **Created** | 2025-02-01 |

### 1.1 Objective

Build a responsive customer-facing dashboard for viewing order history, tracking shipments, and managing account preferences. Must achieve Lighthouse performance score >= 90 and WCAG 2.1 AA accessibility compliance.

### 1.2 Scope

- **In scope:** Order history page with pagination, shipment tracking view, account preferences form, responsive layout (mobile/tablet/desktop), client-side routing, state management.
- **Out of scope:** Payment processing UI, admin features, real-time notifications, mobile native app, offline mode.

### 1.3 Constraints

- Must consume existing REST API at `/api/v2/*` (backend API contract is authoritative).
- Must use the organization's design system component library.
- Must support Chrome, Firefox, Safari, Edge (last 2 versions).
- Development timeline: 6 weeks.
- Bundle size budget: initial load < 200KB gzipped JavaScript.

### 1.4 Expected Deliverables

| Deliverable | Authority Class | Location |
|---|---|---|
| Frontend Design Document | Authoritative | `docs/design/frontend-design.md` |
| ADR-003: State Management Approach | Authoritative | `adr/ADR-003-state-management.md` |
| ADR-004: Component Architecture | Authoritative | `adr/ADR-004-component-architecture.md` |
| Component Library Integration Spec | Authoritative | `docs/component-integration.md` |
| Source Code | Authoritative | `src/` |
| E2E Tests | Authoritative | `tests/e2e/` |
| Component Tests | Authoritative | `src/**/*.test.*` |
| Build Artifacts | Generated | `dist/` |
| Bundle Analysis Report | Generated | `reports/bundle-analysis.html` |

### 1.5 Success Criteria

| ID | Criterion | Verification Method |
|---|---|---|
| SC-1 | Lighthouse performance score >= 90 on all pages | Demonstration |
| SC-2 | WCAG 2.1 AA compliance on all interactive elements | Analysis (axe-core) |
| SC-3 | All API error states handled with user-friendly messages | Test |
| SC-4 | E2E test coverage for all user flows (order history, tracking, preferences) | Test |
| SC-5 | Bundle size < 200KB gzipped JS for initial load | Analysis |
| SC-6 | Responsive layout verified at 320px, 768px, 1440px viewports | Demonstration |

### 1.6 Allowed Operations

| Operation | Included? | Notes |
|---|---|---|
| **DISCOVER** | Yes | Discover existing frontend codebase, design system |
| **ANALYZE** | Yes | Analyze bundle composition, API contract compatibility |
| **TRACE** | Yes | Trace user stories to components and tests |
| **VERIFY** | Yes | Verify API contract conformance, a11y compliance |
| **DOCUMENT** | Yes | Document component API, state management patterns |
| **COMPARE** | Yes | Compare design mockups vs implementation |
| **PLAN** | Yes | ADRs for state management, component architecture |
| **IMPLEMENT** | Yes | Implement components, pages, routing, state |
| **VALIDATE** | Yes | E2E tests, Lighthouse audits, a11y scans |
| **REVIEW** | Yes | Technical review of architecture, code review |

### 1.7 Forbidden Operations

- **No direct database access** -- all data via REST API contract only.
- **No modification of API contract** -- frontend must conform to backend contract.
- **No bypass of design system** without explicit ADR and approval.
- **No modification** of the SES core standard.

### 1.8 Evidence Requirements

| Evidence Item | Required? | Confidence Level | Storage Location |
|---|---|---|---|
| Lighthouse CI report | Yes | A (runtime measurement) | `.lighthouseci/` |
| axe-core accessibility report | Yes | B (static analysis) | `tests/a11y/` |
| E2E test results | Yes | A (runtime) | `tests/e2e/results/` |
| Bundle analysis | Yes | B (build artifact) | `reports/bundle-analysis.html` |
| Code review records | Yes | B (source review) | `reviews/` |
| ADR approval records | Yes | B (documentation) | `adr/` |

---

## 2. Discovery (using Discovery Specification)

> Discovery is governed by §25. Discovery MUST combine static and dynamic analysis and cross-validate per DSC-3. [Ref: §25.4, DSC-3]

### 2.1 Discovery Summary

| Layer | Activity | Findings | Confidence |
|---|---|---|---|
| **Inventory** | Technology detection | React 18.2, TypeScript 5.3, Vite 5.0, Tailwind CSS 3.4 | B |
| **Inventory** | Build system detection | Vite dev server + production build, pnpm package manager | B |
| **Inventory** | Repository inventory | `src/` (components, pages, hooks, stores), `tests/` (unit, e2e), `public/` | B |
| **Structure** | Dependency discovery | 32 runtime dependencies, 48 dev dependencies; React Query, Zustand, React Router | B |
| **Structure** | API contract discovery | OpenAPI spec at `spec/openapi.yaml` -- 18 endpoints documented | B |
| **Security** | Authentication flow discovery | JWT stored in httpOnly cookie; refresh token rotation implemented | A (runtime confirmed) |
| **Behavior** | Workflow discovery | 3 user flows: order history -> detail view, tracking -> status updates, preferences -> save | C (documented in user stories) |

### 2.2 Key Discovery Findings

| Finding ID | Description | Impact | Confidence |
|---|---|---|---|
| F-005 | Existing project uses Redux Toolkit (overkill for scope) | State management ADR needed | B |
| F-006 | No existing E2E test framework | Must select and configure Playwright or Cypress | B |
| F-007 | Design system version 3.2 available (project uses 2.8) | Upgrade path needed | C |
| F-008 | API spec v2 defines 3 endpoints not yet implemented by backend | Contract mismatch risk | B |

---

## 3. Key Decisions (using Decision Record)

> A Decision MUST cite the Evidence and the Impact Analysis that justify it per DEC-2. [Ref: §35.3, DEC-2]

### ADR-003: State Management Approach

| Field | Value |
|---|---|
| **Decision** | Use Zustand for client state; React Query for server state |
| **Decision Context** | Finding F-005 shows Redux Toolkit is overkill; need lightweight client state + robust server state caching |
| **Alternatives** | Redux Toolkit (rejected: too verbose for this scope); Jotai (rejected: less team familiarity); Context API only (rejected: insufficient for server state) |
| **Evidence** | F-005; team skills survey; Zustand + React Query community adoption data |
| **Impact** | All server state uses React Query hooks; form state uses Zustand stores; no Redux dependency |
| **Dependencies** | ADR-004 (component architecture determines hook patterns) |
| **Approval** | Frontend Team Lead |
| **Status** | Approved |
| **Superseded By** | -- |

### ADR-004: Component Architecture

| Field | Value |
|---|---|
| **Decision** | Adopt container/presenter pattern with co-located tests; feature-based directory structure |
| **Decision Context** | Need clear separation between data fetching and UI; team has 4 developers working in parallel |
| **Alternatives** | Atomic design (rejected: too granular for this timeline); pages-only (rejected: poor reusability) |
| **Evidence** | Team size; project timeline; feature count |
| **Impact** | Directory structure: `src/features/{orders,tracking,preferences}/`; shared components in `src/components/` |
| **Dependencies** | ADR-003 (state hooks used by container components) |
| **Approval** | Frontend Team Lead |
| **Status** | Approved |
| **Superseded By** | -- |

---

## 4. Impact Analysis (using Impact Analysis Model)

> Impact analysis MUST use the dependency view and traceability per IMP-2. [Ref: §36.3, IMP-2]

| Dimension | Affected? | Impact Description | Mitigation |
|---|---|---|---|
| **Affected Components** | Yes | 3 new feature modules; shared layout updates | Feature flags for gradual rollout |
| **Dependencies** | Yes | Adds zustand, @tanstack/react-query, @tanstack/react-query-devtools | Pin versions; verify bundle budget |
| **Execution Flow** | Yes | New routes: `/orders`, `/orders/:id`, `/tracking/:id`, `/preferences` | Route guards for auth; lazy loading |
| **Database** | No | Frontend has no direct DB access | N/A (per constraint) |
| **API** | Yes | Consumes 8 of 18 API endpoints; 3 endpoints pending backend implementation | Mock API for frontend development |
| **Security** | Yes | Auth token handling; route-level access control | Reuse existing auth hook; add route guards |
| **Tests** | Yes | Unit tests for 15 components; E2E for 3 user flows | Component Testing with Vitest; E2E with Playwright |
| **Documentation** | Yes | Component Storybook; API integration guide | Auto-generate from JSDoc comments |
| **Deployment** | Yes | New static build artifact; CDN cache invalidation | Versioned asset URLs; preview deployments per PR |
| **Validation** | Yes | Lighthouse CI in PR checks; axe-core in E2E; visual regression | Automated in CI pipeline |

---

## 5. Conformance Assertion

| Field | Value |
|---|---|
| **Artifact ID** | CA-FE-001 |
| **Artifact Type** | Conformance Assertion |
| **Authority Class** | Authoritative |
| **Project Name** | Customer Dashboard Frontend |
| **SES Version** | v0.4.0 |
| **Assertion Date** | 2025-03-20 |
| **Asserting Party** | Frontend Team Lead |
| **Valid Until** | 2025-09-20 |

### Requirements Satisfied

| Requirement Class | SDD Reference | Verification Method | Status | Evidence |
|---|---|---|---|---|
| Engineering Lifecycle | §12 | Inspection | Pass | Follows understanding -> planning -> implementation -> validation |
| Stage Model | §13 | Inspection | Pass | Each stage has entry/exit criteria and evidence |
| Knowledge Model | §14 | Inspection | Pass | ADRs are immutable; findings have confidence levels |
| Review Model | §15 | Inspection | Pass | Technical review completed for architecture; code reviews for all PRs |
| Validation Model | §16 | Test + Demonstration | Pass | Lighthouse >= 90; E2E tests pass; a11y scan clean |
| Artifact Architecture | §11 | Inspection | Pass | Correct authority class assignment; generated artifacts reproducible |
| Mission Model | §32 | Inspection | Pass | All 8 mission elements defined |
| Decision Model | §35 | Inspection | Pass | ADRs have all 9 required fields; approved status |
| Impact Analysis | §36 | Inspection | Pass | All 10 dimensions analyzed |
| Integrity Rules | §40 | Analysis | Pass | No undocumented APIs (frontend consumes documented contract); all decisions recorded |

### Verdict

| Field | Value |
|---|---|
| **Overall Verdict** | **Pass** |
| **Conformance Statement** | The Customer Dashboard Frontend project satisfies the applicable SES v0.4.0 requirements. |
| **Conditions** | Bundle size monitored in CI; Lighthouse CI gates PR merges |

---

> **SDD sections cited in this example:** §4.2 (domain), §11 (artifact authority), §12 (lifecycle), §13 (stage model), §14 (knowledge model), §15 (review model), §16 (validation), §25 (discovery), §26 (confidence), §32 (mission model), §35 (decision model), §36 (impact analysis), §40 (integrity rules).
