# Checklist Template

| Field | Value |
|---|---|
| **Artifact ID** | `[ARTIFACT_ID]` |
| **Artifact Type** | Checklist |
| **Authority Class** | Derived |
| **Owner** | `[OWNER_NAME]` |
| **Version** | `[VERSION]` |
| **Status** | `[STATUS]` |
| **Standard Version** | `[SES_VERSION]` |
| **Created** | `[DATE]` |
| **Derived From** | `[SOURCE_STANDARD_SECTION]` |

---

> **SDD Authority:** This template is derived from the Review Model (§15). [Ref: §15.3]
>
> **Normative Basis:** RV-3 -- "Review MUST be against explicit, written criteria (checklists/verification criteria), not reviewer preference." [Ref: §15.3, RV-3]
>
> **Checklist Classification:** Checklists are Derived artifacts per §11.1; they MUST NOT be hand-edited in isolation from their authoritative source and MUST be regenerable per RA-4. [Ref: §11.1, RA-4]

---

## 1. Checklist Identification

| Field | Value |
|---|---|
| **Checklist Name** | `[CHECKLIST_NAME]` |
| **Target Review Type** | `[REVIEW_TYPE]` |
| **Applicable Stage(s)** | `[STAGE_ID(s)]` |
| **Target Artifact Type(s)** | `[ARTIFACT_TYPE(s)]` |

### Review Type Selection (§15.1)

> Select exactly one review type per §15.1. The SES adopts the review taxonomy of IEEE Std 1028-2008. [Ref: §15.1]

| Review Type | Selected | Purpose (per §15.1) |
|---|---|---|
| **Inspection** | [ ] | Formal, rigorous defect detection against criteria |
| **Technical Review** | [ ] | Evaluate fitness for purpose by qualified reviewers |
| **Walkthrough** | [ ] | Author-led, educational, early feedback |
| **Audit** | [ ] | Independent conformance check against the standard |
| **Management Review** | [ ] | Status/decision review by authority |

---

## 2. Checklist Items

> Checklist items MUST be explicit, written criteria per RV-3. [Ref: §15.3, RV-3]
> Items SHOULD reference specific SDD sections or requirement IDs for traceability. [Ref: §29]

| Item ID | Criterion / Checklist Item | SDD Reference | Status | Notes |
|---|---|---|---|---|
| `[CI-1]` | `[CRITERION_1]` | `[REF]` | Pass / Fail / N/A | `[NOTES]` |
| `[CI-2]` | `[CRITERION_2]` | `[REF]` | Pass / Fail / N/A | `[NOTES]` |
| `[CI-3]` | `[CRITERION_3]` | `[REF]` | Pass / Fail / N/A | `[NOTES]` |
| `[CI-4]` | `[CRITERION_4]` | `[REF]` | Pass / Fail / N/A | `[NOTES]` |
| `[CI-5]` | `[CRITERION_5]` | `[REF]` | Pass / Fail / N/A | `[NOTES]` |
| `[CI-6]` | `[CRITERION_6]` | `[REF]` | Pass / Fail / N/A | `[NOTES]` |
| `[CI-7]` | `[CRITERION_7]` | `[REF]` | Pass / Fail / N/A | `[NOTES]` |
| `[CI-8]` | `[CRITERION_8]` | `[REF]` | Pass / Fail / N/A | `[NOTES]` |

> Add or remove rows as needed. Each checklist MUST be instantiated with criteria relevant to its target artifact and review type.

---

## 3. Findings

> Findings are recorded evidence of review outcomes per RV-5. [Ref: §15.2, RV-5]

| Finding ID | Related Item | Severity | Description | Location |
|---|---|---|---|---|
| `[F-1]` | `[CI-REF]` | Critical / Major / Minor / Info | `[DESCRIPTION]` | `[LOCATION]` |
| `[F-2]` | `[CI-REF]` | Critical / Major / Minor / Info | `[DESCRIPTION]` | `[LOCATION]` |
| `[F-3]` | `[CI-REF]` | Critical / Major / Minor / Info | `[DESCRIPTION]` | `[LOCATION]` |

---

## 4. Disposition

> Disposition records the resolution decision for each finding per RV-5. [Ref: §15.2, RV-5]

| Finding ID | Disposition | Rationale | Approved By | Date |
|---|---|---|---|---|
| `[F-1]` | Resolved / Deferred / Accepted / Rejected | `[RATIONALE]` | `[APPROVER]` | `[DATE]` |
| `[F-2]` | Resolved / Deferred / Accepted / Rejected | `[RATIONALE]` | `[APPROVER]` | `[DATE]` |
| `[F-3]` | Resolved / Deferred / Accepted / Rejected | `[RATIONALE]` | `[APPROVER]` | `[DATE]` |

### Disposition Definitions

| Disposition | Meaning |
|---|---|
| **Resolved** | Finding addressed; fix verified. |
| **Deferred** | Finding acknowledged; fix scheduled for later (must cite follow-up). |
| **Accepted** | Finding acknowledged; no fix planned (must cite risk acceptance rationale). |
| **Rejected** | Finding is invalid or out of scope (must cite rationale). |

---

## 5. Reviewer Section

> Review SHOULD be performed by someone other than the sole author where independence adds value per RV-4. [Ref: §15.2, RV-4]
> Review outcomes MUST be recorded as evidence per RV-5. [Ref: §15.2, RV-5]

### 5.1 Reviewer(s)

| Role | Name | Date | Signature / Acknowledgment |
|---|---|---|---|
| **Lead Reviewer** | `[NAME]` | `[DATE]` | `[ACK]` |
| **Reviewer 2** | `[NAME]` | `[DATE]` | `[ACK]` |
| **Reviewer 3** | `[NAME]` | `[DATE]` | `[ACK]` |

### 5.2 Review Summary

| Field | Value |
|---|---|
| **Target Artifact** | `[ARTIFACT_NAME]` |
| **Artifact Version** | `[ARTIFACT_VERSION]` |
| **Review Date** | `[DATE]` |
| **Total Items** | `[COUNT]` |
| **Items Passed** | `[COUNT]` |
| **Items Failed** | `[COUNT]` |
| **Items N/A** | `[COUNT]` |
| **Overall Verdict** | Pass / Fail / Conditional Pass |

### 5.3 Follow-up Actions

| Action ID | Description | Owner | Due Date | Status |
|---|---|---|---|---|
| `[FA-1]` | `[ACTION]` | `[OWNER]` | `[DATE]` | Open / Closed |
| `[FA-2]` | `[ACTION]` | `[OWNER]` | `[DATE]` | Open / Closed |

---

## 6. Evidence and Traceability

| Field | Value |
|---|---|
| **Review Record Reference** | `[REVIEW_RECORD_ID]` |
| **Related Review Type** | `[REVIEW_TYPE]` |
| **Standard Version** | `[SES_VERSION]` |
| **Repository Location** | `[FILE_PATH]` |

---

> **Placeholder count:** 20 distinct `[PLACEHOLDER]` fields.
