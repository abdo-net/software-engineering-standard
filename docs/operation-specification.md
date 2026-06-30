# Operation Specification

> **Authority Class:** Authoritative
> **SDD Authority:** §34, §32
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 3

## 1. Purpose

This document specifies the closed set of engineering operations defined by the Engineering Operation Model (§34). Operations are specified by preconditions and postconditions, making them composable and verifiable. [Ref: §34.1; Meyer, Design by Contract; ISO/IEC/IEEE 12207 activities and tasks] This document implements the Phase-3 operational specification of the Operation Model defined architecturally in §34. [Ref: §34, Phase boundary note]

Only operations defined in this model **MAY** be performed under a Mission. [Ref: §34.4, OPS-1] A Mission's Allowed Operations are a subset of the operations defined herein. [Ref: §34.4, OPS-1; §32, MIS-3]

---

## 2. Normative Rules

### 2.1 OPS-1 — Closed Operation Set

Only operations in this model **MAY** be performed. A Mission's Allowed Operations are a subset (§32). [Ref: §34.4, OPS-1; §32, MIS-3] No operation outside the ten operations defined in §34.2 **MAY** be performed unless added through governance (§17). [Ref: OPS-1; §17]

### 2.2 OPS-2 — Precondition/Postcondition Enforcement

An operation **MUST NOT** execute unless its Preconditions hold; it **MUST** establish its Postconditions or fail explicitly. [Ref: §34.4, OPS-2; Meyer, Design by Contract] An operation that cannot establish its Postconditions **MUST** fail with recorded evidence of the failure. [Ref: OPS-2]

### 2.3 OPS-3 — Output Provenance and Confidence

Every operation's outputs **MUST** carry provenance (§28) and, for facts, confidence (§26). [Ref: §34.4, OPS-3; §26; §28] An output without provenance is non-authoritative. [Ref: §14.3, KN-1]

### 2.4 OPS-4 — Examination Operation Immutability

Examination operations (DISCOVER, TRACE, COMPARE, VERIFY) **MUST NOT** alter the subject system. [Ref: §34.4, OPS-4; REV-1; §30] This preserves the distinction between examination and modification established in the Reverse Engineering Architecture (§30). [Ref: OPS-4; §30.3, REV-1]

---

## 3. Operation Classification

### 3.1 Examination Operations (Non-Modifying)

Examination operations **MUST NOT** alter the subject system. [Ref: §34.4, OPS-4] These operations produce evidence and artifacts but do not change the system under engineering. [Ref: OPS-4]

| Operation | Governing Section | Purpose Summary |
|---|---|---|
| **DISCOVER** | §25 | Unknown system → understood system; inventory, structure, security, behavior discovery |
| **TRACE** | §29 | Bidirectional traceability across the engineering work chain |
| **COMPARE** | §37 | Objective comparison producing engineering evidence, never opinion |
| **VERIFY** | §16 | Objective conformance verification against stated criteria |

### 3.2 Modification Operations (System-Altering)

Modification operations **MAY** alter the subject system or its governing artifacts. These operations are subject to the full precondition/postcondition contract. [Ref: §34.3; OPS-2]

| Operation | Governing Section | Purpose Summary |
|---|---|---|
| **ANALYZE** | §12 Analysis | Examination producing engineering conclusions; feeds §36 |
| **DOCUMENT** | §38 | Categorized, non-mixed documentation production |
| **PLAN** | §35; §12 Planning | Decision recording and plan production before change |
| **IMPLEMENT** | §12 Implementation | Realizing approved decisions as changes |
| **VALIDATE** | §16 | Objective conformance check establishing a verdict |
| **REVIEW** | §15 | Criteria-based examination of artifacts |

### 3.3 Classification Ambiguity

ANALYZE produces engineering conclusions and feeds Impact Analysis (§36). While ANALYZE is primarily an examination operation, its outputs (conclusions, findings) **MAY** lead to system changes via subsequent IMPLEMENT operations. SDD does not explicitly classify ANALYZE as examination or modification. [Ref: §34.2] ANALYZE **MUST NOT** directly alter the subject system; changes **MUST** flow through the Decision Model (§35) and IMPLEMENT operation. [Ref: §35.3, DEC-4]

VALIDATE and VERIFY are distinct: VALIDATE is the objective conformance check ("are we building the right thing"); VERIFY is the examination against specification ("are we building it right"). [Ref: §16.1] Both are examination operations per their governing sections. SDD does not explicitly classify VALIDATE as examination or modification. [Ref: §34.2]

REVIEW is a criteria-based examination of artifacts. SDD does not explicitly classify REVIEW as examination or modification. [Ref: §34.2] REVIEW **MUST NOT** alter the artifact under review; findings **MUST** be recorded as evidence. [Ref: §15.2, RV-5]

---

## 4. Operation Specifications

### 4.1 DISCOVER

#### 4.1.1 Purpose

Transform an unknown system into an understood system through goal-directed, iterative, evidence-producing discovery. [Ref: §25.2] Discovery is organized into evidence layers; layers are dependency-ordered, not strictly sequential (LC-3). [Ref: §25.2]

#### 4.1.2 Inputs

SDD does not specify the formal Inputs for the DISCOVER operation. [Ref: §34.3] The Discovery Model (§25.2) defines the input as an "Unknown System." [Ref: §25.2]

#### 4.1.3 Outputs

Every discovery output **MUST** carry provenance (KN-1) and a confidence level (§26). [Ref: §25.4, DSC-2] The Discovery Model (§25.2) defines output as: Documentation, Verification → Discovery Complete (§27). [Ref: §25.2] Mandated discovery activities (coverage) are listed in §25.3.

#### 4.1.4 Preconditions

An unknown system **SHALL** pass through Discovery before any modification. [Ref: §25.4, DSC-1] Discovery **MUST** combine static and dynamic analysis and cross-validate (triangulate). [Ref: §25.4, DSC-3]

#### 4.1.5 Postconditions

Discovery is complete only when the "Discovery Complete" criteria (§27) are objectively met. [Ref: §25.4, DSC-5] No discovery conclusion **MAY** assert confidence exceeding its evidence (§26). [Ref: §25.4, DSC-6]

#### 4.1.6 Governing Section

§25 (Engineering Discovery Model). [Ref: §34.2]

---

### 4.2 ANALYZE

#### 4.2.1 Purpose

Produce engineering conclusions from examination of the subject system. Analysis feeds the Engineering Impact Analysis Model (§36). [Ref: §34.2; §12 Analysis]

#### 4.2.2 Inputs

SDD does not specify the formal Inputs for the ANALYZE operation. [Ref: §34.3] The Analysis phase of the Engineering Lifecycle (§12.2) consumes outputs from Discovery and Reverse Engineering. [Ref: §12.2]

#### 4.2.3 Outputs

SDD does not specify the formal Outputs for the ANALYZE operation. [Ref: §34.3] Analysis produces conclusions that feed §36 (Impact Analysis). [Ref: §34.2]

#### 4.2.4 Preconditions

SDD does not specify formal Preconditions for the ANALYZE operation. [Ref: §34.3] Analysis **MUST** produce conclusions backed by evidence from the subject system (LC-2). [Ref: §12.3, LC-2]

#### 4.2.5 Postconditions

SDD does not specify formal Postconditions for the ANALYZE operation. [Ref: §34.3] Analysis conclusions **MUST** feed the Impact Analysis Model (§36) when modification is contemplated. [Ref: §34.2; §36.3, IMP-2]

#### 4.2.6 Governing Section

§12 Analysis; feeds §36 (Engineering Impact Analysis Model). [Ref: §34.2]

---

### 4.3 TRACE

#### 4.3.1 Purpose

Maintain bidirectional traceability across the engineering work chain. [Ref: §29.1]

#### 4.3.2 Inputs

SDD does not specify the formal Inputs for the TRACE operation. [Ref: §34.3] Traceability operates on engineering objects (§43) connected by relationships (§44). [Ref: §29.2]

#### 4.3.3 Outputs

The SES **SHALL** maintain bidirectional traceability across the engineering work chain (§29.2). [Ref: §29.3, TRC-1] Traceability links **SHOULD** be generated artifacts (§11), not hand-maintained. [Ref: §29.3, TRC-3]

#### 4.3.4 Preconditions

Every engineering decision **MUST** be traceable backward (evidence/facts) and forward (implementation, test, documentation). [Ref: §29.3, TRC-2] A change to any node **MUST** be propagable to its linked nodes. [Ref: §29.3, TRC-4]

#### 4.3.5 Postconditions

Traceability links **SHOULD** be generated artifacts (§11), not hand-maintained, to prevent drift. [Ref: §29.3, TRC-3] The operational link schema is deferred to later phases. [Ref: §29.3, TRC-5]

#### 4.3.6 Governing Section

§29 (Engineering Traceability Expansion). [Ref: §34.2]

---

### 4.4 VERIFY

#### 4.4.1 Purpose

Verify conformance to specification — "are we building it right." [Ref: §16.1] VERIFY is an examination operation that produces an objective conformance verdict. [Ref: §34.2; §16]

#### 4.4.2 Inputs

SDD does not specify the formal Inputs for the VERIFY operation. [Ref: §34.3] Verification (§16) operates on implementations against their specifications. [Ref: §16.1]

#### 4.4.3 Outputs

A conformance verdict **MUST** cite the evidence on which it rests (PR-5). [Ref: §16.4, VL-4] Validation evidence **MUST** be recorded and reproducible. [Ref: §16.4, VL-3]

#### 4.4.4 Preconditions

Each requirement class **MUST** have a defined verification method (§16.2). [Ref: §16.4, VL-2] Conformance of a project to the SES **MUST** be expressed as objective pass/fail against stated criteria. [Ref: §16.4, VL-1]

#### 4.4.5 Postconditions

Verification **MUST** produce a recorded, evidenced conformance verdict. [Ref: §16.4, VL-4] Verification **MUST** be a responsibility distinct from implementation/execution (PR-8). [Ref: §16.4, VL-5]

#### 4.4.6 Governing Section

§16 (Validation Model). [Ref: §34.2]

---

### 4.5 DOCUMENT

#### 4.5.1 Purpose

Produce categorized, non-mixed documentation aligned to the Artifact Authority Model (§11) and the Repository Knowledge classes (§31). [Ref: §38.1]

#### 4.5.2 Inputs

SDD does not specify the formal Inputs for the DOCUMENT operation. [Ref: §34.3] Documentation inputs are knowledge artifacts (§14, §31) to be recorded. [Ref: §38.1]

#### 4.5.3 Outputs

Each documentation unit **SHALL** be classified as exactly one of: Observed; Verified; Planned; Implemented; Validated; Historical; Deprecated; Generated; Authoritative. [Ref: §38.2] Generated documentation **MUST NOT** be hand-edited and **MUST** be reproducible. [Ref: §38.3, DOC-3]

#### 4.5.4 Preconditions

Documentation **MUST NOT** mix the §38.2 categories within one authoritative unit. [Ref: §38.3, DOC-1] Each documentation unit **MUST** declare its category (§38.2) and its authority class (§11.2). [Ref: §38.3, DOC-2]

#### 4.5.5 Postconditions

Observed/Planned documentation **MUST NOT** be presented as Verified/Validated without passing the Evidence Chain (§28) / Validation (§16). [Ref: §38.3, DOC-4] Deprecated/Historical documentation **MUST** be retained and marked, not deleted. [Ref: §38.3, DOC-5]

#### 4.5.6 Governing Section

§38 (Engineering Documentation Model). [Ref: §34.2]

---

### 4.6 COMPARE

#### 4.6.1 Purpose

Produce objective comparison that yields engineering evidence, never opinion. [Ref: §37.1]

#### 4.6.2 Inputs

The model **SHALL** support comparison between: System vs Documentation; System vs System; Version vs Version; Implementation vs Contract; Database vs ORM; Runtime vs Source; API vs Documentation; Configuration vs Runtime. [Ref: §37.2]

#### 4.6.3 Outputs

Every comparison **MUST** produce engineering evidence (differences with provenance), never subjective judgment. [Ref: §37.3, CPM-1] Comparison results **MUST** be assigned a confidence level (§26). [Ref: §37.3, CPM-2]

#### 4.6.4 Preconditions

Comparison is an examination operation and **MUST NOT** alter either subject. [Ref: §37.3, CPM-4; OPS-4]

#### 4.6.5 Postconditions

Divergences **MUST** be recorded as findings and **MAY** raise Decisions (§35) or Risks (§21); they **MUST NOT** be silently reconciled. [Ref: §37.3, CPM-3]

#### 4.6.6 Governing Section

§37 (Engineering Comparison Model). [Ref: §34.2]

---

### 4.7 PLAN

#### 4.7.1 Purpose

Produce decisions and plans before change, governed by the Engineering Decision Model (§35) and the Planning phase of the Engineering Lifecycle (§12). [Ref: §34.2; §35; §12 Planning]

#### 4.7.2 Inputs

SDD does not specify the formal Inputs for the PLAN operation. [Ref: §34.3] Planning consumes outputs from Analysis (§12) and feeds the Decision Model (§35). [Ref: §34.2]

#### 4.7.3 Outputs

A Decision **SHALL** record: Decision; Decision Context; Alternatives; Evidence; Impact; Dependencies; Approval; Status; Superseded By. [Ref: §35.2] Every engineering decision **MUST** be recorded with all nine fields. [Ref: §35.3, DEC-1]

#### 4.7.4 Preconditions

A Decision **MUST** cite the Evidence (§26/§28) and the Impact Analysis (§36) that justify it. [Ref: §35.3, DEC-2] A change whose impact cannot be determined **MUST** be treated as high-risk and **MUST NOT** proceed without explicit Mission authorization (§32). [Ref: §36.3, IMP-4]

#### 4.7.5 Postconditions

A Decision is immutable once Approved; change occurs only by a new Decision setting "Superseded By" (consistent with KN-2). [Ref: §35.3, DEC-3] Every Implementation **MUST** trace back to exactly one engineering Decision. [Ref: §35.3, DEC-4]

#### 4.7.6 Governing Section

§35 (Engineering Decision Model); §12 Planning. [Ref: §34.2]

---

### 4.8 IMPLEMENT

#### 4.8.1 Purpose

Realize an approved decision as a change to the subject system. [Ref: §34.2; §12 Implementation]

#### 4.8.2 Inputs

SDD does not specify the formal Inputs for the IMPLEMENT operation. [Ref: §34.3] Implementation **MUST** trace back to exactly one engineering Decision (§35). [Ref: §35.3, DEC-4]

#### 4.8.3 Outputs

SDD does not specify the formal Outputs for the IMPLEMENT operation. [Ref: §34.3] Implementation produces changes to the subject system and associated evidence.

#### 4.8.4 Preconditions

Every Implementation **MUST** begin with an impact analysis spanning the §36.2 dimensions. [Ref: §36.3, IMP-1] Impact analysis **MUST** use the dependency view (§12 Analysis) and traceability (§29). [Ref: §36.3, IMP-2] Identified impacts **MUST** be recorded as evidence and **MUST** feed the authorizing Decision (§35). [Ref: §36.3, IMP-3]

#### 4.8.5 Postconditions

Every implementation **MUST** be documented (INT-1) and **MUST** trace to a Decision (§35) and documentation (§38). [Ref: §40.1, INT-1] A change whose impact cannot be determined **MUST** be treated as high-risk. [Ref: §36.3, IMP-4]

#### 4.8.6 Governing Section

§12 (Engineering Lifecycle — Implementation). [Ref: §34.2]

---

### 4.9 VALIDATE

#### 4.9.1 Purpose

Validate objective conformance — "are we building the right thing." [Ref: §16.1] VALIDATE is the operation that establishes a conformance verdict. [Ref: §34.2; §16]

#### 4.9.2 Inputs

SDD does not specify the formal Inputs for the VALIDATE operation. [Ref: §34.3] Validation operates on implementations and their recorded evidence. [Ref: §16]

#### 4.9.3 Outputs

A conformance verdict **MUST** cite the evidence on which it rests (PR-5). [Ref: §16.4, VL-4] Validation evidence **MUST** be recorded and reproducible. [Ref: §16.4, VL-3]

#### 4.9.4 Preconditions

Each requirement class **MUST** have a defined verification method (§16.2). [Ref: §16.4, VL-2] Conformance **MUST** be expressed as objective pass/fail against stated criteria. [Ref: §16.4, VL-1]

#### 4.9.5 Postconditions

Validation **MUST** produce a recorded conformance verdict with cited evidence. [Ref: §16.4, VL-4] Validation **MUST** be a responsibility distinct from implementation/execution (PR-8). [Ref: §16.4, VL-5] A conformance assertion (§16.5) **MUST** name the standard version it conforms to. [Ref: §18.2, VS-3]

#### 4.9.6 Governing Section

§16 (Validation Model). [Ref: §34.2]

---

### 4.10 REVIEW

#### 4.10.1 Purpose

Perform criteria-based examination of engineering artifacts. [Ref: §34.2; §15]

#### 4.10.2 Inputs

SDD does not specify the formal Inputs for the REVIEW operation. [Ref: §34.3] Review operates on authoritative artifacts (§11) against explicit, written criteria. [Ref: §15.2, RV-3]

#### 4.10.3 Outputs

Review outcomes (findings, disposition) **MUST** be recorded as evidence. [Ref: §15.2, RV-5] Every authoritative artifact **MUST** pass at least one review of an appropriate type before it becomes effective. [Ref: §15.2, RV-1]

#### 4.10.4 Preconditions

Review **MUST** be against explicit, written criteria (checklists/verification criteria), not reviewer preference. [Ref: §15.2, RV-3] Review of work **SHOULD** be performed by someone other than its sole author where independence adds value. [Ref: §15.2, RV-4]

#### 4.10.5 Postconditions

Review outcomes **MUST** be recorded as evidence. [Ref: §15.2, RV-5] Changes to the standard itself **MUST** undergo Inspection (the most rigorous form). [Ref: §15.2, RV-2] Review (§15) is human/criteria-based examination; validation (§16) is objective conformance verification; they are complementary and **MUST NOT** be merged (PR-8). [Ref: §15.3]

#### 4.10.6 Governing Section

§15 (Review Model). [Ref: §34.2]

---

## 5. Operation Constraints

### 5.1 Composite Constraint Summary

The following constraints derive from OPS-1 through OPS-4 and apply to all operations: [Ref: §34.4]

1. **Closed Set.** Only the ten operations defined in §4.1 through §4.10 **MAY** be performed. [Ref: OPS-1]
2. **Mission Binding.** A Mission's Allowed Operations **MUST** be a subset of the ten operations. [Ref: OPS-1; §32, MIS-3]
3. **Contract Enforcement.** No operation **MAY** execute unless its Preconditions hold. [Ref: OPS-2]
4. **Postcondition Obligation.** Every operation **MUST** establish its Postconditions or fail explicitly. [Ref: OPS-2]
5. **Output Provenance.** Every output **MUST** carry provenance (§28) and, for facts, confidence (§26). [Ref: OPS-3]
6. **Examination Immutability.** DISCOVER, TRACE, COMPARE, and VERIFY **MUST NOT** alter the subject system. [Ref: OPS-4]

### 5.2 Operation-to-Mission Binding

A Mission **MUST** define Allowed Operations as a subset of the ten operations herein. [Ref: §32.2; §34.4, OPS-1] A Mission **MUST** define Forbidden Operations. [Ref: §32.2] Forbidden Operations **MUST** be drawn from the Operation Model (§34). [Ref: §32.3, MIS-3]

### 5.3 Operation-to-State Relationship

Operations are performed while the subject system occupies states. SDD does not specify a formal operation-to-state binding matrix. [Ref: §34] The following derived mapping is consistent with the lifecycle (§12.2) and state machine (§33.2):

| Operation | Typically Performed In State | Lifecycle Phase |
|---|---|---|
| DISCOVER | DISCOVERING | Discovery/Understanding |
| ANALYZE | UNDERSTOOD | Analysis |
| TRACE | All states | Cross-cutting |
| VERIFY | VALIDATING | Validation |
| DOCUMENT | DOCUMENTED | Documentation |
| COMPARE | All states | Cross-cutting |
| PLAN | PLANNED | Planning |
| IMPLEMENT | IMPLEMENTING | Implementation |
| VALIDATE | VALIDATING | Validation |
| REVIEW | All states | Cross-cutting (gating) |

SDD does not specify this table; it is a derived operational interpretation. [Ref: §34; §33.2]

---

## 6. Completion Criteria

This document is complete when: [Ref: §34.3; §34.4]

1. All ten operations are specified with their four mandatory elements (Inputs, Outputs, Preconditions, Postconditions). [Ref: §34.3]
2. All four normative rules (OPS-1 through OPS-4) are specified with citations. [Ref: §34.4]
3. Operations are classified as examination or modification per OPS-4. [Ref: §34.4, OPS-4]
4. Operation constraints are specified as a composite of OPS-1 through OPS-4. [Ref: §34.4]
5. Each operation cites its governing section. [Ref: §34.2]

**Note:** Elements marked "SDD does not specify" in this document are architectural gaps that later phases **SHALL** close. Per §34's Phase boundary note, operation procedures are Phase-3 / Phase-5 deliverables; this document specifies the operation set and contracts at the architectural level. [Ref: §34, Phase boundary note]
