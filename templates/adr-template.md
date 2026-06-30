# Architecture Decision Record (ADR) Template

---

## Artifact Metadata

| Field | Value |
|---|---|
| **Artifact ID** | [ADR_ID] |
| **Artifact Type** | Architecture Decision Record (ADR) [Ref: §11.3] |
| **Authority Class** | Authoritative [Ref: §11.1] |
| **Object Type** | Decision [Ref: §42.2] |
| **Owner** | [OWNER] [Ref: §11.2] |
| **Version** | [VERSION] [Ref: §18] |
| **Status** | [STATUS] [Ref: §11.2] |
| **Immutability Rule** | This artifact SHALL NOT be modified once Accepted; it MAY only be superseded by a new ADR [Ref: KN-2, §11.3] |
| **Superseded By** | [SUPERSEDED_BY_ADR_ID_OR_NONE] [Ref: §35.2] |
| **Created Timestamp** | [TIMESTAMP] [Ref: §26.3] |
| **Decision References** | [DECISION_REFERENCE] [Ref: §43.2] |

---

## 1. Decision

> Field definition per §35.2: The recorded engineering choice.
> Normative rule: DEC-1: Every engineering decision MUST be recorded with all nine fields [Ref: §35.2, DEC-1].

**Decision Statement:** [DECISION_STATEMENT]

**Decision Identifier:** [DECISION_ID]

---

## 2. Decision Context

> Field definition per §35.2: The circumstances, constraints, and problem that necessitated this decision.

**Problem Statement:** [PROBLEM_STATEMENT]

**Context:** [CONTEXT_DESCRIPTION]

**Forces / Constraints:** [FORCES_AND_CONSTRAINTS]

**Date of Decision:** [DECISION_DATE]

---

## 3. Alternatives

> Field definition per §35.2: The options considered before reaching this decision.

| Alternative ID | Description | Pros | Cons |
|---|---|---|---|
| [ALT_1_ID] | [ALT_1_DESCRIPTION] | [ALT_1_PROS] | [ALT_1_CONS] |
| [ALT_2_ID] | [ALT_2_DESCRIPTION] | [ALT_2_PROS] | [ALT_2_CONS] |
| [ALT_N_ID] | [ALT_N_DESCRIPTION] | [ALT_N_PROS] | [ALT_N_CONS] |

**Rejected Alternatives:** [REJECTED_ALTERNATIVES_WITH_REASONING]

---

## 4. Evidence

> Field definition per §35.2: The evidence justifying the decision.
> Normative rule: DEC-2: A Decision MUST cite the Evidence (§26/§28) and the Impact Analysis (§36) that justify it [Ref: §35.2, DEC-2].

| Evidence ID | Description | Confidence Level (A-E) [Ref: §26.2] | Evidence Source [Ref: §26.3] |
|---|---|---|---|
| [EV_1_ID] | [EV_1_DESCRIPTION] | [EV_1_CONFIDENCE] | [EV_1_SOURCE] |
| [EV_2_ID] | [EV_2_DESCRIPTION] | [EV_2_CONFIDENCE] | [EV_2_SOURCE] |
| [EV_N_ID] | [EV_N_DESCRIPTION] | [EV_N_CONFIDENCE] | [EV_N_SOURCE] |

**Evidence Source:** [EVIDENCE_SOURCE] [Ref: §26.3]

**Verification Status:** [VERIFICATION_STATUS] [Ref: §26.3]

---

## 5. Impact

> Field definition per §35.2: The consequences of the decision across the system.
> Normative rule: DEC-2: A Decision MUST cite the Evidence and the Impact Analysis that justify it [Ref: §35.2, DEC-2].

| Impact Area | Impact Description | Severity |
|---|---|---|
| Architecture | [ARCH_IMPACT] | [ARCH_SEVERITY] |
| Contracts | [CONTRACT_IMPACT] | [CONTRACT_SEVERITY] |
| Dependencies | [DEPENDENCY_IMPACT] | [DEPENDENCY_SEVERITY] |
| Execution Flow | [EXECUTION_IMPACT] | [EXECUTION_SEVERITY] |
| Database | [DATABASE_IMPACT] | [DATABASE_SEVERITY] |
| API | [API_IMPACT] | [API_SEVERITY] |
| Security | [SECURITY_IMPACT] | [SECURITY_SEVERITY] |
| Tests | [TEST_IMPACT] | [TEST_SEVERITY] |
| Documentation | [DOC_IMPACT] | [DOC_SEVERITY] |
| Deployment | [DEPLOYMENT_IMPACT] | [DEPLOYMENT_SEVERITY] |
| Validation | [VALIDATION_IMPACT] | [VALIDATION_SEVERITY] |

**Impact Analysis Reference:** [IMPACT_ANALYSIS_ID] [Ref: §36]

---

## 6. Dependencies

> Field definition per §35.2: Dependencies of this decision on other decisions, artifacts, or system elements.

| Dependency Type | Dependency ID | Description |
|---|---|---|
| Depends on Decision | [DEP_DECISION_ID] | [DEP_DECISION_DESC] |
| Depends on Contract | [DEP_CONTRACT_ID] | [DEP_CONTRACT_DESC] |
| Depends on Invariant | [DEP_INVARIANT_ID] | [DEP_INVARIANT_DESC] |
| Depends on Requirement | [DEP_REQUIREMENT_ID] | [DEP_REQUIREMENT_DESC] |

**Traceability Links:** [TRACEABILITY_LINKS] [Ref: §48]

---

## 7. Approval

> Field definition per §35.2: The approval status and approvers of this decision.

| Role | Approver | Approval Date | Signature / Commit Reference |
|---|---|---|---|
| Standard Authority | [AUTHORITY_NAME] | [AUTHORITY_DATE] | [AUTHORITY_REF] |
| Technical Reviewer | [REVIEWER_NAME] | [REVIEWER_DATE] | [REVIEWER_REF] |

**Review Record Reference:** [REVIEW_RECORD_ID] [Ref: §15]

**Approval Status:** [APPROVAL_STATUS]

---

## 8. Status

> Field definition per §35.2: The lifecycle state of this decision.

**Current Status:** [CURRENT_STATUS]

Allowed values per §43.2 (Status field): Draft / Accepted / Superseded / Deprecated

**Status History:**

| Status | Date | Changed By | Reason |
|---|---|---|---|
| Previous | [PREV_STATUS_DATE] | [PREV_STATUS_CHANGED_BY] | [PREV_STATUS_REASON] |
| Current | [CURRENT_STATUS_DATE] | [CURRENT_STATUS_CHANGED_BY] | [CURRENT_STATUS_REASON] |

---

## 9. Superseded By

> Field definition per §35.2: The identifier of the decision that supersedes this one, if applicable.
> Normative rule: DEC-3: A Decision is immutable once Approved; change occurs only by a new Decision setting Superseded By [Ref: §35.2, DEC-3].
> Normative rule: DEC-5: Architecture Decisions are the ADR subtype and inherit these rules [Ref: §35.2, DEC-5].

**Superseded By ADR:** [SUPERSEDING_ADR_ID_OR_NONE]

**Superseded Date:** [SUPERSEDED_DATE_OR_NONE]

**Superseding Rationale:** [SUPERSEDING_RATIONALE_OR_NONE]

---

## Immutability Notice

> This ADR is **immutable once Accepted** per §11.3 and KN-2 [Ref: §11.3, KN-2].
> If the decision needs to change, a NEW ADR SHALL be created, and this record SHALL be updated in field 9 (Superseded By) only.
> The original content of this record SHALL NOT be altered, deleted, or rewritten [Ref: KN-2].
> Superseded decisions MUST be retained as Historical knowledge and MUST NOT be deleted [Ref: RKA-3, §31.3].
