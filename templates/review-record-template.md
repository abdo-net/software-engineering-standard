# Review Record Template

| Field | Value |
|---|---|
| **Artifact ID** | `[ARTIFACT_ID]` |
| **Artifact Type** | Review Record |
| **Authority Class** | Authoritative |
| **Owner** | `[OWNER_NAME]` |
| **Version** | `[VERSION]` |
| **Status** | `[STATUS]` |
| **Standard Version** | `[SES_VERSION]` |
| **Created** | `[DATE]` |

---

> **SDD Authority:** This template is derived from the Review Model (§15), specifically RV-5. [Ref: §15.2, RV-5]
>
> **Normative Basis:** RV-5 -- "Review outcomes (findings, disposition) MUST be recorded as evidence." [Ref: §15.2, RV-5]
> Every authoritative artifact MUST pass at least one review of an appropriate type per RV-1. [Ref: §15.2, RV-1]
> Changes to the standard itself MUST undergo Inspection per RV-2. [Ref: §15.2, RV-2]
> Review MUST be against explicit, written criteria per RV-3. [Ref: §15.2, RV-3]
> Review SHOULD be performed by someone other than the sole author per RV-4. [Ref: §15.2, RV-4]

---

## 1. Review Type

> Per §15.1: The SES adopts the review taxonomy of IEEE Std 1028-2008. [Ref: §15.1]

| Review Type | Selected | Rationale |
|---|---|---|
| **Inspection** | [ ] | Formal, rigorous defect detection against criteria |
| **Technical Review** | [ ] | Evaluate fitness for purpose by qualified reviewers |
| **Walkthrough** | [ ] | Author-led, educational, early feedback |
| **Audit** | [ ] | Independent conformance check against the standard |
| **Management Review** | [ ] | Status/decision review by authority |

**Selected Review Type:** `[REVIEW_TYPE]`

---

## 2. Target Artifact

| Field | Value |
|---|---|
| **Artifact Name** | `[ARTIFACT_NAME]` |
| **Artifact ID** | `[TARGET_ARTIFACT_ID]` |
| **Artifact Version Reviewed** | `[ARTIFACT_VERSION]` |
| **Artifact Authority Class** | Authoritative / Derived / Generated |
| **Artifact Location** | `[ARTIFACT_PATH]` |

---

## 3. Reviewer(s)

> Review SHOULD be performed by someone other than the sole author where independence adds value per RV-4. [Ref: §15.2, RV-4]

| Role | Name | Organization | Review Date |
|---|---|---|---|
| **Lead Reviewer** | `[NAME]` | `[ORG]` | `[DATE]` |
| **Reviewer 2** | `[NAME]` | `[ORG]` | `[DATE]` |
| **Reviewer 3** | `[NAME]` | `[ORG]` | `[DATE]` |
| **Author (if walkthrough)** | `[NAME]` | `[ORG]` | `[DATE]` |

---

## 4. Date

| Field | Value |
|---|---|
| **Review Start Date** | `[START_DATE]` |
| **Review End Date** | `[END_DATE]` |
| **Duration** | `[DURATION]` |

---

## 5. Criteria Used

> Review MUST be against explicit, written criteria (checklists/verification criteria) per RV-3. [Ref: §15.2, RV-3]

| Criteria Reference | Criteria Type | Description |
|---|---|---|
| `[CHECKLIST_ID]` | Checklist | `[DESCRIPTION]` |
| `[CRITERIA_ID]` | Verification Criteria | `[DESCRIPTION]` |
| `[STANDARD_SECTION]` | Standard Section | `[DESCRIPTION]` |

---

## 6. Findings

> Findings MUST be recorded as evidence per RV-5. [Ref: §15.2, RV-5]
> Findings MUST cite the specific criterion violated and the location within the target artifact. [Ref: §15.3]

| Finding ID | Severity | Criterion Violated | Location | Description | Evidence |
|---|---|---|---|---|---|
| `[F-1]` | Critical / Major / Minor / Info | `[CRITERION]` | `[LOCATION]` | `[DESCRIPTION]` | `[EVIDENCE]` |
| `[F-2]` | Critical / Major / Minor / Info | `[CRITERION]` | `[LOCATION]` | `[DESCRIPTION]` | `[EVIDENCE]` |
| `[F-3]` | Critical / Major / Minor / Info | `[CRITERION]` | `[LOCATION]` | `[DESCRIPTION]` | `[EVIDENCE]` |

### Severity Definitions

| Severity | Definition |
|---|---|
| **Critical** | Must be resolved before artifact can be accepted; blocks progression. |
| **Major** | Should be resolved before acceptance; may be conditionally accepted with documented risk. |
| **Minor** | Should be addressed; does not block acceptance. |
| **Info** | Observation or suggestion; informational only. |

---

## 7. Disposition

> Disposition records the resolution of each finding per RV-5. [Ref: §15.2, RV-5]

| Finding ID | Disposition | Rationale | Approved By | Date |
|---|---|---|---|---|
| `[F-1]` | Resolved / Deferred / Accepted / Rejected | `[RATIONALE]` | `[APPROVER]` | `[DATE]` |
| `[F-2]` | Resolved / Deferred / Accepted / Rejected | `[RATIONALE]` | `[APPROVER]` | `[DATE]` |
| `[F-3]` | Resolved / Deferred / Accepted / Rejected | `[RATIONALE]` | `[APPROVER]` | `[DATE]` |

### Disposition Definitions

| Disposition | Meaning |
|---|---|
| **Resolved** | Finding addressed; fix verified. |
| **Deferred** | Finding acknowledged; fix scheduled (must cite follow-up). |
| **Accepted** | Finding acknowledged; no fix planned (must cite risk acceptance). |
| **Rejected** | Finding is invalid or out of scope (must cite rationale). |

---

## 8. Follow-up Actions

| Action ID | Description | Owner | Due Date | Status | Evidence Reference |
|---|---|---|---|---|---|
| `[FA-1]` | `[ACTION]` | `[OWNER]` | `[DATE]` | Open / Closed | `[EVIDENCE]` |
| `[FA-2]` | `[ACTION]` | `[OWNER]` | `[DATE]` | Open / Closed | `[EVIDENCE]` |

---

## 9. Evidence References

> Review outcomes are recorded as evidence per RV-5. Every finding MUST be traceable to its source. [Ref: §15.2, RV-5; §28]

| Evidence ID | Type | Location | Description |
|---|---|---|---|
| `[EV-1]` | `[TYPE]` | `[LOCATION]` | `[DESCRIPTION]` |
| `[EV-2]` | `[TYPE]` | `[LOCATION]` | `[DESCRIPTION]` |

---

## 10. Review Verdict

| Field | Value |
|---|---|
| **Overall Verdict** | Pass / Fail / Conditional Pass |
| **Artifact Accepted** | Yes / No / Conditionally |
| **Conditions (if any)** | `[CONDITIONS]` |
| **Next Review Required** | Yes / No |
| **Next Review Type** | `[NEXT_REVIEW_TYPE]` |
| **Review Lead Signature** | `[SIGNATURE]` |
| **Date of Verdict** | `[DATE]` |

---

## 11. Traceability

| Trace Link | Reference |
|---|---|
| **Target Artifact** | `[ARTIFACT_ID]` |
| **Checklist / Criteria Used** | `[CHECKLIST_ID]` |
| **Related Mission** | `[MISSION_ID]` |
| **Authorizing Decision(s)** | `[DECISION_ID]` |
| **Follow-up Review Record** | `[FOLLOW_UP_REVIEW_ID]` |
| **Repository Location** | `[FILE_PATH]` |

---

> **Placeholder count:** 22 distinct `[PLACEHOLDER]` fields.
