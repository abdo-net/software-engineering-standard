# Knowledge Model Schemas

> **Authority Class:** Authoritative
> **SDD Authority:** §14.2, §14.3, §31.2
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 4

## 1. Purpose

This document defines the schemas for all six knowledge categories of the SES Knowledge Model. [Ref: §14.2] The Knowledge Model defines how engineering knowledge is captured, structured, and preserved so that it survives people, sessions, and tools. [Ref: §14.1] Each knowledge category is an authoritative artifact per §14.2 and §11.1.

## 2. Scope

This document specifies schemas for:

1. **Facts** — Verified statements with provenance [Ref: §14.2, KN-1, EVC-1..EVC-6]
2. **Decisions** — ADR-format, immutable [Ref: §14.2, KN-2, DEC-1..DEC-4]
3. **Contracts** — Agreed interfaces + semantics [Ref: §14.2, §11.3]
4. **Invariants** — Constraints that MUST remain true [Ref: §14.2, §11.3]
5. **Rationale** — Why a decision was made; alternatives [Ref: §14.2, §35.2]
6. **Provenance** — Link from fact to source evidence [Ref: §14.2, KN-1, §28]

Each schema SHALL conform to the Object Model (§43), the Artifact Authority Model (§11.1), and the mandatory artifact metadata (§11.2).

## 3. Knowledge Categories

### 3.1 Facts Schema

**Authority Class:** Authoritative (Candidate-authoritative until verified). [Ref: §14.2, §31.2]

**Definition:** Verified statements about the system, each with provenance. [Ref: §14.2]

#### Fields

| Field | Cardinality | Type | Source |
|---|---|---|---|
| **Fact ID** | 1 | Unique identifier | §11.2, §43.2 |
| **Object Type** | 1 | Fixed: `Fact` | §42.2, §43.2 |
| **Authority Class** | 1 | Authoritative / Candidate-authoritative | §11.1, §31.2 |
| **Statement** | 1 | The verified statement | §14.2 (Facts definition) |
| **Confidence Level** | 1 | A–E per §26.2 | §26.3, EVC-1 |
| **Evidence Source** | 1..* | Reference to source evidence | §26.3, KN-1 |
| **Verification Status** | 1 | Unverified / Verified / Rejected | §26.3 |
| **Timestamp** | 1 | ISO 8601 | §26.3 |
| **Repository Reference** | 1 | Canonical repository location | §26.3 |
| **Provenance Record** | 1 | Link to Provenance Record | §11.3, KN-1 |
| **Owner** | 1 | Single accountable owner | §11.2, §43.2 |
| **Status** | 1 | Draft / Accepted / Superseded / Deprecated | §11.2, §43.2 |
| **Version** | 1 | Semantic version | §18, §43.2 |
| **Triangulation Sources** | 0..* | Corroborating sources (static, dynamic, human) | KN-6 |

#### Normative Rules

- **KN-1**: Every recorded fact MUST carry provenance — a reference to the source evidence from which it was derived. A fact without provenance is non-authoritative. [Ref: §14.3, KN-1]
- **KN-3**: A hypothesis MUST be marked as a hypothesis until verified by evidence; it MUST NOT be recorded as a fact. [Ref: §14.3, KN-3]
- **KN-6**: Where feasible, a fact SHOULD be corroborated by more than one source class (static, dynamic, human) before being recorded as authoritative. [Ref: §14.3, KN-6]
- **EVC-1**: Every engineering fact MUST carry a confidence level (A–E). [Ref: §26.4, EVC-1]
- **EVC-2**: Every fact MUST record all five fields (§26.3). [Ref: §26.4, EVC-2]
- **EVC-3**: A Level-E fact is a hypothesis and MUST NOT be treated as authoritative. [Ref: §26.4, EVC-3]
- **EVC-4**: No fact MAY become authoritative without a confidence classification. [Ref: §26.4, EVC-4]
- **EVC-5**: Confidence MAY be raised only by recording additional evidence/provenance; it MUST NOT be raised by assertion. [Ref: §26.4, EVC-5]
- **EVC-6**: Where Level-A evidence conflicts with B/C, the conflict MUST be recorded as a finding/risk; the higher-fidelity (runtime) evidence governs the recorded behavior. [Ref: §26.4, EVC-6]

### 3.2 Decisions Schema

**Authority Class:** Authoritative (immutable once accepted). [Ref: §14.2, §31.2]

**Definition:** Architecture/engineering decisions, ADR-format, immutable once accepted. [Ref: §14.2]

#### Fields

| Field | Cardinality | Type | Source |
|---|---|---|---|
| **Decision ID** | 1 | Unique identifier | §11.2, §43.2 |
| **Object Type** | 1 | Fixed: `Decision` | §42.2, §43.2 |
| **Authority Class** | 1 | Authoritative | §11.1 |
| **Decision** | 1 | The decision statement | §35.2 |
| **Decision Context** | 1 | Situation motivating the decision | §35.2 |
| **Alternatives** | 1..* | Options considered | §35.2 |
| **Evidence** | 1..* | Supporting evidence references | §35.2, DEC-2 |
| **Impact** | 1..* | Impact analysis references | §35.2, DEC-2, §36 |
| **Dependencies** | 0..* | Dependent decisions, components, contracts | §35.2 |
| **Approval** | 1 | Approval status and authority | §35.2, §17 |
| **Status** | 1 | Proposed / Approved / Rejected / Superseded | §35.2 |
| **Superseded By** | 0..1 | Reference to superseding decision | §35.2, KN-2 |
| **Owner** | 1 | Single accountable owner | §11.2, §43.2 |
| **Version** | 1 | Semantic version | §18, §43.2 |
| **Rationale** | 1 | Link to Rationale record | §35.2, §14.2 |
| **Implementation Refs** | 0..* | Links to implementing artifacts | DEC-4 |

#### Normative Rules

- **KN-2**: Decisions MUST be recorded in an immutable, append/supersede format (ADR). An accepted decision MUST NOT be silently edited; it is superseded by a new record. [Ref: §14.3, KN-2]
- **DEC-1**: Every engineering decision MUST be recorded with all nine fields (§35.2). [Ref: §35.3, DEC-1]
- **DEC-2**: A Decision MUST cite the Evidence (§26/§28) and the Impact Analysis (§36) that justify it. [Ref: §35.3, DEC-2]
- **DEC-3**: A Decision is immutable once Approved; change occurs only by a new Decision setting Superseded By. [Ref: §35.3, DEC-3]
- **DEC-4**: Every Implementation MUST trace back to exactly one engineering Decision. [Ref: §35.3, DEC-4]

### 3.3 Contracts Schema

**Authority Class:** Authoritative. [Ref: §14.2, §11.3]

**Definition:** Agreed interfaces + semantics across boundaries. [Ref: §14.2]

#### Fields

| Field | Cardinality | Type | Source |
|---|---|---|---|
| **Contract ID** | 1 | Unique identifier | §11.2, §43.2 |
| **Object Type** | 1 | Fixed: `Contract` | §42.2, §43.2 |
| **Authority Class** | 1 | Authoritative | §11.1, §11.3 |
| **Interface Definition** | 1 | Technical interface specification | §14.2, §11.3 |
| **Semantics** | 1 | Behavioral contract (pre/post/invariants) | §14.2, §11.3 |
| **Boundary** | 1 | The boundary this contract governs | §14.2 |
| **Consumers** | 1..* | Entities that depend on this contract | §11.3 |
| **Providers** | 1..* | Entities that implement this contract | §11.3 |
| **Owner** | 1 | Single accountable owner | §11.2, §43.2 |
| **Status** | 1 | Draft / Accepted / Superseded / Deprecated | §11.2 |
| **Version** | 1 | Semantic version | §18, §43.2 |
| **Governance Record** | 1 | Link to approving governance decision | §14.3, KN-4, §17 |
| **Validation Refs** | 0..* | Links to validation records | §16 |

#### Normative Rules

- **KN-4**: Contracts and invariants are authoritative and changes to them MUST pass through governance + versioning (§17–§18). [Ref: §14.3, KN-4]
- Contracts SHALL conform to established contract formats (OpenAPI, AsyncAPI, Protocol Buffers) as cited in §11.3. [Ref: §11.3]
- Every API MUST have a contract. [Ref: §40, INT-4]

### 3.4 Invariants Schema

**Authority Class:** Authoritative. [Ref: §14.2, §11.3]

**Definition:** Constraints that MUST remain true. [Ref: §14.2]

#### Fields

| Field | Cardinality | Type | Source |
|---|---|---|---|
| **Invariant ID** | 1 | Unique identifier | §11.2, §43.2 |
| **Object Type** | 1 | Fixed: `Invariant` | §42.2, §43.2 |
| **Authority Class** | 1 | Authoritative | §11.1, §11.3 |
| **Constraint Statement** | 1 | The constraint that MUST remain true | §14.2, §11.3 |
| **Scope** | 1 | Component / system / organization-wide | §14.2 |
| **Enforcement** | 1 | Mechanism by which the invariant is checked | §40 |
| **Violation Action** | 1 | Action taken on violation | §40.2 |
| **Owner** | 1 | Single accountable owner | §11.2, §43.2 |
| **Status** | 1 | Active / Waived / Deprecated | §11.2 |
| **Version** | 1 | Semantic version | §18, §43.2 |
| **Governance Record** | 1 | Link to approving governance decision | §14.3, KN-4, §17 |
| **Related Decisions** | 0..* | Decisions that establish or affect this invariant | §35 |

#### Normative Rules

- **KN-4**: Contracts and invariants are authoritative and changes to them MUST pass through governance + versioning (§17–§18). [Ref: §14.3, KN-4]
- Invariants SHALL correspond to the Integrity Rules defined in §40 where applicable. [Ref: §40]
- Violation of any invariant renders the affected work non-conformant per §40.2. [Ref: §40.2]
- Invariants MAY be waived only through governance (§17). [Ref: §40.2]

### 3.5 Rationale Schema

**Authority Class:** Authoritative. [Ref: §14.2]

**Definition:** Why a decision was made; alternatives considered. [Ref: §14.2]

#### Fields

| Field | Cardinality | Type | Source |
|---|---|---|---|
| **Rationale ID** | 1 | Unique identifier | §11.2, §43.2 |
| **Object Type** | 1 | Fixed: `Rationale` | §42.2, §43.2 |
| **Authority Class** | 1 | Authoritative | §11.1 |
| **Decision Reference** | 1 | Link to the decision this rationale explains | §35.2, §14.2 |
| **Context** | 1 | Situation and forces at play | §35.2 |
| **Alternatives Considered** | 1..* | Options evaluated with pros/cons | §35.2, §14.2 |
| **Selected Alternative** | 1 | The chosen option | §35.2 |
| **Justification** | 1 | Evidence-based reasoning for the selection | §35.2, PR-1 |
| **Consequences** | 1..* | Positive and negative consequences | §35.2 |
| **Owner** | 1 | Single accountable owner | §11.2, §43.2 |
| **Status** | 1 | Draft / Accepted / Superseded / Deprecated | §11.2 |
| **Version** | 1 | Semantic version | §18, §43.2 |

#### Normative Rules

- Rationale SHALL be recorded for every engineering Decision. [Ref: §35.2, DEC-1]
- Rationale SHALL cite evidence from the approved evidence base (Appendix A) or be marked UNSUPPORTED. [Ref: PR-1, FR-11]
- The combination of KN-1 + KN-3 + KN-6 is the standard's structural defense against converting assumptions into facts; Rationale SHALL support this defense by documenting the evidence basis for decisions. [Ref: §14.4]

### 3.6 Provenance Schema

**Authority Class:** Authoritative. [Ref: §14.2]

**Definition:** Link from any fact to its source evidence. [Ref: §14.2]

#### Fields

| Field | Cardinality | Type | Source |
|---|---|---|---|
| **Provenance ID** | 1 | Unique identifier | §11.2, §43.2 |
| **Object Type** | 1 | Fixed: `Provenance` | §42.2, §43.2 |
| **Authority Class** | 1 | Authoritative | §11.1 |
| **Fact Reference** | 1 | Link to the fact being provenanced | §14.2, KN-1 |
| **Evidence References** | 1..* | Links to source evidence | §28, ECH-2 |
| **Confidence Level** | 1 | A–E per §26.2 | §26.3, EVC-1 |
| **Verification Status** | 1 | Unverified / Verified / Rejected | §26.3 |
| **Timestamp** | 1 | ISO 8601 | §26.3 |
| **Repository Reference** | 1 | Canonical repository location | §26.3 |
| **Chain Position** | 1 | Position in Evidence Chain (§28.2) | §28.2 |
| **Upstream Link** | 0..1 | Predecessor in Evidence Chain | ECH-2 |
| **Downstream Links** | 0..* | Successors in Evidence Chain | ECH-3 |
| **Owner** | 1 | Single accountable owner | §11.2, §43.2 |
| **Status** | 1 | Draft / Accepted / Superseded / Deprecated | §11.2 |
| **Version** | 1 | Semantic version | §18, §43.2 |

#### Normative Rules

- **KN-1**: Every recorded fact MUST carry provenance — a reference to the source evidence from which it was derived. A fact without provenance is non-authoritative. [Ref: §14.3, KN-1]
- **ECH-1**: An observation MUST NOT be recorded as an engineering fact without passing Evidence → Verification. [Ref: §28.3, ECH-1]
- **ECH-2**: Each link MUST preserve provenance to its predecessor (unbroken chain of custody). [Ref: §28.3, ECH-2]
- **ECH-3**: Every Decision MUST trace backward to verified facts and forward to Implementation, Validation, and Documentation. [Ref: §28.3, ECH-3]
- **ECH-4**: Asserting a downstream node without its upstream evidence (a broken chain) is non-conformant. [Ref: §28.3, ECH-4]
- **ECH-5**: Hypotheses (confidence E, §26) MUST NOT pass the Verification link until verified. [Ref: §28.3, ECH-5]

## 4. Normative Rules (KN-1..KN-6)

The following normative rules govern all knowledge categories:

| ID | Rule | Evidence |
|---|---|---|
| **KN-1** | Every recorded fact MUST carry provenance — a reference to the source evidence (file, trace, schema, commit) from which it was derived. A fact without provenance is non-authoritative. [Ref: §14.3] | PR-5; Chikofsky & Cross |
| **KN-2** | Decisions MUST be recorded in an immutable, append/supersede format (ADR). An accepted decision MUST NOT be silently edited; it is superseded by a new record. [Ref: §14.3] | Nygard, 2011 |
| **KN-3** | A hypothesis MUST be marked as a hypothesis until verified by evidence; it MUST NOT be recorded as a fact. [Ref: §14.3] | von Mayrhauser & Vans, 1995; Feathers |
| **KN-4** | Contracts and invariants are authoritative and changes to them MUST pass through governance + versioning (§17–§18). [Ref: §14.3] | PR-10 |
| **KN-5** | Knowledge MUST reside in the repository (PR-4), never solely in conversation, model memory, or tooling state. [Ref: §14.3] | PR-4 |
| **KN-6** | Triangulation: where feasible, a fact SHOULD be corroborated by more than one source class (static, dynamic, human) before being recorded as authoritative. [Ref: §14.3] | Demeyer et al., 2002 |

## 5. Knowledge Class Mapping (§31.2)

The following table maps each knowledge category to its corresponding Knowledge Class and Authority Class per §31.2 and §11.1:

| Knowledge Category | §14.2 Definition | Knowledge Class (§31.2) | Authority Class (§11.1) | Immutable |
|---|---|---|---|---|
| **Facts** | Verified statements with provenance | Verified Facts / Engineering Knowledge | Candidate-authoritative → Authoritative | No |
| **Decisions** | ADR-format, immutable once accepted | Design Decisions / Architecture Decisions | Authoritative | Yes (superseded, never edited) |
| **Contracts** | Agreed interfaces + semantics | Engineering Knowledge | Authoritative | No (governed change) |
| **Invariants** | Constraints that MUST remain true | Engineering Knowledge | Authoritative | No (governed change) |
| **Rationale** | Why a decision was made; alternatives | Engineering Knowledge | Authoritative | No |
| **Provenance** | Link from fact to source evidence | Engineering Knowledge | Authoritative | No |

### Knowledge Progression

Knowledge SHALL progress through the Evidence Chain per §31.2 and §28:

```
Observed Facts → Verified Facts → Engineering Knowledge
```

- **RKA-1**: Repository knowledge MUST be organized into the defined classes (§31.2), each with an authority class (§11) and, for facts, a confidence level (§26). [Ref: §31.3, RKA-1]
- **RKA-2**: Knowledge MUST progress Observed → Verified → Engineering Knowledge only via the Evidence Chain (§28). [Ref: §31.3, RKA-2]
- **RKA-5**: Authoritative knowledge MUST carry provenance (§28) and, where it is a fact, confidence (§26). [Ref: §31.3, RKA-5]

## 6. Completion Criteria

This schema document is complete when:

1. All six knowledge categories from §14.2 have defined schemas with mandatory fields. [Ref: §14.2]
2. Each schema carries mandatory artifact metadata per §11.2 (identifier, authority class, owner, version, status). [Ref: §11.2]
3. All six normative knowledge rules (KN-1..KN-6) are incorporated. [Ref: §14.3]
4. Each knowledge category is mapped to its §31.2 Knowledge Class and §11.1 Authority Class. [Ref: §31.2, §11.1]
5. The Evidence Chain rules (ECH-1..ECH-5) are mapped to the Provenance schema. [Ref: §28]
6. The Confidence Model (§26) is incorporated into the Facts and Provenance schemas. [Ref: §26]
7. The Decision Model (§35) is incorporated into the Decisions and Rationale schemas. [Ref: §35]
8. The schema does not introduce requirements, fields, or terminology not present in the SDD. [Ref: §11.4]
