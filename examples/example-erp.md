# Example: SES Applied to an ERP System — Acme Manufacturing ERP

> **NON-NORMATIVE** — This document is a worked example for illustrative purposes only.
> It demonstrates how the Software Engineering Standard (SES) MAY be applied to a project
> in the ERP domain. [Ref: §4.2 Domains the SES Must Cover; §24 Phase 9 — Worked examples]
> This example introduces no new rules and extends no architecture.

---

## Artifact Metadata

| Field | Value |
|---|---|
| **Object ID** | EX-ERP-001 |
| **Object Type** | Example |
| **Authority Class** | Generated |
| **Owner** | SES Phase 9 — Example Writer |
| **Lifecycle State** | COMPLETED |
| **Status** | Accepted |
| **Version** | 0.1.0 |
| **Parent Objects** | SES v0.4.0 |
| **Repository Location** | `examples/example-erp.md` |
| **Generated From** | SDD v0.4.0 §32.2, §25.3, §35.2, §13.2, §16.5 |

---

## 1. Fictional Project Context

**Project name:** Acme Manufacturing ERP (codename: "ApexERP")
**Domain:** Enterprise Resource Planning — inventory, procurement, finance, HR
**Context:** A 15-year-old monolithic ERP system with 2.4M LOC in Java EE, Oracle database, EJB 2.x, and a Swing desktop client. The organization needs to add a REST API layer for mobile warehouse operations while preserving existing workflows.

---

## 2. Mission Creation (§32.2)

The Mission is created following the eight-element structure mandated by §32.2. [Ref: §32.2 Mission Structure; MIS-1, MIS-2]

| Mission Element | Content |
|---|---|
| **Objective** | Add a REST API layer to ApexERP enabling mobile warehouse scanning (goods receipt, picking, stock transfer) without disrupting existing Swing client operations. |
| **Scope** | In scope: API design, contract specification, warehouse module integration, authentication/authorization for mobile clients, characterization tests for existing workflows. Out of scope: UI development, changes to procurement/finance/HR modules, database schema changes beyond the warehouse module. |
| **Constraints** | CN-BUDGET: Fixed budget of 480 engineer-hours. CN-TIME: Must deliver before Q3 peak season. CN-INTEGRITY: Zero downtime during deployment; existing Swing workflows MUST NOT be disrupted. CN-DB: No schema changes to tables owned by finance/HR modules. |
| **Expected Deliverables** | (1) OpenAPI contract specification; (2) REST API implementation; (3) ADR for authentication approach; (4) Characterization test suite for warehouse workflows; (5) Deployment plan with rollback procedure; (6) Updated dependency map. |
| **Success Criteria** | SC-API: All 12 endpoints respond per OpenAPI spec (verified by contract test). SC-TEST: ≥80% of existing warehouse workflows covered by characterization tests. SC-REGRESSION: Zero regression in Swing client acceptance tests. SC-PERF: API p95 latency <200ms under 100 concurrent users. |
| **Allowed Operations** | DISCOVER, ANALYZE, TRACE, VERIFY, DOCUMENT, PLAN, IMPLEMENT, VALIDATE, REVIEW [Ref: §34.2 Operations and Governing Sections] |
| **Forbidden Operations** | Direct database modification outside warehouse module; modification of EJB session beans used by finance/HR; deletion of existing Swing client endpoints. |
| **Evidence Requirements** | All facts carry confidence level per §26; all decisions recorded per §35; all APIs carry contract specs per §11.3; conformance assertion recorded per §16.5. |

> **Mission validation note:** The Mission above defines all eight elements required by MIS-2. Allowed Operations are drawn from the closed set in §34.2 per MIS-3. [Ref: MIS-2; MIS-3]

---

## 3. Discovery Activities (§25.3)

Discovery is performed following the mandated activity set from §25.3. [Ref: §25.3 Mandated Discovery Activities; DSC-1, DSC-2, DSC-3]

### 3.1 Discovery Results Summary

| Activity Layer | Activities Performed | Key Findings | Confidence |
|---|---|---|---|
| **Inventory Layer** | Asset Inventory; Repository Inventory; Technology Detection; Build System Detection; Runtime Environment Detection | Monorepo in Git. Java EE 6, JBoss AS 7.2, Ant+Ivy build, Oracle 12c, JBoss running on RHEL 7. JVM heap 4GB in production. | B (source-confirmed) |
| **Structure Layer** | Dependency Discovery; Module Discovery; API Discovery; Database Discovery; Configuration Discovery | 47 Maven-style modules (actually Ant-built). 156 EJB interfaces. 213 database tables; 38 belong to warehouse module. JNDI datasources configured in `standalone.xml`. | B/C (mixed source/doc) |
| **Security Layer** | Security Discovery; Authentication Discovery; Authorization Discovery | JAAS realm backed by Oracle. Role-based: `WAREHOUSE_CLERK`, `WAREHOUSE_MGR`, `ADMIN`. No OAuth/JWT. Passwords hashed with SHA-256 (legacy — recorded as risk). | B (source) |
| **Behavior Layer** | Event Discovery; Workflow Discovery; Execution Flow Recovery; Runtime Observation | Warehouse workflow: `GoodsReceipt → QualityCheck → Putaway → StockUpdate`. Triggered by EJB message-driven beans. JMS queue `warehouse.incoming`. | A/B (runtime + source triangulated) |
| **Analysis Methods** | Static Analysis; Dynamic Analysis; Cross-Validation (triangulation) | SonarQube: 1,847 issues, 12 critical. Triangulation: runtime JMX traces confirm call graph from static analysis. One divergence found in JMS message path — recorded as finding F-003. | D (triangulated) |
| **Synthesis** | Architecture Recovery; Knowledge Extraction; Evidence Collection; Documentation; Verification | Recovered: 3-layer architecture (Presentation → EJB → DAO). No service layer abstraction. Knowledge extracted to `docs/discovery/apexerp-knowledge.md`. | D |

### 3.2 Discovery Evidence Sample

| Fact ID | Statement | Confidence | Evidence Source | Verification Status |
|---|---|---|---|---|
| F-001 | ApexERP uses EJB 2.x session beans for business logic | B | `src/ejb/` contains 89 `*Bean.java` files with `ejb-jar.xml` | Source inspection |
| F-002 | Warehouse module owns 38 tables prefixed `WH_` | B | `schema/warehouse.ddl` contains 38 `CREATE TABLE` statements | Source inspection |
| F-003 | JMS route `warehouse.incoming` has a fork not visible in static call graph | A | JMX trace shows message delivery to `PutawayMDB` AND `AuditMDB` | Runtime observation; divergence recorded per DSC-3 |
| F-004 | JAAS realm `apex-ldap` authenticates against Oracle table `SYS_USERS` | B | `login-config.xml` references `apex-ldap`; `SysUserDAO` queries `SYS_USERS` | Source inspection |

> **Discovery completeness:** Discovery is goal-directed per DSC-4 — sufficiency for the Mission is the criterion, not full comprehension. Discovery evidence carries provenance and confidence per DSC-2 and EVC-1. [Ref: DSC-2; DSC-4; EVC-1]

---

## 4. Key Decisions (§35.2)

Decisions are recorded following the nine-field structure from §35.2. [Ref: §35.2 Decision Structure; DEC-1]

### Decision 1: Authentication Approach for Mobile API

| Field | Content |
|---|---|
| **Decision** | Introduce a JWT-based authentication gateway as a separate WAR module; proxy requests to existing EJB layer after translating JWT to JAAS principal. |
| **Decision Context** | Mobile clients cannot use the existing Swing JAAS login dialog. OAuth2 was considered but requires identity infrastructure the organization does not have. API must integrate with existing role-based authorization. |
| **Alternatives** | Alt-A: Extend JAAS with custom login module for HTTP Basic. Alt-B: Deploy OAuth2 authorization server. Alt-C: API-key-based authentication. |
| **Evidence** | F-004 (existing JAAS/Oracle auth). Impact analysis (§36): Alt-A couples API to legacy auth; Alt-B requires infrastructure project exceeding scope; Alt-C does not support role-based authorization. |
| **Impact** | + New module `api-gateway.war` with clear boundary. + Existing EJB authorization logic reused unchanged. ~ New JWT secret management (operational concern). − Additional network hop (latency risk, mitigated by colocation). |
| **Dependencies** | F-004; F-005 (EJB role annotations). Gateway module depends on `warehouse-ejb` module only. |
| **Approval** | Approved by Tech Lead + Architect on 2024-03-15. |
| **Status** | Approved |
| **Superseded By** | — |

### Decision 2: API Contract First vs. Code First

| Field | Content |
|---|---|
| **Decision** | OpenAPI contract first: specification authored before implementation, used to generate server stubs and client SDK. |
| **Decision Context** | Mobile team needs client SDK in parallel with backend development. Characterization tests for existing workflows require agreed contract to define "correct" behavior. |
| **Alternatives** | Alt-A: Code-first (generate OpenAPI from annotations). Alt-B: Contract-first (this decision). |
| **Evidence** | Mission deliverable D1 requires OpenAPI spec. Parallel team development requires contract stability. PR-6 (single source of truth) favors specification as authoritative. |
| **Impact** | + Parallel development enabled. + Contract is authoritative artifact per §11.3. ~ Requires discipline: implementation must not drift from spec (enforced by contract tests per §16.3). |
| **Dependencies** | Mission expected deliverable #1. |
| **Approval** | Approved by Architect on 2024-03-18. |
| **Status** | Approved |
| **Superseded By** | — |

> **Decision integrity note:** Both decisions are immutable per DEC-3. If either needs change, a new Decision would supersede it. Every implementation below traces to exactly one Decision per DEC-4. [Ref: DEC-3; DEC-4]

---

## 5. Stage Progression (§13.2)

Stage progression follows the mandatory schema from §13.2. [Ref: §13.2 Mandatory Stage Schema] For brevity, two representative stages are shown.

### Stage 1: API Contract Specification

| Field | Content |
|---|---|
| **Entry Criteria** | Discovery Complete for warehouse module (38 tables, 12 EJB interfaces identified). Decision 2 (Contract First) is Approved. |
| **Inputs** | Discovery facts F-001 through F-004; warehouse module dependency graph; Decision 2 record. |
| **Activities** | Map EJB methods to REST resources; define request/response schemas; specify error codes; write OpenAPI 3.0 YAML; conduct contract review with mobile team. |
| **Outputs** | `contracts/warehouse-api-v1.openapi.yaml` — Authoritative artifact per §11.3. Review record RV-API-001. |
| **Evidence Produced** | OpenAPI file passes Spectral linting. Review checklist completed (IEEE 1028-style inspection per §15.1). |
| **Exit Criteria** | OpenAPI spec reviewed and approved by mobile team + backend architect. All 12 endpoints have request/response schemas. Error responses defined for 4xx/5xx. |
| **Verification Criteria** | Linting passes (zero errors). Review record signed off. Mobile team confirms SDK generation succeeds. [Ref: PR-7] |
| **Review Type** | Inspection per §15.1 (gating a contract artifact). [Ref: RV-1] |

### Stage 2: API Implementation

| Field | Content |
|---|---|
| **Entry Criteria** | Stage 1 exit criteria verified. Decision 1 (JWT Gateway) is Approved. Repository Readiness gate "Implementation Ready" satisfied per §41.2. |
| **Inputs** | `contracts/warehouse-api-v1.openapi.yaml`; Decision 1; Decision 2; impact analysis record IMP-API-001. |
| **Activities** | Implement `api-gateway.war` with JWT validation; implement EJB facades adapting REST to existing warehouse session beans; write contract tests; write characterization tests for 3 warehouse workflows. |
| **Outputs** | `api-gateway.war` (Authoritative — hand-authored implementation). `warehouse-api-impl.jar` (Authoritative). Contract test suite (Authoritative). Characterization test report. |
| **Evidence Produced** | Contract tests: 12/12 pass. Characterization tests: 47/60 workflows covered (78% — below 80% target, recorded as risk RK-CHAR-001). Static analysis: 0 critical issues introduced. |
| **Exit Criteria** | All 12 contract tests pass. Zero critical static-analysis findings. p95 latency <200ms in load test. Swing client regression tests pass. |
| **Verification Criteria** | Contract test report (Test). Static analysis report (Analysis). Load test result (Demonstration). Regression test report (Test). [Ref: §16.2] |
| **Review Type** | Technical Review per §15.1. [Ref: §15.1] |

> **Stage rules observed:** SG-1 — exit criteria verified before stage declared complete. SG-2 — outputs classified per Artifact Authority Model (§11.1). SG-4 — validation responsibility (contract test authoring) kept distinct from implementation responsibility per PR-8. [Ref: SG-1; SG-2; SG-4]

---

## 6. Conformance Assertion (§16.5)

The conformance assertion is recorded following §16.5. [Ref: §16.5 Conformance / Certification Concept; FR-15; VL-1, VL-4]

| Field | Value |
|---|---|
| **Project** | ApexERP Mobile Warehouse API |
| **Standard Version** | SES v0.4.0 |
| **Assertion Date** | 2024-05-20 |
| **Asserted By** | Engineering Lead (with Independent Reviewer confirmation per RV-4) |
| **Conformance Scope** | Partial conformance — Warehouse module REST API layer only. Other ApexERP modules not assessed. |
| **Evidence Summary** | All required artifacts present: Mission (8 elements, §32.2), 2 Decisions (9 fields each, §35.2), Discovery record (§25.3 activities with confidence/provenance, §26.2), Stage records (§13.2 schema), Review records (§15.1 types), Validation records (§16.2 methods). |
| **Pass/Fail Verdict** | **PASS** — All applicable SES requirements for this Mission scope are satisfied. |
| **Cited Evidence** | Mission record: MS-001. Decisions: DEC-001, DEC-002. Discovery: DSC-RPT-001. Stages: STG-001, STG-002. Reviews: RV-API-001, RV-IMPL-001. Validation: VAL-RPT-001. |
| **Limitations** | Characterization test coverage at 78% (below 80% target); risk RK-CHAR-001 accepted by stakeholders. Conformance does not cover ERP modules outside warehouse. |

> **Verifiability note:** The assertion cites specific evidence records per VL-4 and names the standard version per VS-3. The verdict is objective pass/fail per VL-1. [Ref: VL-1; VL-4; VS-3]

---

## 7. SES Sections Cited in This Example

| SDD Section | How Demonstrated |
|---|---|
| §4.2 (ERP domain) | Example context: fictional ApexERP system |
| §11.1 (Artifact Authority Model) | Outputs classified as Authoritative/Generated |
| §11.2 (Artifact Metadata) | Metadata header on this example document |
| §11.3 (Contract Specification) | OpenAPI contract as authoritative artifact |
| §13.2 (Mandatory Stage Schema) | Two stages with all 8 fields populated |
| §15.1 (Review Types) | Inspection + Technical Review applied |
| §16.2 (Verification Methods) | Test, Analysis, Demonstration used |
| §16.5 (Conformance Assertion) | Recorded verdict with evidence |
| §25.3 (Discovery Activities) | All 6 activity layers demonstrated |
| §26.2 (Confidence Levels) | Facts graded A–E |
| §32.2 (Mission Structure) | Mission with all 8 elements |
| §34.2 (Operations) | Allowed Operations drawn from closed set |
| §35.2 (Decision Structure) | Two decisions with all 9 fields |
| §41.2 (Readiness Gates) | Implementation Ready gate referenced |

---

> **End of Example.** This document is NON-NORMATIVE and exists solely to demonstrate SES application. [Ref: §24 Phase 9; §10.3 Authority Rule]
