# Design Document Template

| Field | Value |
|---|---|
| **Artifact ID** | `[ARTIFACT_ID]` |
| **Artifact Type** | Design Document |
| **Authority Class** | Authoritative |
| **Owner** | `[OWNER_NAME]` |
| **Version** | `[VERSION]` |
| **Status** | Draft / Accepted / Superseded / Deprecated |
| **Standard Version** | `[SES_VERSION]` |
| **Created** | `[DATE]` |

---

> **SDD Authority:** This template is derived from the Engineering Lifecycle Planning phase (§12), the Engineering Decision Model (§35), and the Engineering Impact Analysis Model (§36). [Ref: §12.2, §35, §36]
>
> **Related Models:** Engineering State Model (§33); Engineering Documentation Model (§38); Engineering Traceability Expansion (§29). [Ref: §33, §38, §29]

---

## 1. Purpose

[PLACEHOLDER: State the purpose of this design document. What problem does it solve? Why is it being created?]

---

## 2. Scope

[PLACEHOLDER: Define what this design document covers and what it explicitly does NOT cover. Scope boundaries MUST be clear per §4.3.]

---

## 3. Context

### 3.1 Decision Context

[PLACEHOLDER: Describe the engineering context in which this design was created. What decisions led to this point? What constraints apply?]

### 3.2 Related Decisions

| Decision ID | Title | Status | Link |
|---|---|---|---|
| `[DEC-1]` | `[DECISION_TITLE]` | Approved / Pending | `[LINK]` |
| `[DEC-2]` | `[DECISION_TITLE]` | Approved / Pending | `[LINK]` |

---

## 4. Architecture

### 4.1 Architecture Overview

[PLACEHOLDER: Provide the high-level architecture this design document describes. Include component diagrams, data flow, or structural descriptions as appropriate.]

### 4.2 Component Design

| Component | Responsibility | Interface | Dependencies |
|---|---|---|---|
| `[COMPONENT_1]` | `[RESPONSIBILITY]` | `[INTERFACE]` | `[DEPS]` |
| `[COMPONENT_2]` | `[RESPONSIBILITY]` | `[INTERFACE]` | `[DEPS]` |

### 4.3 Data Design

[PLACEHOLDER: Describe data models, schemas, storage decisions, and data flow.]

---

## 5. Decisions

> Every engineering decision MUST be recorded with all nine fields per DEC-1. [Ref: §35.3, DEC-1]
> A Decision MUST cite the Evidence (§26/§28) and the Impact Analysis (§36) per DEC-2. [Ref: §35.3, DEC-2]
> A Decision is immutable once Approved; change occurs only by superseding per DEC-3. [Ref: §35.3, DEC-3]
> Every Implementation MUST trace back to exactly one engineering Decision per DEC-4. [Ref: §35.3, DEC-4]

### 5.1 Architecture Decision Records (ADRs)

| ADR ID | Title | Status | Supersedes |
|---|---|---|---|
| `[ADR-1]` | `[ADR_TITLE]` | Proposed / Approved / Rejected / Superseded | `[PRIOR_ADR]` |
| `[ADR-2]` | `[ADR_TITLE]` | Proposed / Approved / Rejected / Superseded | `[PRIOR_ADR]` |

### 5.2 Decision Detail

#### [ADR-1]: [ADR_TITLE]

| Field | Value |
|---|---|
| **Decision** | `[DECISION_STATEMENT]` |
| **Decision Context** | `[CONTEXT]` |
| **Alternatives** | `[ALTERNATIVES_CONSIDERED]` |
| **Evidence** | `[EVIDENCE_REFERENCE]` |
| **Impact** | `[IMPACT_ANALYSIS_REF]` |
| **Dependencies** | `[DEPENDENCIES]` |
| **Approval** | `[APPROVED_BY]` |
| **Status** | `[STATUS]` |
| **Superseded By** | `[SUPERSEDING_ADR]` |

---

## 6. Risk Analysis

> Risk analysis references the Risk Model (§21). [Ref: §21]

| Risk ID | Risk | Likelihood | Impact | Mitigation | Owner |
|---|---|---|---|---|---|
| `[RK-1]` | `[RISK_DESCRIPTION]` | High / Med / Low | High / Med / Low | `[MITIGATION]` | `[OWNER]` |
| `[RK-2]` | `[RISK_DESCRIPTION]` | High / Med / Low | High / Med / Low | `[MITIGATION]` | `[OWNER]` |

---

## 7. Impact Analysis

> Every Implementation MUST begin with an impact analysis spanning all dimensions per IMP-1. [Ref: §36.3, IMP-1]
> Impact analysis MUST use the dependency view and traceability per IMP-2. [Ref: §36.3, IMP-2]
> Identified impacts MUST be recorded as evidence and MUST feed the authorizing Decision per IMP-3. [Ref: §36.3, IMP-3]
> A change whose impact cannot be determined MUST be treated as high-risk per IMP-4. [Ref: §36.3, IMP-4]
> Impact analysis MUST precede the IMPLEMENTING state per IMP-5. [Ref: §36.3, IMP-5]

### 7.1 Impact Propagation Analysis

| Dimension | Affected? | Impact Description | Mitigation |
|---|---|---|---|
| **Affected Components** | [ ] | `[IMPACT_DESC]` | `[MITIGATION]` |
| **Dependencies** | [ ] | `[IMPACT_DESC]` | `[MITIGATION]` |
| **Execution Flow** | [ ] | `[IMPACT_DESC]` | `[MITIGATION]` |
| **Database** | [ ] | `[IMPACT_DESC]` | `[MITIGATION]` |
| **API** | [ ] | `[IMPACT_DESC]` | `[MITIGATION]` |
| **Security** | [ ] | `[IMPACT_DESC]` | `[MITIGATION]` |
| **Tests** | [ ] | `[IMPACT_DESC]` | `[MITIGATION]` |
| **Documentation** | [ ] | `[IMPACT_DESC]` | `[MITIGATION]` |
| **Deployment** | [ ] | `[IMPACT_DESC]` | `[MITIGATION]` |
| **Validation** | [ ] | `[IMPACT_DESC]` | `[MITIGATION]` |

### 7.2 Impact Summary

[PLACEHOLDER: Summarize the overall impact of the proposed changes. High-impact changes MUST have explicit Mission authorization per IMP-4.] [Ref: §36.3, IMP-4]

---

## 8. Dependencies

### 8.1 External Dependencies

| Dependency | Version / Constraint | Purpose | Risk if Unavailable |
|---|---|---|---|
| `[DEP-1]` | `[VERSION]` | `[PURPOSE]` | `[RISK]` |
| `[DEP-2]` | `[VERSION]` | `[PURPOSE]` | `[RISK]` |

### 8.2 Internal Dependencies

| Dependency | Satisfied By | Status |
|---|---|---|
| `[INTDEP-1]` | `[ARTIFACT_REF]` | Satisfied / Pending |
| `[INTDEP-2]` | `[ARTIFACT_REF]` | Satisfied / Pending |

---

## 9. Validation Approach

> Validation references the Validation Model (§16). [Ref: §16]
> Every requirement class MUST have a defined verification method per VL-2 (Inspection, Analysis, Demonstration, Test). [Ref: §16.4, VL-2]

| Validation Item | Method | Criteria | Evidence Location |
|---|---|---|---|
| `[VAL-1]` | Inspection / Analysis / Demonstration / Test | `[CRITERIA]` | `[LOCATION]` |
| `[VAL-2]` | Inspection / Analysis / Demonstration / Test | `[CRITERIA]` | `[LOCATION]` |

---

## 10. Sequencing

| Order | Activity | Depends On | Produces |
|---|---|---|---|
| 1 | `[ACTIVITY_1]` | `[DEP]` | `[OUTPUT]` |
| 2 | `[ACTIVITY_2]` | `[DEP]` | `[OUTPUT]` |
| 3 | `[ACTIVITY_3]` | `[DEP]` | `[OUTPUT]` |

---

## 11. Traceability

| Trace Link | Reference |
|---|---|
| **Parent Mission** | `[MISSION_ID]` |
| **Authorizing Decision(s)** | `[DECISION_ID]` |
| **Related ADRs** | `[ADR_IDS]` |
| **Impact Analysis** | `[IMPACT_ID]` |
| **Review Record** | `[REVIEW_ID]` |
| **Repository Location** | `[FILE_PATH]` |

---

> **Placeholder count:** 25 distinct `[PLACEHOLDER]` fields.
