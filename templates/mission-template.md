| Field | Value |
|---|---|
| **Artifact ID** | `[ARTIFACT_ID]` |
| **Artifact Type** | Mission |
| **Authority Class** | Authoritative |
| **Owner** | `[OWNER_NAME]` |
| **Version** | `[VERSION]` |
| **Status** | `[STATUS]` |
| **Standard Version** | `[SES_VERSION]` |
| **Created** | `[DATE]` |

---

> **SDD Authority:** This template is derived from the Engineering Mission Model (§32). [Ref: §32.2]
>
> **Normative Rules Applied:** MIS-1 (no activity without active Mission); MIS-2 (all 8 elements required); MIS-3 (Allowed/Forbidden Operations from §34); MIS-4 (scope/constraints binding); MIS-5 (objective success criteria); MIS-6 (artifact-to-mission traceability). [Ref: §32.3]

---

## 1. Objective

[PLACEHOLDER: State the clear, singular objective of this engineering mission. The objective MUST be objective and verifiable per MIS-5. Every produced artifact MUST trace to this Mission per MIS-6.]

---

## 2. Scope

[PLACEHOLDER: Define what is in scope for this mission. Engineering activity MUST NOT exceed the Mission Scope per MIS-4. Deviations REQUIRE a new or amended Mission per MIS-4.]

---

## 3. Constraints

[PLACEHOLDER: List all non-negotiable boundaries. These may include time, budget, technology, compliance, or organizational constraints. A Mission is NOT active if this element is omitted per MIS-2.]

---

## 4. Expected Deliverables

[PLACEHOLDER: Enumerate the concrete artifacts, outputs, or changes expected from this mission. Each deliverable MUST be classified per the Artifact Authority Model (§11.1).] [Ref: §11]

---

## 5. Success Criteria

[PLACEHOLDER: Define objective, verifiable criteria that determine when this mission is complete. Success criteria MUST be objectively verifiable per MIS-5 and §16 (Validation Model).]

---

## 6. Allowed Operations

[PLACEHOLDER: Select from the canonical operation set defined in §34.2. A Mission's Allowed Operations are a subset of the Operation Model per OPS-1 and MIS-3.]

The canonical operations per §34.2 are:

| Operation | Included? | Notes |
|---|---|---|
| **DISCOVER** | [ ] | Governed by §25 |
| **ANALYZE** | [ ] | Governed by §12 Analysis |
| **TRACE** | [ ] | Governed by §29 |
| **VERIFY** | [ ] | Governed by §16 |
| **DOCUMENT** | [ ] | Governed by §38 |
| **COMPARE** | [ ] | Governed by §37 |
| **PLAN** | [ ] | Governed by §35 and §12 Planning |
| **IMPLEMENT** | [ ] | Governed by §12 Implementation |
| **VALIDATE** | [ ] | Governed by §16 |
| **REVIEW** | [ ] | Governed by §15 |

[PLACEHOLDER: Check the operations permitted for this mission. Examination operations (DISCOVER, TRACE, COMPARE, VERIFY) MUST NOT alter the subject system per OPS-4 and REV-1.] [Ref: §34.4, §30.3]

---

## 7. Forbidden Operations

[PLACEHOLDER: Explicitly list any operations from the canonical set (§34.2) that are NOT permitted for this mission. Engineering activity MUST NOT exceed the Mission Scope or violate its Constraints per MIS-4.]

---

## 8. Evidence Requirements

[PLACEHOLDER: Define what evidence MUST be produced and recorded for this mission. Evidence MUST carry provenance (§28) and, where it constitutes a fact, a confidence level (§26, levels A-E).] [Ref: §26, §28]

| Evidence Item | Required? | Confidence Level | Storage Location |
|---|---|---|---|
| `[EVIDENCE_ITEM_1]` | [ ] | A / B / C / D / E | `[LOCATION]` |
| `[EVIDENCE_ITEM_2]` | [ ] | A / B / C / D / E | `[LOCATION]` |
| `[EVIDENCE_ITEM_3]` | [ ] | A / B / C / D / E | `[LOCATION]` |

> **Confidence Levels (§26.2):** A = Observed at runtime (highest); B = Confirmed by implementation; C = Confirmed by documentation; D = Derived from multiple sources; E = Engineering hypothesis (unverified). [Ref: §26.2]

---

## Mission Traceability

| Trace Link | Reference |
|---|---|
| **Authorizing Decision** | `[DECISION_REFERENCE]` |
| **Parent Mission** | `[PARENT_MISSION_ID]` |
| **Target System** | `[SYSTEM_NAME]` |
| **Repository Location** | `[FILE_PATH]` |

---

> **Placeholder count:** 14 distinct `[PLACEHOLDER]` fields.
