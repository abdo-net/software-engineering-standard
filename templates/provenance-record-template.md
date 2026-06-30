# Provenance Record Template

---

## Artifact Metadata

| Field | Value |
|---|---|
| **Artifact ID** | [PROVENANCE_RECORD_ID] |
| **Artifact Type** | Provenance Record [Ref: §11.3] |
| **Authority Class** | Authoritative [Ref: §11.1] |
| **Object Type** | Evidence [Ref: §42.2, §14.2] |
| **Owner** | [OWNER] [Ref: §11.2] |
| **Version** | [VERSION] [Ref: §18] |
| **Status** | [STATUS] [Ref: §11.2] |
| **Created Timestamp** | [TIMESTAMP] [Ref: §26.3] |
| **Decision References** | [DECISION_REFERENCE] [Ref: §43.2] |

---

## 1. Fact Identity

> Field definition per §14.2: Facts are verified statements about the system, each with provenance [Ref: §14.2].
> Normative rule: KN-1: Every recorded fact MUST carry provenance — a reference to the source evidence; a fact without provenance is non-authoritative [Ref: KN-1, §14.3].

**Fact Identifier:** [FACT_ID]

**Fact Type:** [FACT_TYPE]

Allowed values: Observed / Verified / Synthesized / Derived / Other

**Fact Statement:** [FACT_STATEMENT]

**Related Knowledge Category:** [KNOWLEDGE_CATEGORY]

Allowed values per §14.2: Facts / Decisions / Contracts / Invariants / Rationale / Provenance

**Date Recorded:** [DATE_RECORDED]

**Recorded By:** [RECORDED_BY]

---

## 2. Confidence Level (A-E)

> Mandatory fact field 1 of 5 per §26.3: Confidence Level.
> Normative rule: EVC-1: Every engineering fact MUST carry a confidence level (A-E) [Ref: EVC-1, §26.4].

**Confidence Level:** [CONFIDENCE_LEVEL]

| Level | Definition | Relative Strength |
|---|---|---|
| A | Observed directly at runtime (actual behavior) | Highest |
| B | Confirmed by implementation (source code) | High |
| C | Confirmed by official documentation | Medium |
| D | Derived from multiple independent evidence sources (triangulation / inference) | Medium-low |
| E | Engineering hypothesis (unverified) | Lowest |

**Selected Level:** [SELECTED_CONFIDENCE_LEVEL] [Ref: §26.2]

**Confidence Rationale:** [CONFIDENCE_RATIONALE]

**Confidence Change History:**

| Previous Level | New Level | Date | Reason |
|---|---|---|---|
| [PREV_LVL] | [NEW_LVL] | [CHANGE_DATE] | [CHANGE_REASON] |

> Normative rule: EVC-5: Confidence MAY be raised only by recording additional evidence/provenance; it MUST NOT be raised by assertion [Ref: EVC-5, §26.4].

---

## 3. Evidence Source

> Mandatory fact field 2 of 5 per §26.3: Evidence Source.
> Normative rule: EVC-2: Every fact MUST record all five fields [Ref: EVC-2, §26.4].

**Evidence Source Type:** [EVIDENCE_SOURCE_TYPE]

Allowed values: Static Analysis / Dynamic Analysis / Runtime Observation / Official Documentation / Human Expert / Triangulated / Automated Tool / Other

**Evidence Source Description:** [EVIDENCE_SOURCE_DESCRIPTION]

**Evidence Source Location:** [EVIDENCE_SOURCE_LOCATION]

**Evidence Source Commit Reference:** [EVIDENCE_SOURCE_COMMIT_REF]

**Triangulation Applied:** [TRIANGULATION_APPLIED]

Normative: Per KN-6, where feasible a fact SHOULD be corroborated by more than one source class before being recorded as authoritative [Ref: KN-6, §14.3].

**Triangulation Sources:**

| Source Class | Source ID | Result |
|---|---|---|
| Static | [STATIC_SRC_ID] | [STATIC_RESULT] |
| Dynamic | [DYNAMIC_SRC_ID] | [DYNAMIC_RESULT] |
| Human | [HUMAN_SRC_ID] | [HUMAN_RESULT] |

**Evidence Chain Reference:** [EVIDENCE_CHAIN_ID] [Ref: §28]

---

## 4. Verification Status

> Mandatory fact field 3 of 5 per §26.3: Verification Status.
> Normative rule: EVC-3: A Level-E fact is a hypothesis and MUST NOT be treated as authoritative [Ref: EVC-3, §26.4].

**Current Verification Status:** [VERIFICATION_STATUS]

Allowed values: Unverified / Pending / Verified / Failed / Rejected / Obsolete

**Verification Method Used:** [VERIFICATION_METHOD]

Allowed values per §16.2: Inspection / Analysis / Demonstration / Test

**Verification Date:** [VERIFICATION_DATE]

**Verified By:** [VERIFIED_BY]

**Verification Evidence:** [VERIFICATION_EVIDENCE]

**Verification Artefact References:** [VERIFICATION_ARTEFACT_REFS]

**Next Verification Due:** [NEXT_VERIFICATION_DUE]

---

## 5. Timestamp

> Mandatory fact field 4 of 5 per §26.3: Timestamp.
> Normative rule: EVC-2: Every fact MUST record all five fields [Ref: EVC-2, §26.4].

**Record Created Timestamp:** [RECORD_CREATED_TS]

**Evidence Captured Timestamp:** [EVIDENCE_CAPTURED_TS]

**Verification Completed Timestamp:** [VERIFICATION_COMPLETED_TS]

**Last Updated Timestamp:** [LAST_UPDATED_TS]

**Timezone:** [TIMEZONE]

**Timestamp Format:** ISO 8601 (YYYY-MM-DDTHH:MM:SSZ) [Ref: NIST SP 800-86]

---

## 6. Repository Reference

> Mandatory fact field 5 of 5 per §26.3: Repository Reference.
> Normative rule: EVC-2: Every fact MUST record all five fields [Ref: EVC-2, §26.4].

**Repository Location (canonical path):** [REPOSITORY_LOCATION]

**File Path(s):** [FILE_PATHS]

**Commit Hash:** [COMMIT_HASH]

**Branch / Tag:** [BRANCH_OR_TAG]

**Line Numbers (if applicable):** [LINE_NUMBERS]

**Related Object IDs:** [RELATED_OBJECT_IDS] [Ref: §43]

**Traceability Graph Node ID:** [TRACEABILITY_NODE_ID] [Ref: §48]

---

## 7. Provenance Chain

> Field definition per §11.3: Provenance Record — links any recorded fact to its source evidence [Ref: §11.3].
> Normative rule: ECH-2: Each link MUST preserve provenance to its predecessor (unbroken chain of custody) [Ref: ECH-2, §28.3].

**Upstream Provenance (predecessor):** [UPSTREAM_PROVENANCE_ID]

**Downstream References (successors):** [DOWNSTREAM_REFERENCE_IDS]

**Chain Position:** [CHAIN_POSITION]

Allowed values: Observation / Evidence / Verification / Fact / Knowledge / Decision / Implementation / Validation / Documentation / Repository [Ref: §28.2]

**Chain Integrity Check:** [CHAIN_INTEGRITY_STATUS]

Normative: Per ECH-4, asserting a downstream node without its upstream evidence is non-conformant [Ref: ECH-4, §28.3].

---

## 8. Governance & Traceability

> Normative rule: EVC-4: No fact MAY become authoritative without a confidence classification [Ref: EVC-4, §26.4].

**Authorizing Decision:** [AUTHORIZING_DECISION_ID] [Ref: §35]

**Traceability Links:** [TRACEABILITY_LINKS] [Ref: §48]

**Review Record Reference:** [REVIEW_RECORD_ID] [Ref: §15]

**Related Facts:** [RELATED_FACT_IDS]

**Related Decisions:** [RELATED_DECISION_IDS]

**Related Contracts:** [RELATED_CONTRACT_IDS]

**Confidence Model Reference:** [CONFIDENCE_MODEL_ID] [Ref: §26]

---

## 9. Change Log

> Normative rule: VS-2: Every change MUST be recorded in a changelog [Ref: §18, VS-2].

| Version | Date | Author | Change | Governance Reference |
|---|---|---|---|---|
| [CHG_1_VER] | [CHG_1_DATE] | [CHG_1_AUTHOR] | [CHG_1_DESC] | [CHG_1_GOV_REF] |
| [CHG_2_VER] | [CHG_2_DATE] | [CHG_2_AUTHOR] | [CHG_2_DESC] | [CHG_2_GOV_REF] |
| [CHG_N_VER] | [CHG_N_DATE] | [CHG_N_AUTHOR] | [CHG_N_DESC] | [CHG_N_GOV_REF] |
