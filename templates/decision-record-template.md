# Decision Record Template

---

## Artifact Metadata

| Field | Value |
|---|---|
| **Artifact ID** | [DECISION_ID] |
| **Artifact Type** | Decision Record [Ref: §35.2] |
| **Authority Class** | Authoritative [Ref: §11.1] |
| **Object Type** | Decision [Ref: §42.2] |
| **Owner** | [OWNER] [Ref: §11.2] |
| **Version** | [VERSION] [Ref: §18] |
| **Status** | [STATUS] [Ref: §11.2] |
| **Immutability Rule** | This artifact SHALL NOT be modified once Approved; it MAY only be superseded by a new Decision Record [Ref: DEC-3, §35.3] |
| **Superseded By** | [SUPERSEDED_BY_DECISION_ID_OR_NONE] [Ref: §35.2] |
| **Created Timestamp** | [TIMESTAMP] [Ref: §26.3] |
| **Decision References** | [DECISION_REFERENCE] [Ref: §43.2] |

---

## Applicable Normative Rules

> The following rules from §35.3 SHALL govern all decision records [Ref: §35.3].

| Rule ID | Rule Statement | Status |
|---|---|---|
| **DEC-1** | Every engineering decision MUST be recorded with all nine fields (§35.2) [Ref: DEC-1, §35.3] | [DEC_1_STATUS] |
| **DEC-2** | A Decision MUST cite the Evidence (§26/§28) and the Impact Analysis (§36) that justify it [Ref: DEC-2, §35.3] | [DEC_2_STATUS] |
| **DEC-3** | A Decision is immutable once Approved; change occurs only by a new Decision setting Superseded By [Ref: DEC-3, §35.3] | [DEC_3_STATUS] |
| **DEC-4** | Every Implementation MUST trace back to exactly one engineering Decision [Ref: DEC-4, §35.3] | [DEC_4_STATUS] |
| **DEC-5** | Architecture Decisions are the ADR subtype (§11.3) and inherit these rules [Ref: DEC-5, §35.3] | [DEC_5_STATUS] |

---

## 1. Decision

> Field definition per §35.2: The recorded engineering choice.
> Normative rule: DEC-1: Every engineering decision MUST be recorded with all nine fields [Ref: §35.2, DEC-1].
> Normative rule: DEC-4: Every Implementation MUST trace back to exactly one engineering Decision [Ref: §35.2, DEC-4].

**Decision Statement:** [DECISION_STATEMENT]

**Decision Identifier:** [DECISION_ID]

**Decision Category:** [DECISION_CATEGORY]

Allowed values: Architecture / Design / Technology / Process / Organizational / Tooling / Security / Other

**Decision Subtype Reference:** [DECISION_SUBTYPE]

> Note: If this is an Architecture Decision, use the ADR template (adr-template.md) per DEC-5 [Ref: DEC-5, §35.3].

---

## 2. Decision Context

> Field definition per §35.2: The circumstances, constraints, and problem that necessitated this decision.

**Problem Statement:** [PROBLEM_STATEMENT]

**Context:** [CONTEXT_DESCRIPTION]

**Forces / Constraints:** [FORCES_AND_CONSTRAINTS]

**Mission Reference:** [MISSION_REFERENCE] [Ref: §32]

**State Reference:** [STATE_REFERENCE] [Ref: §33]

**Stage Reference:** [STAGE_REFERENCE] [Ref: §13]

**Date of Decision:** [DECISION_DATE]

---

## 3. Alternatives

> Field definition per §35.2: The options considered before reaching this decision.

| Alternative ID | Description | Pros | Cons | Confidence Level |
|---|---|---|---|---|
| [ALT_1_ID] | [ALT_1_DESCRIPTION] | [ALT_1_PROS] | [ALT_1_CONS] | [ALT_1_CONFIDENCE] |
| [ALT_2_ID] | [ALT_2_DESCRIPTION] | [ALT_2_PROS] | [ALT_2_CONS] | [ALT_2_CONFIDENCE] |
| [ALT_N_ID] | [ALT_N_DESCRIPTION] | [ALT_N_PROS] | [ALT_N_CONS] | [ALT_N_CONFIDENCE] |

**Rejected Alternatives:** [REJECTED_ALTERNATIVES_WITH_REASONING]

**Context-Binding Rationale:** [CONTEXT_BINDING]

> Per PR-12, where the evidence base shows multiple valid approaches, the SES presents them and binds the choice to context [Ref: PR-12, §7].

---

## 4. Evidence

> Field definition per §35.2: The evidence justifying the decision.
> Normative rule: DEC-2: A Decision MUST cite the Evidence (§26/§28) and the Impact Analysis (§36) that justify it [Ref: §35.2, DEC-2].

| Evidence ID | Description | Confidence Level (A-E) [Ref: §26.2] | Evidence Source [Ref: §26.3] | Verification Status |
|---|---|---|---|---|
| [EV_1_ID] | [EV_1_DESCRIPTION] | [EV_1_CONFIDENCE] | [EV_1_SOURCE] | [EV_1_VERIFY_STATUS] |
| [EV_2_ID] | [EV_2_DESCRIPTION] | [EV_2_CONFIDENCE] | [EV_2_SOURCE] | [EV_2_VERIFY_STATUS] |
| [EV_N_ID] | [EV_N_DESCRIPTION] | [EV_N_CONFIDENCE] | [EV_N_SOURCE] | [EV_N_VERIFY_STATUS] |

**Evidence Source:** [EVIDENCE_SOURCE] [Ref: §26.3]

**Verification Status:** [VERIFICATION_STATUS] [Ref: §26.3]

**Provenance Record Reference:** [PROVENANCE_RECORD_ID] [Ref: §26.3]

**Hypothesis Marking:** [HYPOTHESIS_MARKING]

> Normative rule: KN-3: A hypothesis MUST be marked as a hypothesis until verified by evidence; it MUST NOT be recorded as a fact [Ref: KN-3, §14.3].

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

**Impact Analysis ID:** [IMPACT_ANALYSIS_ID] [Ref: §36]

**Impact Propagation Path:** [IMPACT_PROPAGATION_PATH] [Ref: §36.2]

---

## 6. Dependencies

> Field definition per §35.2: Dependencies of this decision on other decisions, artifacts, or system elements.

| Dependency Type | Dependency ID | Description |
|---|---|---|
| Depends on Decision | [DEP_DECISION_ID] | [DEP_DECISION_DESC] |
| Depends on Contract | [DEP_CONTRACT_ID] | [DEP_CONTRACT_DESC] |
| Depends on Invariant | [DEP_INVARIANT_ID] | [DEP_INVARIANT_DESC] |
| Depends on Requirement | [DEP_REQUIREMENT_ID] | [DEP_REQUIREMENT_DESC] |
| Depends on Fact | [DEP_FACT_ID] | [DEP_FACT_DESC] |

**Traceability Links:** [TRACEABILITY_LINKS] [Ref: §48]

**Dependency Graph Reference:** [DEPENDENCY_GRAPH_ID] [Ref: §45]

---

## 7. Approval

> Field definition per §35.2: The approval status and approvers of this decision.

| Role | Approver | Approval Date | Signature / Commit Reference |
|---|---|---|---|
| Standard Authority | [AUTHORITY_NAME] | [AUTHORITY_DATE] | [AUTHORITY_REF] |
| Technical Reviewer | [REVIEWER_NAME] | [REVIEWER_DATE] | [REVIEWER_REF] |

**Review Type:** [REVIEW_TYPE]

Allowed values per §15.1: Inspection / Technical Review / Walkthrough / Audit / Management Review

**Review Record Reference:** [REVIEW_RECORD_ID] [Ref: §15]

**Approval Status:** [APPROVAL_STATUS]

**Governance Reference:** [GOVERNANCE_REFERENCE] [Ref: §17]

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

**Lifecycle State:** [LIFECYCLE_STATE] [Ref: §33]

---

## 9. Superseded By

> Field definition per §35.2: The identifier of the decision that supersedes this one, if applicable.
> Normative rule: DEC-3: A Decision is immutable once Approved; change occurs only by a new Decision setting Superseded By [Ref: §35.2, DEC-3].

**Superseded By Decision:** [SUPERSEDING_DECISION_ID_OR_NONE]

**Superseded Date:** [SUPERSEDED_DATE_OR_NONE]

**Superseding Rationale:** [SUPERSEDING_RATIONALE_OR_NONE]

**Superseding Decision Evidence:** [SUPERSEDING_DECISION_EVIDENCE]

> Superseded decisions MUST be retained as Historical knowledge and MUST NOT be deleted [Ref: RKA-3, §31.3].

---

## Implementation Trace

> Normative rule: DEC-4: Every Implementation MUST trace back to exactly one engineering Decision [Ref: DEC-4, §35.3].

| Implementation ID | Description | Traceability Link | Validation Status |
|---|---|---|---|
| [IMPL_1_ID] | [IMPL_1_DESC] | [IMPL_1_TRACE] | [IMPL_1_VALIDATION] |
| [IMPL_2_ID] | [IMPL_2_DESC] | [IMPL_2_TRACE] | [IMPL_2_VALIDATION] |
| [IMPL_N_ID] | [IMPL_N_DESC] | [IMPL_N_TRACE] | [IMPL_N_VALIDATION] |

---

## Immutability Notice

> This Decision Record is **immutable once Approved** per DEC-3 [Ref: §35.3].
> If the decision needs to change, a NEW Decision Record SHALL be created, and this record SHALL be updated in field 9 (Superseded By) only.
> The original content of this record SHALL NOT be altered, deleted, or rewritten [Ref: DEC-3, KN-2].
> Superseded decisions MUST be retained as Historical knowledge and MUST NOT be deleted [Ref: RKA-3, §31.3].
> Per DEC-5, if this is an Architecture Decision, the ADR template (adr-template.md) SHALL be used [Ref: DEC-5, §35.3].
