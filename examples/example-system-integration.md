# Example: SES Applied to System Integration — Nexus Supply Chain Hub

> **NON-NORMATIVE** — This document is a worked example for illustrative purposes only.
> It demonstrates how the Software Engineering Standard (SES) MAY be applied to a project
> in the system integration domain. [Ref: §4.2 Domains the SES Must Cover; §24 Phase 9 — Worked examples]
> This example introduces no new rules and extends no architecture.

---

## Artifact Metadata

| Field | Value |
|---|---|
| **Object ID** | EX-SI-001 |
| **Object Type** | Example |
| **Authority Class** | Generated |
| **Owner** | SES Phase 9 — Example Writer |
| **Lifecycle State** | COMPLETED |
| **Status** | Accepted |
| **Version** | 0.1.0 |
| **Parent Objects** | SES v0.4.0 |
| **Repository Location** | `examples/example-system-integration.md` |
| **Generated From** | SDD v0.4.0 §32.2, §25.3, §35.2, §13.2, §16.5 |

---

## 1. Fictional Project Context

**Project name:** Nexus Supply Chain Hub (codename: "NexusHub")
**Domain:** System integration — connecting warehouse management, shipping carriers, and ERP systems
**Context:** A logistics company operates 12 warehouses using Warehouse Management System "WareX", ships via 3 carriers (FedEx API, UPS API, DHL API), and runs financials in SAP S/4HANA. Currently, warehouse staff manually copy shipping labels and tracking numbers between systems. The organization needs to build an integration hub that automates: (1) order flow from SAP to WareX, (2) shipping label generation from WareX to carrier APIs, (3) tracking number update from carriers back to SAP, (4) inventory sync from WareX to SAP.

---

## 2. Mission Creation (§32.2)

The Mission is created following the eight-element structure mandated by §32.2. [Ref: §32.2 Mission Structure; MIS-1, MIS-2]

| Mission Element | Content |
|---|---|
| **Objective** | Build NexusHub integration middleware connecting SAP S/4HANA (financials/orders), WareX (warehouse management), and 3 carrier APIs (FedEx, UPS, DHL) to automate order flow, shipping label generation, tracking synchronization, and inventory updates across 12 warehouse locations. |
| **Scope** | In scope: Integration hub design and implementation; API adapters for SAP ODATA, WareX REST, FedEx/UPS/DHL APIs; message routing and transformation; error handling and dead-letter queue; operational monitoring dashboard; integration test suite. Out of scope: Changes to SAP S/4HANA core; changes to WareX; carrier API migrations; data warehouse/analytics. |
| **Constraints** | CN-SAP: SAP changes limited to standard ODATA API — no custom ABAP. CN-WAREX: WareX changes limited to webhook configuration — no code changes. CN-THROUGHPUT: Must handle 50K shipments/day across 12 warehouses (peak: 5K/hour). CN-ORDER: Order state must be eventually consistent within 5 minutes end-to-end. CN-RETRY: Failed operations must retry automatically with exponential backoff; manual intervention only after 5 attempts. |
| **Expected Deliverables** | (1) ADR for integration pattern selection; (2) ADR for error handling strategy; (3) API contract specifications for all 5 system adapters; (4) Integration hub implementation; (5) End-to-end integration test suite; (6) Operational monitoring configuration; (7) Runbook for incident response. |
| **Success Criteria** | SC-E2E: 99.9% of orders flow from SAP → WareX → carrier → tracking update within 5 minutes. SC-ERROR: <0.1% of shipments require manual intervention. SC-RETRY: 100% of transient failures resolve within 5 retry attempts. SC-MONITOR: All integration points have health checks with <30s detection time. |
| **Allowed Operations** | DISCOVER, ANALYZE, TRACE, VERIFY, DOCUMENT, COMPARE, PLAN, IMPLEMENT, VALIDATE, REVIEW [Ref: §34.2 Operations and Governing Sections] |
| **Forbidden Operations** | Direct database access to SAP or WareX (must use published APIs); modification of carrier SDKs; bypassing retry logic for immediate retry; deployment without integration test pass. |
| **Evidence Requirements** | All facts carry confidence level per §26; all decisions recorded per §35; all API contracts specified per §11.3; integration validated by end-to-end tests; conformance assertion recorded per §16.5. |

> **Mission validation note:** The Mission above defines all eight elements required by MIS-2. Integration-specific validation concerns (eventual consistency, retry behavior, health monitoring) are in scope per the Mission definition. [Ref: MIS-2]

---

## 3. Discovery Activities (§25.3) — Integration-Specific

Discovery is performed following the mandated activity set from §25.3. [Ref: §25.3 Mandated Discovery Activities; DSC-1, DSC-2, DSC-3] Discovery for system integration emphasizes API discovery and cross-system contract validation.

### 3.1 Discovery Results Summary

| Activity Layer | Activities Performed | Key Findings | Confidence |
|---|---|---|---|
| **Inventory Layer** | Asset Inventory; Repository Inventory; Technology Detection; Build System Detection; Runtime Environment Detection | No existing integration code. SAP S/4HANA 2022 (ODATA v4). WareX v4.2 (REST + webhooks). Carrier APIs: FedEx REST (2023), UPS JSON (2022), DHL XML (SOAP). Target runtime: Kubernetes (EKS). | B/C (vendor docs + source) |
| **Structure Layer** | Dependency Discovery; Module Discovery; API Discovery; Database Discovery; Configuration Discovery | SAP: 12 ODATA entities relevant; `SalesOrder`, `Delivery`, `Inventory` are in scope. WareX: 8 REST endpoints; `/orders`, `/shipments`, `/inventory`, `/webhooks`. FedEx: 6 REST endpoints. UPS: 5 JSON endpoints. DHL: 4 SOAP operations. All 5 systems have separate authentication mechanisms. | B (vendor API docs) |
| **Security Layer** | Security Discovery; Authentication Discovery; Authorization Discovery | SAP: OAuth2 + SAML (SSO). WareX: API key + HMAC. FedEx: OAuth2. UPS: OAuth2. DHL: Basic Auth + WS-Security. All use TLS 1.2+. Token expiry varies: SAP 3600s, FedEx 3600s, UPS 14400s, DHL no expiry. | B (vendor docs) |
| **Behavior Layer** | Event Discovery; Workflow Discovery; Execution Flow Recovery; Runtime Observation | Current manual workflow: `SAP order → warehouse staff prints pick list → picks items → logs into carrier website → prints label → copies tracking to SAP → updates inventory in SAP`. End-to-end time: 12–45 minutes manual. | A (observed workflow) |
| **Analysis Methods** | Static Analysis; Dynamic Analysis; Cross-Validation (triangulation) | Static: API schema analysis (OpenAPI/SWSDL/WADL). Dynamic: Test calls to each API endpoint using sandbox credentials. Triangulation: SAP ODATA metadata document matches test call responses for `SalesOrder` entity. One divergence: WareX webhook payload schema (docs) differs from actual webhook body (runtime) — finding F-SI-006. | D (triangulated) |
| **Synthesis** | Architecture Recovery; Knowledge Extraction; Evidence Collection; Documentation; Verification | Recovered: 5 integration points with heterogeneous protocols (ODATA, REST, SOAP). 4 authentication mechanisms. 3 data format standards (JSON, XML, ODATA). Knowledge extracted to `docs/discovery/nexushub-knowledge.md`. | D |

### 3.2 Discovery Evidence Sample — Integration-Specific

| Fact ID | Statement | Confidence | Evidence Source | Verification Status |
|---|---|---|---|---|
| F-SI-001 | SAP ODATA `SalesOrder` entity has 47 fields; 8 are required for integration | B | `/$metadata` document shows `SalesOrder` EntityType with 47 Property elements; test `GET /SalesOrder('100001')` returns all 47 | Source + runtime triangulated |
| F-SI-002 | WareX REST `/orders` endpoint accepts POST with JSON body for order creation | A | `POST /orders` in sandbox returns 201 with order ID; OpenAPI spec from vendor confirms schema | Runtime + doc triangulated |
| F-SI-003 | FedEx API rate limit: 10 requests/second per API key | B | FedEx developer docs state 10 req/s; load test at 15 req/s receives HTTP 429 | Runtime-confirmed |
| F-SI-004 | UPS OAuth token expires in 14,400 seconds (4 hours) | A | `POST /security/v1/oauth/token` response contains `"expires_in":14400`; observed token fails after 4 hours | Runtime observation |
| F-SI-005 | DHL SOAP API uses `wsse:UsernameToken` with plaintext password (no nonce) | B | WSDL shows `Security` header with `UsernameToken`; test call succeeds with provided credentials | Source + runtime |
| F-SI-006 | WareX webhook `shipment.created` payload has additional `warehouse_zone` field not in documentation | A | Actual webhook delivery contains `{..., "warehouse_zone": "A12"}`; docs do not list this field | Runtime observation; divergence recorded per DSC-3 |

> **Discovery completeness:** Discovery is goal-directed per DSC-4 — sufficiency for the Mission is the criterion, not full comprehension. Integration-specific discovery emphasizes API contracts, authentication mechanisms, and rate limits. Cross-validation (triangulation) is critical: finding F-SI-006 ( WareX webhook divergence) was caught by comparing documentation (static) against actual webhook delivery (dynamic) per DSC-3. [Ref: DSC-2; DSC-3; DSC-4; EVC-1]

---

## 4. Key Decisions (§35.2)

Decisions are recorded following the nine-field structure from §35.2. [Ref: §35.2 Decision Structure; DEC-1]

### Decision 1: Integration Pattern — Hub-and-Spoke vs. Point-to-Point

| Field | Content |
|---|---|
| **Decision** | Hub-and-spoke architecture: NexusHub acts as central integration middleware with adapters for each of the 5 external systems. All routing and transformation logic lives in the hub. |
| **Decision Context** | 5 systems to integrate (SAP, WareX, FedEx, UPS, DHL). Point-to-point would require 10 connections (n(n-1)/2). Adding a 6th system later is likely. Need centralized monitoring, retry logic, and error handling. |
| **Alternatives** | Alt-A: Point-to-point (each system connects directly to others). Alt-B: Hub-and-spoke (selected). Alt-C: Enterprise Service Bus (full-featured ESB product). |
| **Evidence** | Impact analysis (§36): Alt-A creates 10 integration points to maintain, no centralized retry/monitoring. Alt-B creates 5 adapters, centralized logic, easier testing. Alt-C adds vendor dependency (violates CN-1/PR-3) and operational complexity exceeding Mission scope. |
| **Impact** | + 5 adapters vs. 10 point-to-point connections. + Centralized retry, monitoring, error handling. + Adding 6th system requires only 1 new adapter. ~ Hub is a SPOF (mitigated by Kubernetes HA deployment). |
| **Dependencies** | F-SI-001 through F-SI-005 (API discovery). CN-THROUGHPUT (50K/day). CN-RETRY (exponential backoff requirement). |
| **Approval** | Approved by Integration Architect on 2024-05-10. |
| **Status** | Approved |
| **Superseded By** | — |

### Decision 2: Error Handling and Dead-Letter Strategy

| Field | Content |
|---|---|
| **Decision** | Circuit breaker + dead-letter queue pattern: transient failures (HTTP 5xx, timeout) retry with exponential backoff; permanent failures (HTTP 4xx except 429, schema validation failure) go to dead-letter queue for manual review; circuit breaker opens after 50% error rate over 60 seconds. |
| **Decision Context** | Mission requires <0.1% manual intervention (SC-ERROR) and automatic retry up to 5 attempts (CN-RETRY). 5 external systems with varying reliability. Need to distinguish transient from permanent failures. |
| **Alternatives** | Alt-A: Retry all failures (including 4xx) — wastes resources on unrecoverable errors. Alt-B: No retry, all to dead-letter — violates CN-RETRY. Alt-C: Circuit breaker + DLQ with smart classification (selected). |
| **Evidence** | F-SI-003 (FedEx rate limit 10 req/s — 429 is transient, should retry). F-SI-006 (schema divergence — permanent, needs human decision). SAP ODATA 401 with expired token — transient (refresh + retry). WareX 400 with invalid order ID — permanent (data issue). |
| **Impact** | + Distinguishes transient from permanent correctly. + Circuit breaker prevents cascade failures. + DLQ provides audit trail for compliance. ~ Requires classification table maintained per carrier/API behavior. |
| **Dependencies** | F-SI-003, F-SI-006. Decision 1 (hub-and-spoke — error handling is centralized). CN-RETRY, SC-ERROR. |
| **Approval** | Approved by Integration Architect + SRE Lead on 2024-05-12. |
| **Status** | Approved |
| **Superseded By** | — |

> **Decision integrity note:** Both decisions are immutable per DEC-3. If either needs change, a new Decision would supersede it. Every implementation below traces to exactly one Decision per DEC-4. [Ref: DEC-3; DEC-4]

---

## 5. Stage Progression (§13.2)

Stage progression follows the mandatory schema from §13.2. [Ref: §13.2 Mandatory Stage Schema] For brevity, two representative stages are shown.

### Stage 1: Adapter Development and Validation

| Field | Content |
|---|---|
| **Entry Criteria** | Discovery Complete for all 5 external systems. Decision 1 (hub-and-spoke) and Decision 2 (error handling) are Approved. Sandbox credentials obtained for all systems. Repository Readiness gate "Implementation Ready" satisfied per §41.2. |
| **Inputs** | Decisions DEC-SI-001, DEC-SI-002; discovery facts F-SI-001 through F-SI-006; vendor API documentation; sandbox credentials. |
| **Activities** | Implement 5 adapters (SAP-ODATA, WareX-REST, FedEx-REST, UPS-JSON, DHL-SOAP); implement authentication refresh for each token type; implement request/response transformation; write unit tests for each adapter; run integration tests against sandboxes; validate rate limit handling; validate schema handling for F-SI-006 divergence. |
| **Outputs** | `adapters/` — 5 adapter modules (Authoritative). Auth refresh service (Authoritative). Adapter unit test suite (Authoritative). Integration test report. |
| **Evidence Produced** | Unit tests: 89/89 pass. Integration tests: 25/25 pass against sandboxes. Rate limit test: FedEx adapter throttles correctly at 10 req/s. Schema test: F-SI-006 `warehouse_zone` field handled gracefully (logged, passed through). |
| **Exit Criteria** | All unit + integration tests pass. Each adapter connects successfully to sandbox. Authentication refresh works for all 4 token types. Rate limiting handled. Divergence F-SI-006 documented and handled. |
| **Verification Criteria** | Unit test report (Test). Integration test report (Test). Rate limit benchmark (Demonstration). Schema handling test (Test). [Ref: §16.2] |
| **Review Type** | Technical Review per §15.1. [Ref: §15.1] |

### Stage 2: End-to-End Integration and Monitoring

| Field | Content |
|---|---|
| **Entry Criteria** | Stage 1 exit criteria verified. All 5 adapters pass individual tests. Decision 2 (error handling) is Approved. Message queue infrastructure (RabbitMQ) deployed. |
| **Inputs** | Stage 1 outputs; Decisions DEC-SI-001, DEC-SI-002; message queue infrastructure; monitoring stack (Prometheus + Grafana). |
| **Activities** | Implement message routing logic (SAP order → WareX order → carrier label → tracking update → SAP delivery); implement circuit breaker and DLQ; implement health checks for all 5 adapters; deploy monitoring dashboards; run end-to-end integration test across all 4 workflows; run chaos test (carrier API downtime simulation); run load test at 5K shipments/hour peak. |
| **Outputs** | `hub/` — routing + transformation logic (Authoritative). `resilience/` — circuit breaker + DLQ (Authoritative). Monitoring dashboards (Generated from config). E2E test suite (Authoritative). Chaos test report. Load test report. |
| **Evidence Produced** | E2E tests: 4 workflows × 50 scenarios = 200 tests, all pass. Chaos test: circuit breaker opens in 3 seconds on simulated FedEx outage; DLQ receives 12 messages during 5-minute outage; all processed after recovery. Load test: 5,200 shipments/hour sustained for 2 hours; p95 E2E latency 3.2 minutes (under 5-minute budget). Health check detection: 18 seconds average. |
| **Exit Criteria** | All E2E tests pass. Circuit breaker functions correctly. DLQ processes messages after recovery. Load test at 5K/hour passes. Health check detection <30s. Zero unhandled schema errors. |
| **Verification Criteria** | E2E test report (Test). Chaos test log (Demonstration). Load test report (Test). Health check timing (Analysis). [Ref: §16.2] |
| **Review Type** | Inspection per §15.1 (for financial transaction routing — risk-critical). [Ref: RV-1] |

> **Stage rules observed:** SG-1 — exit criteria verified before stage declared complete. SG-2 — outputs classified per Artifact Authority Model (§11.1). SG-4 — validation responsibility (E2E test authoring + chaos test) kept distinct from implementation per PR-8. [Ref: SG-1; SG-2; SG-4]

---

## 6. Conformance Assertion (§16.5)

The conformance assertion is recorded following §16.5. [Ref: §16.5 Conformance / Certification Concept; FR-15; VL-1, VL-4]

| Field | Value |
|---|---|
| **Project** | NexusHub Supply Chain Integration |
| **Standard Version** | SES v0.4.0 |
| **Assertion Date** | 2024-10-20 |
| **Asserted By** | Integration Architect (with Independent Reviewer confirmation per RV-4) |
| **Conformance Scope** | Partial conformance — Integration hub for 4 workflows (order flow, label generation, tracking sync, inventory update) across 5 systems. Does not cover future system additions or data warehouse integration. |
| **Evidence Summary** | All required artifacts present: Mission (8 elements, §32.2), 2 Decisions (9 fields each, §35.2), Discovery record (§25.3 activities with confidence/provenance, §26.2), Stage records (§13.2 schema), Review records (§15.1 types), Validation records (§16.2 methods). Integration-specific concerns (API contract validation, cross-system consistency, health monitoring) addressed. |
| **Pass/Fail Verdict** | **PASS** — All applicable SES requirements for this Mission scope are satisfied. |
| **Cited Evidence** | Mission record: MS-SI-001. Decisions: DEC-SI-001, DEC-SI-002. Discovery: DSC-RPT-SI-001. Stages: STG-SI-001, STG-SI-002. Reviews: RV-ADAPTER-001, RV-E2E-001. Validation: VAL-RPT-SI-001. |
| **Limitations** | Sandbox testing only — production validation is a separate post-deployment Mission. Divergence F-SI-006 (WareX webhook schema) is handled but may require adapter update if WareX changes the field. Rate limits are per current carrier API versions — changes require adapter updates. Conformance does not cover disaster recovery or multi-region deployment. |

> **Verifiability note:** The assertion cites specific evidence records per VL-4 and names the standard version per VS-3. The verdict is objective pass/fail per VL-1. [Ref: VL-1; VL-4; VS-3]

---

## 7. SES Sections Cited in This Example

| SDD Section | How Demonstrated |
|---|---|
| §4.2 (system integration domain) | Example context: fictional NexusHub supply chain integration |
| §11.1 (Artifact Authority Model) | Outputs classified as Authoritative/Generated |
| §11.2 (Artifact Metadata) | Metadata header on this example document |
| §11.3 (Contract Specification) | API contracts for all 5 system adapters |
| §13.2 (Mandatory Stage Schema) | Two stages with all 8 fields populated |
| §15.1 (Review Types) | Technical Review + Inspection applied |
| §16.2 (Verification Methods) | Test, Analysis, Demonstration used |
| §16.5 (Conformance Assertion) | Recorded verdict with evidence |
| §25.3 (Discovery Activities) | All 6 activity layers demonstrated |
| §26.2 (Confidence Levels) | Facts graded A–E |
| §32.2 (Mission Structure) | Mission with all 8 elements |
| §34.2 (Operations) | Allowed Operations drawn from closed set |
| §35.2 (Decision Structure) | Two decisions with all 9 fields |
| §36 (Impact Analysis) | Impact analysis referenced in Decision 1 |
| §41.2 (Readiness Gates) | Implementation Ready gate referenced |

---

> **End of Example.** This document is NON-NORMATIVE and exists solely to demonstrate SES application. [Ref: §24 Phase 9; §10.3 Authority Rule]
