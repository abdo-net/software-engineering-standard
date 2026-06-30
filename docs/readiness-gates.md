# Readiness Gates

> **Authority Class:** Authoritative
> **SDD Authority:** §41.2, §41.3, §27, §40, §35, §16, §38, §29, §32, §34, §50
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 5

## 1. Purpose

This document specifies the nine readiness gates that determine when a repository is ready for implementation. Readiness is the aggregate of Completion States (§27); the gates introduce no new criteria, only their composition. [Ref: §41.1; §41.2]

Each readiness gate is an objective, verifiable checkpoint. A gate is satisfied only when its constituent conditions are met and evidenced. [Ref: §41.3 RDY-1, RDY-2]

## 2. Scope

This document defines all nine readiness gates mandated by §41.2 and the five normative rules of §41.3. It specifies per-gate criteria, dependencies between gates, and the conditions under which readiness is established or revoked.

This document does NOT define: the per-state completion criteria (defined in `completion-criteria.md` per §27); the operational readiness verification procedures (Phase 6); the readiness checklist template (Phase 8); the conformance assertion procedure (§16.5, Phase 6).

## 3. Normative Rules (RDY-1..RDY-5)

The following rules govern all readiness gates. Violation of any rule renders a readiness assertion non-conformant. [Ref: §41.3]

| ID | Rule | Evidence |
|---|---|---|
| **RDY-1** | "Implementation Ready" **MUST NOT** be asserted unless all subordinate gates (§41.2) are objectively satisfied. Implementation Ready is the terminal gate; it requires all preceding gates. | [Ref: §27; PR-7] |
| **RDY-2** | Readiness gates **MUST** be evidenced (provenance) and recorded. An unrecorded readiness assertion is non-conformant. | [Ref: PR-5] |
| **RDY-3** | Any INT (§40) violation **MUST** block "Repository Ready". INT violations are completeness invariants; no gate that depends on repository integrity may pass while an INT rule is violated. | [Ref: §40] |
| **RDY-4** | Readiness is re-evaluated each cycle (§39); prior readiness **MUST NOT** persist across material change (§36). A change that triggers impact analysis invalidates prior readiness until re-verified. | [Ref: §39; §36] |
| **RDY-5** | Detailed gate criteria are the per-state criteria of §27; §41 defines composition only. This document realizes that composition. | [Ref: §27; Development Order] |

## 4. Readiness Gates

### 4.1 Architecture Complete

**Definition:** The Architecture Complete readiness gate is satisfied when the Architecture Complete completion state (§27) is objectively met. [Ref: §41.2]

**Gate Criteria:**

| # | Criterion | SDD Authority |
|---|---|---|
| ARC-1 | Architecture Complete completion state (§27) exit criteria are verified per CMP-1 and CMP-2. | §27; §27.3 CMP-1, CMP-2 |
| ARC-2 | Architecture decisions are recorded as ADRs with all nine fields (§35.2). | §35 DEC-1 |
| ARC-3 | Architecture decisions are immutable once accepted (§35 DEC-3). | §35 DEC-3 |
| ARC-4 | No undocumented architecture element exists (§40 INT-1, INT-2). | §40 |
| ARC-5 | Architecture recovery outputs carry provenance (§28) and confidence (§26). | §28; §26 |
| ARC-6 | The readiness assertion is evidenced and recorded (RDY-2). | §41.3 RDY-2 |

**Gate State:**
- **Satisfied when:** All criteria ARC-1 through ARC-6 are met.
- **Blocked by:** Any INT violation (RDY-3); unverified Architecture Complete completion state.

---

### 4.2 Knowledge Complete

**Definition:** The Knowledge Complete readiness gate is satisfied when the Knowledge Complete completion state (§27) is objectively met. [Ref: §41.2]

**Gate Criteria:**

| # | Criterion | SDD Authority |
|---|---|---|
| KNC-1 | Knowledge Complete completion state (§27) exit criteria are verified per CMP-1 and CMP-2. | §27; §27.3 CMP-1, CMP-2 |
| KNC-2 | All facts carry provenance (§14.3 KN-1). | §14.3 KN-1 |
| KNC-3 | Knowledge progression follows Observed -> Verified -> Engineering Knowledge (§31 RKA-2). | §31 RKA-2 |
| KNC-4 | Hypotheses are marked as hypotheses (§14.3 KN-3; §26 EVC-3). | §14.3 KN-3 |
| KNC-5 | Knowledge resides in the repository (§14.3 KN-5). | §14.3 KN-5 |
| KNC-6 | The readiness assertion is evidenced and recorded (RDY-2). | §41.3 RDY-2 |

**Gate State:**
- **Satisfied when:** All criteria KNC-1 through KNC-6 are met.
- **Blocked by:** Any INT violation (RDY-3); facts without provenance.

---

### 4.3 Discovery Complete

**Definition:** The Discovery Complete readiness gate is satisfied when the Discovery Complete completion state (§27) is objectively met. [Ref: §41.2]

**Gate Criteria:**

| # | Criterion | SDD Authority |
|---|---|---|
| DSC-1 | Discovery Complete completion state (§27) exit criteria are verified per CMP-1 and CMP-2. | §27; §27.3 CMP-1, CMP-2 |
| DSC-2 | All mandated discovery activities (§25.3) are performed. | §25.3 |
| DSC-3 | Discovery outputs carry provenance (§28) and confidence (§26). | §25 DSC-2; §26 |
| DSC-4 | Cross-validation is performed; disagreements are recorded (§25 DSC-3). | §25 DSC-3 |
| DSC-5 | The readiness assertion is evidenced and recorded (RDY-2). | §41.3 RDY-2 |

**Gate State:**
- **Satisfied when:** All criteria DSC-1 through DSC-5 are met.
- **Blocked by:** Any INT violation (RDY-3); incomplete discovery activities.

---

### 4.4 Decision Complete

**Definition:** The Decision Complete readiness gate is satisfied when all required Decisions are recorded and Approved (§35). [Ref: §41.2]

**Gate Criteria:**

| # | Criterion | SDD Authority |
|---|---|---|
| DEC-1 | All required engineering decisions are recorded with all nine fields (§35.2). | §35 DEC-1 |
| DEC-2 | All recorded decisions are in "Approved" status. | §35.2 (Status field) |
| DEC-3 | All decisions are immutable once approved (§35 DEC-3); no silently edited decisions exist. | §35 DEC-3 |
| DEC-4 | Every implementation traces back to exactly one engineering Decision (§35 DEC-4; §40 INT-1). | §35 DEC-4; §40 INT-1 |
| DEC-5 | Decisions cite evidence (§26/§28) and impact analysis (§36). | §35 DEC-2 |
| DEC-6 | The readiness assertion is evidenced and recorded (RDY-2). | §41.3 RDY-2 |

**Gate State:**
- **Satisfied when:** All criteria DEC-1 through DEC-6 are met.
- **Blocked by:** Any unrecorded decision required for the Mission; any decision not in Approved status.

---

### 4.5 Documentation Complete

**Definition:** The Documentation Complete readiness gate is satisfied when the Documentation Complete completion state (§27) is met and the Engineering Documentation Model (§38) is satisfied. [Ref: §41.2]

**Gate Criteria:**

| # | Criterion | SDD Authority |
|---|---|---|
| DOCC-1 | Documentation Complete completion state (§27) exit criteria are verified per CMP-1 and CMP-2. | §27; §27.3 CMP-1, CMP-2 |
| DOCC-2 | §38 Documentation Model is satisfied. | §38 |
| DOCC-3 | Each documentation unit declares its category (§38.2) and authority class (§38 DOC-2). | §38 DOC-2 |
| DOCC-4 | Documentation does not mix categories within one authoritative unit (§38 DOC-1). | §38 DOC-1 |
| DOCC-5 | Generated documentation is not hand-edited and is reproducible (§38 DOC-3; RA-4). | §38 DOC-3 |
| DOCC-6 | Deprecated/Historical documentation is retained and marked (§38 DOC-5). | §38 DOC-5 |
| DOCC-7 | The readiness assertion is evidenced and recorded (RDY-2). | §41.3 RDY-2 |

**Gate State:**
- **Satisfied when:** All criteria DOCC-1 through DOCC-7 are met.
- **Blocked by:** Any INT violation (RDY-3); undocumented elements per §40.

---

### 4.6 Traceability Complete

**Definition:** The Traceability Complete readiness gate is satisfied when the §29 traceability chain is complete and no INT (§40) violations exist. [Ref: §41.2]

**Gate Criteria:**

| # | Criterion | SDD Authority |
|---|---|---|
| TC-1 | The engineering traceability chain (§29.2) is complete bidirectionally. | §29 TRC-1 |
| TC-2 | Every engineering decision is traceable backward (evidence/facts) and forward (implementation, test, documentation) (§29 TRC-2). | §29 TRC-2 |
| TC-3 | Traceability links are generated artifacts where feasible (§29 TRC-3). | §29 TRC-3 |
| TC-4 | No INT (§40) violation exists. Specifically: no orphan object (CON-1), no duplicate authority (CON-2), no duplicate ownership (CON-3), no broken traceability (CON-4), no broken dependency (CON-5), no circular authority (CON-6), no conflicting lifecycle state (CON-7), no invalid relationship (CON-8). | §40; §49 CON-1..CON-8 |
| TC-5 | Every engineering object is a node in the traceability graph (§48 TGR-1). | §48 TGR-1 |
| TC-6 | The readiness assertion is evidenced and recorded (RDY-2). | §41.3 RDY-2 |

**Gate State:**
- **Satisfied when:** All criteria TC-1 through TC-6 are met.
- **Blocked by:** Any INT violation (RDY-3); orphan objects; broken traceability links.

---

### 4.7 Validation Ready

**Definition:** The Validation Ready readiness gate is satisfied when the §16 preconditions are met. [Ref: §41.2]

**Gate Criteria:**

| # | Criterion | SDD Authority |
|---|---|---|
| VR-1 | The Validation Model (§16) preconditions are met. | §16 |
| VR-2 | Verification methods are defined for each requirement class (§16 VL-2). | §16 VL-2 |
| VR-3 | Validation evidence will be recorded and reproducible (§16 VL-3). | §16 VL-3 |
| VR-4 | Validation is a responsibility distinct from implementation (§16 VL-5; PR-8). | §16 VL-5; PR-8 |
| VR-5 | The fast-feedback validation ordering (§16.3) is established. | §16.3 |
| VR-6 | The readiness assertion is evidenced and recorded (RDY-2). | §41.3 RDY-2 |

**Gate State:**
- **Satisfied when:** All criteria VR-1 through VR-6 are met.
- **Blocked by:** Undefined verification methods; validation not independent from implementation.

---

### 4.8 Implementation Ready

**Definition:** The Implementation Ready readiness gate is satisfied when all subordinate gates (§4.1 through §4.7) are satisfied AND the Mission Allowed Operations include IMPLEMENT (§32, §34). [Ref: §41.2; §41.3 RDY-1]

**Gate Criteria:**

| # | Criterion | SDD Authority |
|---|---|---|
| IR-1 | Architecture Complete gate (§4.1) is satisfied. | §41.2; §41.3 RDY-1 |
| IR-2 | Knowledge Complete gate (§4.2) is satisfied. | §41.2; §41.3 RDY-1 |
| IR-3 | Discovery Complete gate (§4.3) is satisfied. | §41.2; §41.3 RDY-1 |
| IR-4 | Decision Complete gate (§4.4) is satisfied. | §41.2; §41.3 RDY-1 |
| IR-5 | Documentation Complete gate (§4.5) is satisfied. | §41.2; §41.3 RDY-1 |
| IR-6 | Traceability Complete gate (§4.6) is satisfied. | §41.2; §41.3 RDY-1 |
| IR-7 | Validation Ready gate (§4.7) is satisfied. | §41.2; §41.3 RDY-1 |
| IR-8 | Mission Allowed Operations include IMPLEMENT (§32 MIS-3; §34). | §32 MIS-3; §34 |
| IR-9 | Impact analysis (§36 IMP-1) is performed for the planned implementation. | §36 IMP-1 |
| IR-10 | The readiness assertion is evidenced and recorded (RDY-2). | §41.3 RDY-2 |

**Gate State:**
- **Satisfied when:** All criteria IR-1 through IR-10 are met.
- **Blocked by:** Any unsatisfied subordinate gate (IR-1 through IR-7); Mission not authorizing IMPLEMENT; unperformed impact analysis.
- **Special Rule:** This gate MUST NOT be asserted unless all subordinate gates are objectively satisfied (RDY-1). [Ref: §41.3 RDY-1]

---

### 4.9 Repository Ready

**Definition:** The Repository Ready readiness gate is satisfied when all gates above (§4.1 through §4.8) are satisfied AND all consistency invariants (§49) and integrity rules (§40) are satisfied. [Ref: §41.2; §41.3 RDY-3]

**Gate Criteria:**

| # | Criterion | SDD Authority |
|---|---|---|
| RR-1 | Architecture Complete gate (§4.1) is satisfied. | §41.2 |
| RR-2 | Knowledge Complete gate (§4.2) is satisfied. | §41.2 |
| RR-3 | Discovery Complete gate (§4.3) is satisfied. | §41.2 |
| RR-4 | Decision Complete gate (§4.4) is satisfied. | §41.2 |
| RR-5 | Documentation Complete gate (§4.5) is satisfied. | §41.2 |
| RR-6 | Traceability Complete gate (§4.6) is satisfied. | §41.2 |
| RR-7 | Validation Ready gate (§4.7) is satisfied. | §41.2 |
| RR-8 | Implementation Ready gate (§4.8) is satisfied. | §41.2 |
| RR-9 | All §49 consistency invariants (CON-1..CON-8) are satisfied. | §49 |
| RR-10 | All §40 integrity rules (INT-1..INT-10) are satisfied. | §40 |
| RR-11 | No orphan object exists in the traceability graph (§48 TGR-1; §49 CON-1). | §48 TGR-1; §49 CON-1 |
| RR-12 | Repository Completeness dimensions (§50.2) are satisfied where applicable. | §50 CPL-1 |
| RR-13 | The readiness assertion is evidenced and recorded (RDY-2). | §41.3 RDY-2 |

**Gate State:**
- **Satisfied when:** All criteria RR-1 through RR-13 are met.
- **Blocked by:** Any unsatisfied subordinate gate; any INT violation (RDY-3); any §49 invariant violation.
- **Special Rule:** Any INT violation MUST block Repository Ready (RDY-3). [Ref: §41.3 RDY-3]

## 5. Gate Dependencies

The readiness gates form a directed acyclic graph. Satisfying a gate requires all gates it depends upon to be satisfied first. [Ref: §41.2; §45]

```
Architecture Complete ----┐
Knowledge Complete --------┤
Discovery Complete --------┤
Decision Complete ---------┤
Documentation Complete ----┼──> Implementation Ready ──> Repository Ready
Traceability Complete -----┤
Validation Ready ----------┘
```

**Dependency Rules:**

| Gate | Depends On | SDD Authority |
|---|---|---|
| Architecture Complete | Discovery Complete (recommended ordering) | §25; §12.2 |
| Knowledge Complete | Discovery Complete | §25; §14 |
| Discovery Complete | (entry gate; no dependencies) | §25 |
| Decision Complete | Architecture Complete, Knowledge Complete (recommended) | §35; §12.2 |
| Documentation Complete | Knowledge Complete, Architecture Complete (recommended) | §38; §12.2 |
| Traceability Complete | All completion states with traceable outputs | §29; §48 |
| Validation Ready | Documentation Complete (recommended) | §16; §12.2 |
| Implementation Ready | Architecture Complete, Knowledge Complete, Discovery Complete, Decision Complete, Documentation Complete, Traceability Complete, Validation Complete | §41.2; §41.3 RDY-1 |
| Repository Ready | All gates above | §41.2; §41.3 RDY-3 |

**Re-evaluation Rule:** Per RDY-4, readiness is re-evaluated each cycle (§39). Prior readiness MUST NOT persist across material change (§36). Any change that triggers impact analysis (§36) invalidates all downstream gates until re-verified. [Ref: §41.3 RDY-4; §39; §36]

## 6. Completion Criteria

This document is complete when:

1. All five normative rules RDY-1 through RDY-5 are stated (§3). [Ref: §41.3]
2. All nine readiness gates defined in §41.2 are specified with gate criteria (§4). [Ref: §41.2]
3. Gate dependencies are documented as a directed acyclic graph (§5). [Ref: §45 DEP-2]
4. The re-evaluation rule (RDY-4) is stated (§5). [Ref: §41.3 RDY-4]
5. Every gate criterion references its SDD authority.
6. All criteria use RFC 2119 keywords per §46. [Ref: §46]
