# Completion Criteria

> **Authority Class:** Authoritative
> **SDD Authority:** §27.2, §27.3, §16, §26, §28, §40
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 5

## 1. Purpose

This document specifies the objective exit criteria for all thirteen completion states defined in the Engineering Completion Criteria model (§27). Each completion state defines a named point at which a body of engineering work is objectively complete. [Ref: §27.1; §27.2]

The completion criteria prevent subjective "done" by requiring verifiable, evidenced exit conditions for each state. [Ref: §27.3 CMP-1]

## 2. Scope

This document defines exit criteria for all thirteen completion states mandated by §27.2. Each state specifies objective, verifiable exit criteria per CMP-1. Where the SDD does not specify detail for a criterion, this document states so explicitly.

This document does NOT define: the verification procedures for each criterion (Phase 6); the metric thresholds for completeness dimensions (§50 CPL-5); stage-level exit criteria (§13; defined in `stage-catalog.md`).

## 3. Normative Rules (CMP-1..CMP-5)

The following rules govern all completion states. Violation of any rule renders a completion assertion non-conformant. [Ref: §27.3]

| ID | Rule | Evidence |
|---|---|---|
| **CMP-1** | Each completion state **MUST** define **objective, verifiable** exit criteria; subjective "done" is prohibited. Every criterion SHALL be answerable with "yes/no" or a measurable quantity. | [Ref: PR-7; IEEE 1028-2008] |
| **CMP-2** | A completion state is reached only when its exit criteria are verified by a method in §16.2 (Inspection, Analysis, Demonstration, or Test). | [Ref: §16; ISO/IEC/IEEE 29148] |
| **CMP-3** | "Engineering Complete" **MUST NOT** be asserted unless all subordinate completion states are complete and evidenced. | [Ref: PR-8; stage-gate practice] |
| **CMP-4** | Completion **MUST** be evidenced and recorded (provenance). A completion assertion without recorded evidence is non-conformant. | [Ref: PR-5] |
| **CMP-5** | Detailed per-state criteria are the Phase 5/6 deliverable; §27 defines the model only. This document populates that model. | [Ref: Development Order] |

## 4. Completion States

### 4.1 Discovery Complete

**Definition:** The unknown system has been transformed into an understood system through the discovery process. All mandated discovery activities have been performed and their outputs are recorded. [Ref: §27.2; §25]

**Objective Exit Criteria:**

| # | Criterion | Verification Method | SDD Authority |
|---|---|---|---|
| DC-1 | All mandated discovery activities (§25.3) are performed: Asset Inventory, Repository Inventory, Technology Detection, Build System Detection, Runtime Environment Detection, Dependency Discovery, Module Discovery, API Discovery, Database Discovery, Configuration Discovery, Security Discovery, Authentication Discovery, Authorization Discovery, Event Discovery, Workflow Discovery, Execution Flow Recovery, Runtime Observation, Static Analysis, Dynamic Analysis, Cross Validation, Architecture Recovery, Knowledge Extraction, Evidence Collection, Documentation, Verification. | Inspection | §25.3 |
| DC-2 | Discovery outputs are recorded with provenance (§28). | Inspection | §25 DSC-2; §28 ECH-2 |
| DC-3 | All discovery outputs carry confidence levels (A--E) per §26. | Inspection | §26 EVC-1 |
| DC-4 | Cross-validation is performed; disagreements are recorded, not silently resolved (§25 DSC-3). | Inspection | §25 DSC-3 |
| DC-5 | Discovery is goal-directed and iterative; sufficiency for the Mission is demonstrated (§25 DSC-4). | Analysis | §25 DSC-4; §32 |
| DC-6 | No discovery conclusion asserts confidence exceeding its evidence (§25 DSC-6). | Analysis | §25 DSC-6; §26 |
| DC-7 | The Evidence Chain (§28) is unbroken from observations through to knowledge. | Inspection | §28 ECH-1, ECH-2 |
| DC-8 | All INT rules (§40) applicable to discovered elements are satisfied (e.g., no undocumented dependency, API, database, configuration, workflow, security rule). | Inspection | §40 INT-3, INT-4, INT-5, INT-6, INT-7, INT-8 |

---

### 4.2 Knowledge Complete

**Definition:** Engineering knowledge has been synthesized from verified facts and is recorded in the repository as authoritative knowledge. [Ref: §27.2; §14; §31]

**Objective Exit Criteria:**

| # | Criterion | Verification Method | SDD Authority |
|---|---|---|---|
| KC-1 | All facts carry provenance (§14.3 KN-1). | Inspection | §14.3 KN-1 |
| KC-2 | All facts carry confidence levels (A--E) per §26. | Inspection | §26 EVC-1 |
| KC-3 | Knowledge progression follows Observed -> Verified -> Engineering Knowledge via the Evidence Chain (§31 RKA-2). | Inspection | §31 RKA-2; §28 |
| KC-4 | Hypotheses (Level-E facts) are marked as hypotheses and not treated as authoritative (§14.3 KN-3; §26 EVC-3). | Inspection | §14.3 KN-3; §26 EVC-3 |
| KC-5 | Knowledge resides in the repository; no essential knowledge lives only in conversation or tooling (§14.3 KN-5). | Inspection | §14.3 KN-5; PR-4 |
| KC-6 | Triangulation is performed where feasible; multi-source corroboration is documented (§14.3 KN-6). | Analysis | §14.3 KN-6 |
| KC-7 | Knowledge classes (§31.2) are correctly assigned: Observed Facts, Verified Facts, Engineering Knowledge, Design Decisions, Architecture Decisions, Operational Knowledge, Historical Knowledge, Deprecated Knowledge, Generated Knowledge, Derived Knowledge, Authoritative Knowledge. | Inspection | §31.2 |
| KC-8 | Superseded knowledge is retained as Historical; deprecated knowledge is marked, not deleted (§31 RKA-3). | Inspection | §31 RKA-3 |

---

### 4.3 Dependency Complete

**Definition:** All dependencies of the subject system are discovered, documented, and validated. No undocumented dependencies remain. [Ref: §27.2; §25; §40]

**Objective Exit Criteria:**

| # | Criterion | Verification Method | SDD Authority |
|---|---|---|---|
| DPC-1 | All internal dependencies are discovered and documented. | Inspection | §25.3 (Dependency Discovery, Module Discovery) |
| DPC-2 | All external dependencies are discovered and documented. | Inspection | §25.3 (Dependency Discovery) |
| DPC-3 | The dependency graph is declared and acyclic (§49 CON-6). | Analysis | §45 DEP-2; §49 CON-6 |
| DPC-4 | Every dependency is traceable in the traceability graph (§48). | Inspection | §48 TGR-1; §29 TRC-1 |
| DPC-5 | No undocumented dependency exists (§40 INT-3). | Inspection | §40 INT-3 |
| DPC-6 | Dependency changes are impact-analyzed (§36 IMP-1). | Inspection | §36 IMP-1 |
| DPC-7 | Dependency discovery results carry confidence levels (§26). | Inspection | §26 EVC-1 |

---

### 4.4 Architecture Complete

**Definition:** The architecture of the subject system is recovered, documented, and validated. All architectural decisions are recorded. [Ref: §27.2; §30; §35]

**Objective Exit Criteria:**

| # | Criterion | Verification Method | SDD Authority |
|---|---|---|---|
| AC-1 | Architecture recovery is performed; higher-level abstractions are produced from lower-level artifacts (§30 REV-2). | Inspection | §30 REV-2 |
| AC-2 | All architecture decisions are recorded as ADRs with all nine fields (§35.2; §11.3). | Inspection | §35 DEC-1; §11.3 |
| AC-3 | Architecture decisions are immutable once accepted; superseded decisions retain historical status (§35 DEC-3). | Inspection | §35 DEC-3; §31 RKA-3 |
| AC-4 | Architecture documentation is categorized per §38.2 and declares its authority class (§38 DOC-2). | Inspection | §38 DOC-2 |
| AC-5 | The architecture is traceable in the traceability graph (§48). | Inspection | §48 TGR-1 |
| AC-6 | Architecture recovery outputs carry confidence levels (§26). | Inspection | §26 EVC-1 |
| AC-7 | No INT violation exists for architecture elements (§40). | Inspection | §40 |

---

### 4.5 Execution Flow Complete

**Definition:** All execution flows of the subject system are recovered, documented, and validated. [Ref: §27.2; §25; §29]

**Objective Exit Criteria:**

| # | Criterion | Verification Method | SDD Authority |
|---|---|---|---|
| EFC-1 | Execution Flow Recovery activity is performed (§25.3). | Inspection | §25.3 |
| EFC-2 | All entry points are identified and documented. | Inspection | §25 (Behavior Layer) |
| EFC-3 | All call chains are identified and documented. | Inspection | §25 (Behavior Layer) |
| EFC-4 | Control flow is recovered and documented. | Inspection | §25 (Behavior Layer) |
| EFC-5 | Execution flow documentation carries confidence levels (§26). | Inspection | §26 EVC-1 |
| EFC-6 | Execution flows are traceable in the traceability graph (§48). | Inspection | §48 TGR-1 |
| EFC-7 | Runtime observation corroborates static analysis where feasible; disagreements are recorded (§26 EVC-6). | Analysis | §26 EVC-6 |

---

### 4.6 API Complete

**Definition:** All APIs of the subject system are discovered, documented with contracts, and validated. No undocumented API remains. [Ref: §27.2; §25; §40 INT-4]

**Objective Exit Criteria:**

| # | Criterion | Verification Method | SDD Authority |
|---|---|---|---|
| APC-1 | All API endpoints/interfaces are discovered (§25.3 API Discovery). | Inspection | §25.3 |
| APC-2 | Every API has a contract specification (§11.3 Contract Specification). | Inspection | §11.3; §40 INT-4 |
| APC-3 | API contracts declare interface plus semantics across boundaries. | Inspection | §11.3 |
| APC-4 | API documentation is categorized per §38.2 and declares its authority class (§38 DOC-2). | Inspection | §38 DOC-2 |
| APC-5 | APIs are traceable in the traceability graph (§48). | Inspection | §48 TGR-1 |
| APC-6 | API discovery results carry confidence levels (§26). | Inspection | §26 EVC-1 |
| APC-7 | No undocumented API exists (§40 INT-4). | Inspection | §40 INT-4 |

---

### 4.7 Database Complete

**Definition:** All database objects of the subject system are discovered and documented. No undocumented database object remains. [Ref: §27.2; §25; §40 INT-5]

**Objective Exit Criteria:**

| # | Criterion | Verification Method | SDD Authority |
|---|---|---|---|
| DBC-1 | All database systems are discovered (§25.3 Database Discovery). | Inspection | §25.3 |
| DBC-2 | All database schemas are discovered and documented. | Inspection | §25.3 |
| DBC-3 | All database migrations are identified and documented. | Inspection | §25.3 |
| DBC-4 | All data flows are identified and documented. | Inspection | §25.3 |
| DBC-5 | Database documentation is categorized per §38.2 and declares its authority class (§38 DOC-2). | Inspection | §38 DOC-2 |
| DBC-6 | Database objects are traceable in the traceability graph (§48). | Inspection | §48 TGR-1 |
| DBC-7 | No undocumented database object exists (§40 INT-5). | Inspection | §40 INT-5 |

---

### 4.8 Security Complete

**Definition:** All security mechanisms of the subject system are discovered and documented. No undocumented security rule remains. [Ref: §27.2; §25; §40 INT-8]

**Objective Exit Criteria:**

| # | Criterion | Verification Method | SDD Authority |
|---|---|---|---|
| SC-1 | Security Discovery is performed (§25.3). | Inspection | §25.3 |
| SC-2 | Authentication Discovery is performed; all authentication methods and flows are documented (§25.3). | Inspection | §25.3 |
| SC-3 | Authorization Discovery is performed; all authorization models and permissions are documented (§25.3). | Inspection | §25.3 |
| SC-4 | All security controls are identified and documented. | Inspection | §25 (Security Layer) |
| SC-5 | Security documentation is categorized per §38.2 and declares its authority class (§38 DOC-2). | Inspection | §38 DOC-2 |
| SC-6 | Security elements are traceable in the traceability graph (§48). | Inspection | §48 TGR-1 |
| SC-7 | No undocumented security rule exists (§40 INT-8). | Inspection | §40 INT-8 |

---

### 4.9 Workflow Complete

**Definition:** All workflows of the subject system are discovered and documented. No undocumented workflow remains. [Ref: §27.2; §25; §40 INT-7]

**Objective Exit Criteria:**

| # | Criterion | Verification Method | SDD Authority |
|---|---|---|---|
| WC-1 | Workflow Discovery is performed (§25.3). | Inspection | §25.3 |
| WC-2 | All business/workflows are identified and documented. | Inspection | §25.3 |
| WC-3 | All workflow states and transitions are identified and documented. | Inspection | §25 (Behavior Layer) |
| WC-4 | All events, event sources, and handlers are identified and documented (§25.3 Event Discovery). | Inspection | §25.3 |
| WC-5 | Workflow documentation is categorized per §38.2 and declares its authority class (§38 DOC-2). | Inspection | §38 DOC-2 |
| WC-6 | Workflows are traceable in the traceability graph (§48). | Inspection | §48 TGR-1 |
| WC-7 | No undocumented workflow exists (§40 INT-7). | Inspection | §40 INT-7 |

---

### 4.10 Runtime Complete

**Definition:** The runtime behavior of the subject system is observed, documented, and validated. [Ref: §27.2; §25; §26]

**Objective Exit Criteria:**

| # | Criterion | Verification Method | SDD Authority |
|---|---|---|---|
| RTC-1 | Runtime Observation is performed (§25.3). | Demonstration | §25.3 |
| RTC-2 | Actual runtime behavior is observed and documented (Level-A evidence per §26). | Demonstration | §26 (Level A) |
| RTC-3 | Runtime behavior is compared with source-derived expectations; divergences are recorded as findings (§26 EVC-6; §37 CPM-3). | Analysis | §26 EVC-6; §37 CPM-3 |
| RTC-4 | Runtime documentation carries confidence levels (§26), with runtime observations marked Level-A. | Inspection | §26 EVC-1 |
| RTC-5 | Runtime observations are traceable in the traceability graph (§48). | Inspection | §48 TGR-1 |
| RTC-6 | Canary/SLO verification is performed where applicable (§16.3). | Demonstration | §16.3 |

---

### 4.11 Documentation Complete

**Definition:** All required documentation is produced, categorized, and validated. [Ref: §27.2; §38]

**Objective Exit Criteria:**

| # | Criterion | Verification Method | SDD Authority |
|---|---|---|---|
| DOC-1 | All required documentation units are produced. | Inspection | §38 |
| DOC-2 | Each documentation unit declares its category (§38.2): Observed, Verified, Planned, Implemented, Validated, Historical, Deprecated, Generated, or Authoritative. | Inspection | §38 DOC-2 |
| DOC-3 | Each documentation unit declares its authority class (§11.1): Authoritative, Derived, or Generated. | Inspection | §38 DOC-2 |
| DOC-4 | Documentation does not mix categories within one authoritative unit (§38 DOC-1). | Inspection | §38 DOC-1 |
| DOC-5 | Generated documentation is not hand-edited and is reproducible (§38 DOC-3; RA-4). | Analysis | §38 DOC-3; RA-4 |
| DOC-6 | Observed/Planned documentation is not presented as Verified/Validated without passing the Evidence Chain / Validation (§38 DOC-4). | Inspection | §38 DOC-4 |
| DOC-7 | Deprecated/Historical documentation is retained and marked, not deleted (§38 DOC-5; §31 RKA-3). | Inspection | §38 DOC-5; §31 RKA-3 |
| DOC-8 | Documentation is traceable in the traceability graph (§48). | Inspection | §48 TGR-1 |

---

### 4.12 Validation Complete

**Definition:** All validation activities have been executed and conformance is objectively verified. [Ref: §27.2; §16]

**Objective Exit Criteria:**

| # | Criterion | Verification Method | SDD Authority |
|---|---|---|---|
| VC-1 | All applicable validation layers are executed per §16.3 ordering: static analysis, unit, integration, contract, regression, system/E2E, non-functional, runtime verification, review. | Inspection | §16.3 |
| VC-2 | Conformance verdict is objective pass/fail against stated criteria (§16 VL-1). | Analysis | §16 VL-1 |
| VC-3 | Each requirement class has a defined verification method (§16.2): Inspection, Analysis, Demonstration, or Test. | Inspection | §16 VL-2 |
| VC-4 | Validation evidence is recorded and reproducible (§16 VL-3). | Inspection | §16 VL-3 |
| VC-5 | The conformance verdict cites the evidence on which it rests (§16 VL-4). | Inspection | §16 VL-4 |
| VC-6 | Validation is performed independently from implementation (§16 VL-5; PR-8). | Inspection | §16 VL-5; PR-8 |
| VC-7 | Validation results are traceable in the traceability graph (§48). | Inspection | §48 TGR-1 |

---

### 4.13 Engineering Complete

**Definition:** The entire body of engineering work is complete. All subordinate completion states are satisfied, all evidence is recorded, and the repository is ready. [Ref: §27.2; §27.3 CMP-3]

**Objective Exit Criteria:**

| # | Criterion | Verification Method | SDD Authority |
|---|---|---|---|
| EC-1 | Discovery Complete (§4.1) is satisfied and evidenced. | Inspection | §27.3 CMP-3; §4.1 |
| EC-2 | Knowledge Complete (§4.2) is satisfied and evidenced. | Inspection | §27.3 CMP-3; §4.2 |
| EC-3 | Dependency Complete (§4.3) is satisfied and evidenced. | Inspection | §27.3 CMP-3; §4.3 |
| EC-4 | Architecture Complete (§4.4) is satisfied and evidenced. | Inspection | §27.3 CMP-3; §4.4 |
| EC-5 | Execution Flow Complete (§4.5) is satisfied and evidenced. | Inspection | §27.3 CMP-3; §4.5 |
| EC-6 | API Complete (§4.6) is satisfied and evidenced. | Inspection | §27.3 CMP-3; §4.6 |
| EC-7 | Database Complete (§4.7) is satisfied and evidenced. | Inspection | §27.3 CMP-3; §4.7 |
| EC-8 | Security Complete (§4.8) is satisfied and evidenced. | Inspection | §27.3 CMP-3; §4.8 |
| EC-9 | Workflow Complete (§4.9) is satisfied and evidenced. | Inspection | §27.3 CMP-3; §4.9 |
| EC-10 | Runtime Complete (§4.10) is satisfied and evidenced. | Inspection | §27.3 CMP-3; §4.10 |
| EC-11 | Documentation Complete (§4.11) is satisfied and evidenced. | Inspection | §27.3 CMP-3; §4.11 |
| EC-12 | Validation Complete (§4.12) is satisfied and evidenced. | Inspection | §27.3 CMP-3; §4.12 |
| EC-13 | All completion assertions are evidenced and recorded with provenance (§27.3 CMP-4). | Inspection | §27.3 CMP-4 |
| EC-14 | All §49 consistency invariants are satisfied. | Analysis | §49 CON-9 |
| EC-15 | All §40 integrity rules (INT-1..INT-10) are satisfied. | Inspection | §40 |
| EC-16 | The traceability graph (§48) is complete with no orphan objects. | Analysis | §48 TGR-1; §49 CON-1 |

## 5. Completion Criteria

This document is complete when:

1. All five normative rules CMP-1 through CMP-5 are stated (§3). [Ref: §27.3]
2. All thirteen completion states defined in §27.2 are specified with objective, verifiable exit criteria (§4). [Ref: §27.2]
3. Each completion state's criteria reference the applicable SDD sections.
4. "Engineering Complete" (§4.13) includes all subordinate states per CMP-3. [Ref: §27.3 CMP-3]
5. All criteria use RFC 2119 keywords per §46. [Ref: §46]
