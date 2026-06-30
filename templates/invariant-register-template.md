# Invariant Register Template

---

## Artifact Metadata

| Field | Value |
|---|---|
| **Artifact ID** | [INVARIANT_REGISTER_ID] |
| **Artifact Type** | Invariant Register [Ref: §11.3] |
| **Authority Class** | Authoritative [Ref: §11.1] |
| **Object Type** | Artifact (Knowledge — Invariant) [Ref: §42.2, §14.2] |
| **Owner** | [OWNER] [Ref: §11.2] |
| **Version** | [VERSION] [Ref: §18] |
| **Status** | [STATUS] [Ref: §11.2] |
| **Immutability Rule** | Changes to invariants MUST pass through governance and versioning per KN-4 [Ref: KN-4] |
| **Created Timestamp** | [TIMESTAMP] [Ref: §26.3] |
| **Decision References** | [DECISION_REFERENCE] [Ref: §43.2] |

---

## 1. Invariant Identity

> Field definition per §11.3: Invariant Register — the constraints that MUST remain true [Ref: §11.3].
> Authority per §40.1: These are constitutional integrity rules; violation renders work non-conformant [Ref: §40.2].

**Invariant Identifier:** [INVARIANT_ID]

**Invariant Type:** [INVARIANT_TYPE]

Allowed values per §40.1 classification: Structural / Behavioral / Data / Security / Configuration / Dependency / API / Documentation / Process / Other

**Priority:** [PRIORITY]

Allowed values: Critical / High / Medium / Low

**Date Created:** [DATE_CREATED]

**Date Last Verified:** [DATE_LAST_VERIFIED]

---

## 2. Description

> Field definition per §40.1: Each invariant defines a "no undocumented X" completeness rule [Ref: §40.1].

**Invariant Statement:** [INVARIANT_STATEMENT]

**Formal Specification:** [FORMAL_SPECIFICATION]

**Natural Language Description:** [DESCRIPTION]

**Rationale:** [RATIONALE]

**Related Integrity Rules (INT-1..INT-10):** [RELATED_INT_RULES]

| INT Rule | Relationship | Notes |
|---|---|---|
| INT-1 (No undocumented implementation) | [INT_1_REL] | [INT_1_NOTES] |
| INT-2 (No undocumented decision) | [INT_2_REL] | [INT_2_NOTES] |
| INT-3 (No undocumented dependency) | [INT_3_REL] | [INT_3_NOTES] |
| INT-4 (No undocumented API) | [INT_4_REL] | [INT_4_NOTES] |
| INT-5 (No undocumented database object) | [INT_5_REL] | [INT_5_NOTES] |
| INT-6 (No undocumented configuration) | [INT_6_REL] | [INT_6_NOTES] |
| INT-7 (No undocumented workflow) | [INT_7_REL] | [INT_7_NOTES] |
| INT-8 (No undocumented security rule) | [INT_8_REL] | [INT_8_NOTES] |
| INT-9 (No undocumented assumption) | [INT_9_REL] | [INT_9_NOTES] |
| INT-10 (No undocumented evidence) | [INT_10_REL] | [INT_10_NOTES] |

---

## 3. Scope

> Field definition per §40.1: Each invariant applies to a defined scope within the system [Ref: §40.1].

**Scope Type:** [SCOPE_TYPE]

Allowed values: System-wide / Subsystem / Module / Component / API / Database / Configuration / Security Boundary / Process / Other

**Scope Description:** [SCOPE_DESCRIPTION]

**Affected Components:** [AFFECTED_COMPONENTS]

**Affected Contracts:** [AFFECTED_CONTRACT_IDS]

**Affected Decisions:** [AFFECTED_DECISION_IDS]

**Boundary Crossed:** [BOUNDARY_CROSSED]

---

## 4. Enforcement Mechanism

> Field definition per §40.2: INT rules MAY be waived only through governance; otherwise they MUST be enforced [Ref: §40.2].

**Enforcement Type:** [ENFORCEMENT_TYPE]

Allowed values: Automated / Manual / Hybrid / Review-gated / Governance-only

**Enforcement Mechanism:** [ENFORCEMENT_MECHANISM_DESCRIPTION]

**Automated Check Reference:** [AUTOMATED_CHECK_ID]

**Tool / Script Used:** [TOOL_OR_SCRIPT]

**Tool Independence Note:** This field is OPTIONAL per CN-1; enforcement mechanisms MUST be described in tool-agnostic terms where possible [Ref: CN-1].

**Enforcement Trigger:** [ENFORCEMENT_TRIGGER]

Allowed values: Pre-commit / Pre-merge / Continuous / On-demand / Review gate / State transition / Other

**Enforcement Frequency:** [ENFORCEMENT_FREQUENCY]

---

## 5. Verification Method

> Field definition per §16.2: Every requirement SHALL be assigned one or more verification methods [Ref: §16.2].

**Primary Verification Method:** [PRIMARY_VERIFICATION_METHOD]

Allowed values per §16.2: Inspection / Analysis / Demonstration / Test

**Verification Method Details:** [VERIFICATION_METHOD_DETAILS]

**Verification Criteria (pass/fail):** [VERIFICATION_CRITERIA]

**Verification Evidence Produced:** [VERIFICATION_EVIDENCE]

**Confidence Level Required for Verification:** [CONFIDENCE_LEVEL_REQUIRED] [Ref: §26.2]

**Verification Artifacts:** [VERIFICATION_ARTIFACTS]

**Verification Schedule:** [VERIFICATION_SCHEDULE]

---

## 6. Violation Handling

> Field definition per §40.2: Violation of any INT rule renders the affected work non-conformant, MUST block state transition, and MUST block Repository Readiness [Ref: §40.2].

**Violation Classification:** [VIOLATION_CLASSIFICATION]

Allowed values: Non-conformant (blocking) / Warning (non-blocking) / Informational

**State Transition Impact:** [STATE_TRANSITION_IMPACT]

Normative: Per STA-5, an INT violation MUST block the transition out of its originating state [Ref: STA-5, §40.2].

**Repository Readiness Impact:** [READINESS_IMPACT]

Normative: Per RDY-3, any INT violation MUST block "Repository Ready" [Ref: RDY-3, §41.3].

**Immediate Action on Violation:** [IMMEDIATE_ACTION]

**Escalation Path:** [ESCALATION_PATH]

**Waiver Process:** [WAIVER_PROCESS]

Normative: Per §40.2, INT rules MAY be waived only through governance (§17) [Ref: §40.2, §17].

**Waiver Authority:** [WAIVER_AUTHORITY]

**Waiver Reference (if waived):** [WAIVER_REFERENCE]

**Violation History:**

| Date | Violation Description | Detected By | Resolution | Resolution Date |
|---|---|---|---|---|
| [V_1_DATE] | [V_1_DESC] | [V_1_DETECTED_BY] | [V_1_RESOLUTION] | [V_1_RES_DATE] |
| [V_2_DATE] | [V_2_DESC] | [V_2_DETECTED_BY] | [V_2_RESOLUTION] | [V_2_RES_DATE] |

---

## 7. Governance & Traceability

> Normative rule: KN-4: Contracts and invariants are authoritative and changes MUST pass through governance + versioning [Ref: KN-4, §14.3].

**Authorizing Decision:** [AUTHORIZING_DECISION_ID] [Ref: §35]

**Traceability Links:** [TRACEABILITY_LINKS] [Ref: §48]

**Review Record Reference:** [REVIEW_RECORD_ID] [Ref: §15]

**Related Invariants:** [RELATED_INVARIANT_IDS]

**Related Contracts:** [RELATED_CONTRACT_IDS] [Ref: §11.3]

**Related Requirements:** [RELATED_REQUIREMENT_IDS]

**Evidence References:** [EVIDENCE_REFERENCES] [Ref: §28]

**Provenance Record:** [PROVENANCE_RECORD_ID] [Ref: §26.3]

---

## 8. Change Log

> Normative rule: VS-2: Every change MUST be recorded in a changelog [Ref: §18, VS-2].

| Version | Date | Author | Change | Governance Reference |
|---|---|---|---|---|
| [CHG_1_VER] | [CHG_1_DATE] | [CHG_1_AUTHOR] | [CHG_1_DESC] | [CHG_1_GOV_REF] |
| [CHG_2_VER] | [CHG_2_DATE] | [CHG_2_AUTHOR] | [CHG_2_DESC] | [CHG_2_GOV_REF] |
| [CHG_N_VER] | [CHG_N_DATE] | [CHG_N_AUTHOR] | [CHG_N_DESC] | [CHG_N_GOV_REF] |
