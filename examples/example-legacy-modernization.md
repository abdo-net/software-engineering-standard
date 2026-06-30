# Example: SES Applied to Legacy Modernization — Meridiem Banking Platform

> **NON-NORMATIVE** — This document is a worked example for illustrative purposes only.
> It demonstrates how the Software Engineering Standard (SES) MAY be applied to a project
> in the legacy modernization domain. [Ref: §4.2 Domains the SES Must Cover; §12.4 Rewrite vs Strangler Fig; §24 Phase 9 — Worked examples]
> This example introduces no new rules and extends no architecture.

---

## Artifact Metadata

| Field | Value |
|---|---|
| **Object ID** | EX-LGM-001 |
| **Object Type** | Example |
| **Authority Class** | Generated |
| **Owner** | SES Phase 9 — Example Writer |
| **Lifecycle State** | COMPLETED |
| **Status** | Accepted |
| **Version** | 0.1.0 |
| **Parent Objects** | SES v0.4.0 |
| **Repository Location** | `examples/example-legacy-modernization.md` |
| **Generated From** | SDD v0.4.0 §12.4, §32.2, §25.3, §35.2, §13.2, §16.5 |

---

## 1. Fictional Project Context

**Project name:** Meridiem Banking Platform (codename: "Meridiem")
**Domain:** Legacy modernization — retail banking core system
**Context:** A 25-year-old banking platform handling 1.8M accounts, written in COBOL with CICS on IBM z/OS, DB2 for z/OS database, and 3270 terminal emulation for branch staff. The system processes deposits, withdrawals, transfers, and loan applications. The organization wants to modernize the customer-facing account services (balance inquiry, transfer, transaction history) to a cloud-native architecture while keeping the COBOL core for back-office processing (loan workflows, regulatory reporting). The decision between rewrite and Strangler Fig (§12.4) is central to this engagement.

---

## 2. Mission Creation (§32.2)

The Mission is created following the eight-element structure mandated by §32.2. [Ref: §32.2 Mission Structure; MIS-1, MIS-2]

| Mission Element | Content |
|---|---|
| **Objective** | Modernize customer-facing account services (balance inquiry, transfer, transaction history) from 3270/CICS to a cloud-native REST API + web frontend, while preserving the COBOL core for back-office processing. All customer data must remain in DB2 for z/OS until a future Mission addresses data migration. |
| **Scope** | In scope: API design for 3 service domains (accounts, transfers, transactions); API implementation; web frontend; CICS integration layer (adapter from REST to CICS COMMAREA); characterization tests for existing COBOL business rules. Out of scope: Loan application module; regulatory reporting; back-office staff workflows; DB2 schema changes; data migration off z/OS. |
| **Constraints** | CN-REG: Must comply with banking regulations (PCI-DSS, SOX) — all changes auditable. CN-DATA: Customer account data MUST remain in DB2 for z/OS (no migration in this Mission). CN-AVAIL: 99.95% uptime during transition; maintenance windows max 4 hours monthly. CN-RISK: Zero financial transaction loss or duplication. |
| **Expected Deliverables** | (1) ADR for modernization approach (Strangler Fig vs. Rewrite); (2) ADR for CICS integration pattern; (3) REST API contract (OpenAPI); (4) CICS adapter service specification; (5) Characterization test suite for COBOL business rules; (6) Migration plan with rollback procedure; (7) Operational runbook. |
| **Success Criteria** | SC-API: All 18 endpoints respond per OpenAPI spec. SC-CICS: Adapter correctly maps REST to 14 CICS COMMAREA programs. SC-RULES: 100% of characterized COBOL business rules produce identical results via API. SC-REG: Security audit passes with zero critical findings. SC-AVAIL: Zero unplanned downtime during cutover. |
| **Allowed Operations** | DISCOVER, ANALYZE, TRACE, VERIFY, DOCUMENT, COMPARE, PLAN, IMPLEMENT, VALIDATE, REVIEW [Ref: §34.2 Operations and Governing Sections] |
| **Forbidden Operations** | Modification of COBOL source code; changes to DB2 schema; direct database writes from cloud side (read-only via adapter); deletion of existing 3270 transactions before new path verified. |
| **Evidence Requirements** | All facts carry confidence level per §26; all decisions recorded per §35; all approaches compared per FR-12/PR-12; business rule equivalence verified by characterization tests; conformance assertion recorded per §16.5. |

> **Mission validation note:** The Mission above defines all eight elements required by MIS-2. Expected deliverable #1 explicitly requires comparison of competing approaches per §12.4 and FR-12. [Ref: MIS-2; FR-12]

---

## 3. Discovery Activities (§25.3)

Discovery is performed following the mandated activity set from §25.3. [Ref: §25.3 Mandated Discovery Activities; DSC-1, DSC-2, DSC-3]

### 3.1 Discovery Results Summary

| Activity Layer | Activities Performed | Key Findings | Confidence |
|---|---|---|---|
| **Inventory Layer** | Asset Inventory; Repository Inventory; Technology Detection; Build System Detection; Runtime Environment Detection | 347 COBOL programs in CA-Endevor SCM. CICS TS 5.6, DB2 z/OS 13, IBM z/OS 2.5. Batch jobs via JCL. 3270 terminal definitions in CICS RDO. | B (source-confirmed) |
| **Structure Layer** | Dependency Discovery; Module Discovery; API Discovery; Database Discovery; Configuration Discovery | 14 CICS programs handle customer-facing services (prefix `AC*`). DB2: 23 tables; `ACCOUNTS`, `TRANSACTIONS`, `TRANSFERS` are in scope. CICS COMMAREA maps: 14 copybooks (`AC*.CPY`). No existing API layer. | B (source) |
| **Security Layer** | Security Discovery; Authentication Discovery; Authorization Discovery | CICS RACF security: transaction-level + resource-level. DB2 auth via CICS connection. No encryption on CICS-COBOL internal paths. TLS available on CICS Web Support (not currently used). | B/C (mixed) |
| **Behavior Layer** | Event Discovery; Workflow Discovery; Execution Flow Recovery; Runtime Observation | Transfer workflow: `AC01 (validate) → AC02 (debit) → AC03 (credit) → AC04 (log)`. SMF records show 450K transfers/day. CICS transaction rate: 1,200 TPS peak. | A (runtime-confirmed) |
| **Analysis Methods** | Static Analysis; Dynamic Analysis; Cross-Validation (triangulation) | Static: COBOL code inspection of 14 programs. Dynamic: CICS transaction monitoring (CEMT, CEDF). Triangulation: SMF transaction counts match dynamic trace; business rule output from static analysis matches runtime test cases. | D (triangulated) |
| **Synthesis** | Architecture Recovery; Knowledge Extraction; Evidence Collection; Documentation; Verification | Recovered: 3-tier CICS architecture (Presentation → BMS/COBOL → DB2). Business rules embedded in COBOL (no rule engine). Knowledge extracted to `docs/discovery/meridiem-knowledge.md`. | D |

### 3.2 Discovery Evidence Sample

| Fact ID | Statement | Confidence | Evidence Source | Verification Status |
|---|---|---|---|---|
| F-LGM-001 | 14 CICS programs handle customer-facing account services | B | Endevor listing shows 14 elements with prefix `AC*` in `CUSTSERV` system; CICS RDO has 14 transaction definitions | Source inspection |
| F-LGM-002 | Transfer workflow uses 4 CICS programs: AC01–AC04 | B | `ACTRANS.COBOL` contains `EXEC CICS LINK` to AC01–AC04 in sequence; CEDF trace confirms | Source + runtime triangulated |
| F-LGM-003 | CICS peak transaction rate is 1,200 TPS | A | SMF type 110 records show 1,200 max TPS over 30 days | Runtime observation |
| F-LGM-004 | DB2 `ACCOUNTS` table has 1.8M rows with 47 columns | B | `SELECT COUNT(*) FROM ACCOUNTS` returns 1,800,234; `DESCRIBE TABLE ACCOUNTS` shows 47 columns | Runtime + source |
| F-LGM-005 | No existing API or service layer; all access via CICS transactions | B | CICS RDO has no WEBService definitions; no URIMAP entries; no REST adapter configured | Source inspection |

> **Discovery completeness:** Discovery is goal-directed per DSC-4 — sufficiency for the Mission is the criterion, not full comprehension. Discovery evidence carries provenance and confidence per DSC-2 and EVC-1. [Ref: DSC-2; DSC-4; EVC-1]

---

## 4. Key Decisions (§35.2) — Including §12.4 Competing Approaches

Decisions are recorded following the nine-field structure from §35.2. [Ref: §35.2 Decision Structure; DEC-1] Decision 1 explicitly demonstrates the competing approaches comparison required by §12.4, FR-12, and PR-12.

### Decision 1: Modernization Approach — Strangler Fig vs. Rewrite

| Field | Content |
|---|---|
| **Decision** | Adopt incremental modernization via Strangler Fig pattern: intercept customer-facing requests at a facade layer, route incrementally to new services while delegating to CICS/COBOL for services not yet modernized. |
| **Decision Context** | §12.4 presents "Rewrite vs. incremental modernization (Strangler Fig)" as a documented tension. The Mission requires modernizing 3 service domains while preserving COBOL core. CN-AVAIL requires 99.95% uptime. CN-RISK requires zero transaction loss. |
| **Alternatives** | Alt-A: **Big-bang rewrite** — Build new system in parallel, cut over all 3 domains simultaneously. Alt-B: **Strangler Fig (incremental)** — Build facade, modernize domain by domain, COBOL remains during transition (selected). [Ref: §12.4] |
| **Evidence** | §12.4: "Incremental is the documented default at scale." [Ref: Fowler, "StranglerFigApplication"; Brodie & Stonebraker, *Migrating Legacy Systems*, 1995]. F-LGM-003 (1,200 TPS peak — high transaction volume favors incremental). F-LGM-005 (no existing API layer — greenfield facade needed regardless). Impact analysis (§36): Alt-A requires parallel run of full system for months, doubling infrastructure cost and operational complexity. Alt-B allows per-domain validation, smaller blast radius, gradual team skill transition. Risk analysis (§21): Alt-A has high risk of cutover failure; Alt-B spreads risk across 3 smaller cutovers. PR-12 (Context-sensitivity): high-availability, high-risk, regulated context favors incremental. |
| **Impact** | + Risk spread across 3 incremental cutovers. + Continuous value delivery (first domain live in 8 weeks vs. 14 months for full rewrite). + Team learns cloud patterns incrementally. ~ Requires facade layer (permanent architectural element). ~ COBOL/CICS remains longer (accepted constraint per CN-DATA). − Some duplicated effort during transition period. |
| **Dependencies** | F-LGM-003, F-LGM-005. §12.4 competing approaches framework. §36 Impact Analysis Model. §21 Risk model. |
| **Approval** | Approved by Enterprise Architect + Banking Compliance Officer on 2024-02-15. |
| **Status** | Approved |
| **Superseded By** | — |

### Decision 2: CICS Integration Pattern

| Field | Content |
|---|---|
| **Decision** | Use CICS Web Support with JSON adapter pattern: CICS receives HTTP requests, maps JSON to COMMAREA via a thin COBOL adapter program (new code), invokes existing business logic programs unchanged. |
| **Decision Context** | CN-DATA requires DB2 for z/OS to remain authoritative. New cloud services need to invoke existing COBOL business rules. Must not modify existing COBOL programs per Mission constraints. |
| **Alternatives** | Alt-A: Direct DB2 access from cloud (JDBC) — bypasses CICS, violates business rule encapsulation. Alt-B: CICS Transaction Gateway (CTG) from cloud — Java connector, adds latency. Alt-C: CICS Web Support with JSON adapter (selected) — native HTTP, minimal overhead. |
| **Evidence** | F-LGM-002 (transfer workflow is AC01→AC02→AC03→AC04). Business rules are in COBOL, not just DB2 constraints — bypassing CICS risks rule violation. F-LGM-005 (no existing web layer). CICS Web Support available (TLS capable). Benchmark: Alt-C adds 12ms latency vs. Alt-B's 45ms. |
| **Impact** | + Existing COBOL programs unchanged (CN-REG compliance preserved). + Low latency addition (12ms). + TLS encryption end-to-end. ~ Requires 14 thin adapter programs (auto-generated from copybooks). |
| **Dependencies** | Decision 1 (Strangler Fig — facade routes to CICS Web Support). F-LGM-002, F-LGM-005. |
| **Approval** | Approved by z/OS Platform Lead on 2024-02-20. |
| **Status** | Approved |
| **Superseded By** | — |

> **Decision integrity note:** Both decisions are immutable per DEC-3. Decision 1 explicitly references §12.4 competing approaches, FR-12, and PR-12 as required. The decision binds the choice to context (high-availability banking, regulated environment) rather than mandating one approach dogmatically. [Ref: DEC-3; §12.4; FR-12; PR-12]

---

## 5. Stage Progression (§13.2)

Stage progression follows the mandatory schema from §13.2. [Ref: §13.2 Mandatory Stage Schema] For brevity, two representative stages are shown.

### Stage 1: Facade + First Domain (Balance Inquiry)

| Field | Content |
|---|---|
| **Entry Criteria** | Discovery Complete for customer-facing CICS programs. Decision 1 (Strangler Fig) and Decision 2 (CICS Web Support) are Approved. Characterization tests for AC05 (balance inquiry COBOL program) pass. Repository Readiness gate "Implementation Ready" satisfied per §41.2. |
| **Inputs** | Decisions DEC-LGM-001, DEC-LGM-002; discovery facts F-LGM-001 through F-LGM-005; COBOL copybook for AC05 COMMAREA; CICS Web Support configuration guide. |
| **Activities** | Implement API facade with routing logic; implement AC05 JSON adapter in COBOL; deploy CICS Web Support with TLS; implement balance inquiry REST endpoint; write contract tests; write characterization tests comparing API output to 3270 transaction output; run security scan. |
| **Outputs** | `facade/` service (Authoritative). `adapters/AC05JSON.cbl` (Authoritative). `api/balance-v1.openapi.yaml` (Authoritative). Characterization test suite (Authoritative). Security scan report. |
| **Evidence Produced** | Contract tests: 6/6 pass. Characterization tests: 1,000 random accounts compared between API and 3270 path — 100% match. Security scan: zero critical findings. Load test: p99 latency 45ms (facade + CICS adapter + DB2). |
| **Exit Criteria** | All contract tests pass. Characterization tests 100% match. Security scan clean. Load test p99 <100ms. Code review completed. Compliance sign-off. |
| **Verification Criteria** | Contract test report (Test). Characterization comparison report (Analysis). Security scan (Analysis). Load test (Demonstration). [Ref: §16.2] |
| **Review Type** | Inspection per §15.1 (security-critical facade + compliance requirement). [Ref: RV-1] |

### Stage 2: Transfer Domain Migration

| Field | Content |
|---|---|
| **Entry Criteria** | Stage 1 exit criteria verified. Transfer domain characterization tests for AC01–AC04 pass. Impact analysis record IMP-LGM-002 reviewed. |
| **Inputs** | Stage 1 outputs; Decisions DEC-LGM-001, DEC-LGM-002; discovery facts F-LGM-002 (AC01–AC04 workflow); COBOL copybooks for AC01–AC04 COMMAREA areas. |
| **Activities** | Implement AC01–AC04 JSON adapters; implement transfer REST endpoints (initiate, confirm, status); integrate with facade routing; write contract tests; write characterization tests for transfer rules (overdraft limits, daily limits, currency validation); run regression test on balance inquiry (Stage 1); run penetration test. |
| **Outputs** | `adapters/AC01JSON.cbl` through `AC04JSON.cbl` (Authoritative). Updated `facade/` with transfer routes (Authoritative). `api/transfers-v1.openapi.yaml` (Authoritative). Penetration test report. |
| **Evidence Produced** | Contract tests: 18/18 pass. Characterization: 50 transfer scenarios — 100% match with COBOL output. Regression: Stage 1 balance inquiry tests still pass (no regression). Penetration test: 2 medium findings, remediated, re-tested. |
| **Exit Criteria** | All transfer contract tests pass. Characterization 100% match. Stage 1 regression tests pass. Penetration test clean. Financial audit confirms zero transaction loss during testing. |
| **Verification Criteria** | Contract test report (Test). Characterization report (Analysis). Regression test report (Test). Penetration test report (Analysis). Financial audit sign-off (Inspection). [Ref: §16.2] |
| **Review Type** | Inspection per §15.1 (financial transaction handling — highest risk). [Ref: RV-1] |

> **Stage rules observed:** SG-1 — exit criteria verified before stage declared complete. SG-2 — outputs classified per Artifact Authority Model (§11.1). SG-3 — Stage 2 re-uses Stage 1 infrastructure (iteration recorded). SG-4 — validation responsibility (characterization test authoring) kept distinct from implementation per PR-8. [Ref: SG-1; SG-2; SG-3; SG-4]

---

## 6. Conformance Assertion (§16.5)

The conformance assertion is recorded following §16.5. [Ref: §16.5 Conformance / Certification Concept; FR-15; VL-1, VL-4]

| Field | Value |
|---|---|
| **Project** | Meridiem Banking Platform — Customer Services Modernization |
| **Standard Version** | SES v0.4.0 |
| **Assertion Date** | 2024-08-30 |
| **Asserted By** | Enterprise Architect (with Independent Reviewer confirmation per RV-4) |
| **Conformance Scope** | Partial conformance — Balance inquiry and transfer domains (2 of 3 planned). Transaction history domain is in progress and not assessed. |
| **Evidence Summary** | All required artifacts present: Mission (8 elements, §32.2), 2 Decisions (9 fields each, §35.2) including §12.4 competing approaches comparison, Discovery record (§25.3 activities with confidence/provenance, §26.2), Stage records (§13.2 schema), Review records (§15.1 types), Validation records (§16.2 methods). Strangler Fig approach per §12.4 documented with context binding per PR-12. |
| **Pass/Fail Verdict** | **PASS** — All applicable SES requirements for this Mission scope are satisfied. |
| **Cited Evidence** | Mission record: MS-LGM-001. Decisions: DEC-LGM-001 (with §12.4 comparison), DEC-LGM-002. Discovery: DSC-RPT-LGM-001. Stages: STG-LGM-001, STG-LGM-002. Reviews: RV-FACADE-001, RV-TRANSFER-001. Validation: VAL-RPT-LGM-001. |
| **Limitations** | Only 2 of 3 domains modernized. Third domain (transaction history) pending. COBOL core remains in use — full retirement is a future Mission. Conformance does not cover loan module or regulatory reporting. Strangler Fig transition period creates temporary architectural complexity (accepted per Decision 1). |

> **Verifiability note:** The assertion cites specific evidence records per VL-4 and names the standard version per VS-3. The verdict is objective pass/fail per VL-1. [Ref: VL-1; VL-4; VS-3]

---

## 7. SES Sections Cited in This Example

| SDD Section | How Demonstrated |
|---|---|
| §4.2 (legacy modernization domain) | Example context: fictional Meridiem banking platform |
| §11.1 (Artifact Authority Model) | Outputs classified as Authoritative/Generated |
| §11.2 (Artifact Metadata) | Metadata header on this example document |
| §11.3 (Contract Specification) | OpenAPI contracts as authoritative artifacts |
| §12.4 (Rewrite vs Strangler Fig) | Decision 1 compares approaches per FR-12/PR-12 |
| §13.2 (Mandatory Stage Schema) | Two stages with all 8 fields populated |
| §15.1 (Review Types) | Inspection applied |
| §16.2 (Verification Methods) | Test, Analysis, Demonstration used |
| §16.5 (Conformance Assertion) | Recorded verdict with evidence |
| §21 (Risk model) | Risk analysis referenced in Decision 1 |
| §25.3 (Discovery Activities) | All 6 activity layers demonstrated |
| §26.2 (Confidence Levels) | Facts graded A–E |
| §32.2 (Mission Structure) | Mission with all 8 elements |
| §34.2 (Operations) | Allowed Operations drawn from closed set |
| §35.2 (Decision Structure) | Two decisions with all 9 fields |
| §36 (Impact Analysis) | Impact analysis referenced in Decision 1 |
| §41.2 (Readiness Gates) | Implementation Ready gate referenced |

---

> **End of Example.** This document is NON-NORMATIVE and exists solely to demonstrate SES application. [Ref: §24 Phase 9; §10.3 Authority Rule]
