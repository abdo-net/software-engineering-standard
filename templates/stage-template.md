# Stage Template

| Field | Value |
|---|---|
| **Artifact ID** | `[ARTIFACT_ID]` |
| **Artifact Type** | Stage |
| **Authority Class** | Authoritative |
| **Owner** | `[OWNER_NAME]` |
| **Version** | `[VERSION]` |
| **Status** | `[STATUS]` |
| **Standard Version** | `[SES_VERSION]` |
| **Created** | `[DATE]` |

---

> **SDD Authority:** This template is derived from the Stage Model (§13). [Ref: §13.2]
>
> **Normative Rules Applied:** SG-1 (exit criteria must be verified); SG-2 (outputs classified per §11); SG-3 (re-entry must be recorded); SG-4 (separation of duties). [Ref: §13.3]

---

## Stage Identification

| Field | Value |
|---|---|
| **Stage Name** | `[STAGE_NAME]` |
| **Stage ID** | `[STAGE_ID]` |
| **Lifecycle Phase** | Understanding / Reverse Engineering / Analysis / Planning / Implementation / Validation / Documentation / Maintenance / Evolution / Retirement |
| **Governing State (§33)** | `[STATE_NAME]` |

---

## 1. Entry Criteria

> Per §13.2: Preconditions that MUST hold before the stage may begin. [Ref: §13.2]

[PLACEHOLDER: List all preconditions that MUST be satisfied before this stage can be entered. A stage MUST NOT begin until its entry criteria are met.]

| Criterion ID | Criterion | Verification Method |
|---|---|---|
| `[EC-1]` | `[ENTRY_CRITERION_1]` | `[METHOD]` |
| `[EC-2]` | `[ENTRY_CRITERION_2]` | `[METHOD]` |
| `[EC-3]` | `[ENTRY_CRITERION_3]` | `[METHOD]` |

---

## 2. Inputs

> Per §13.2: Authoritative artifacts consumed. [Ref: §13.2]

[PLACEHOLDER: Enumerate all authoritative artifacts that this stage consumes as inputs. Inputs MUST be classified per the Artifact Authority Model (§11.1).]

| Input ID | Artifact | Authority Class | Source Location |
|---|---|---|---|
| `[IN-1]` | `[INPUT_ARTIFACT_1]` | Auth/Derived/Gen | `[LOCATION]` |
| `[IN-2]` | `[INPUT_ARTIFACT_2]` | Auth/Derived/Gen | `[LOCATION]` |

---

## 3. Activities

> Per §13.2: Work performed. [Ref: §13.2]

[PLACEHOLDER: Describe the activities performed during this stage. Activities MUST produce the stated outputs and evidence.]

| Activity ID | Activity | Responsible Role | Output Produced |
|---|---|---|---|
| `[ACT-1]` | `[ACTIVITY_1]` | `[ROLE]` | `[OUTPUT_REF]` |
| `[ACT-2]` | `[ACTIVITY_2]` | `[ROLE]` | `[OUTPUT_REF]` |
| `[ACT-3]` | `[ACTIVITY_3]` | `[ROLE]` | `[OUTPUT_REF]` |

---

## 4. Outputs

> Per §13.2: Artifacts produced, with authority class. [Ref: §13.2]
> Stage outputs MUST be classified per the Artifact Authority Model per SG-2. [Ref: §13.3, SG-2]

[PLACEHOLDER: Enumerate all artifacts produced by this stage, each with its authority class per §11.1.]

| Output ID | Artifact | Authority Class | Destination |
|---|---|---|---|
| `[OUT-1]` | `[OUTPUT_ARTIFACT_1]` | Auth/Derived/Gen | `[LOCATION]` |
| `[OUT-2]` | `[OUTPUT_ARTIFACT_2]` | Auth/Derived/Gen | `[LOCATION]` |

---

## 5. Evidence Produced

> Per §13.2: Verifiable evidence of the work. [Ref: §13.2]

[PLACEHOLDER: Specify the verifiable evidence produced during this stage. Evidence MUST carry provenance (§28).]

| Evidence ID | Evidence Item | Type | Location | Provenance |
|---|---|---|---|---|
| `[EV-1]` | `[EVIDENCE_ITEM_1]` | `[TYPE]` | `[LOCATION]` | `[SOURCE]` |
| `[EV-2]` | `[EVIDENCE_ITEM_2]` | Type | `[LOCATION]` | `[SOURCE]` |

---

## 6. Exit Criteria

> Per §13.2: Postconditions that MUST hold to leave the stage. [Ref: §13.2]
> A stage MUST NOT be declared complete unless its exit criteria are verified per SG-1. [Ref: §13.3, SG-1]

[PLACEHOLDER: List all postconditions that MUST be satisfied to exit this stage.]

| Criterion ID | Criterion | Verification Method | Met? |
|---|---|---|---|
| `[XC-1]` | `[EXIT_CRITERION_1]` | `[METHOD]` | [ ] |
| `[XC-2]` | `[EXIT_CRITERION_2]` | `[METHOD]` | [ ] |
| `[XC-3]` | `[EXIT_CRITERION_3]` | `[METHOD]` | [ ] |

---

## 7. Verification Criteria

> Per §13.2: How exit is objectively checked. [Ref: §13.2]

[PLACEHOLDER: Define the objective method(s) by which exit criteria are verified. Verification MUST be against explicit, written criteria per RV-3 (§15.3).] [Ref: §15.3]

| Criterion ID | Verification Method | Verification Criteria | Pass/Fail |
|---|---|---|---|
| `[VC-1]` | Inspection / Analysis / Demonstration / Test | `[CRITERIA]` | `[RESULT]` |
| `[VC-2]` | Inspection / Analysis / Demonstration / Test | `[CRITERIA]` | `[RESULT]` |

---

## 8. Review Type

> Per §13.2: Which review (§15) gates the stage. [Ref: §13.2]

[PLACEHOLDER: Select the review type that gates this stage per §15.1. Every authoritative artifact MUST pass at least one review of an appropriate type per RV-1.] [Ref: §15.2, RV-1]

| Review Type | Selected | Rationale |
|---|---|---|
| **Inspection** | [ ] | Formal, rigorous defect detection; for high-risk artifacts per §15.1 |
| **Technical Review** | [ ] | Evaluate fitness for purpose by qualified reviewers per §15.1 |
| **Walkthrough** | [ ] | Author-led, educational, early feedback per §15.1 |
| **Audit** | [ ] | Independent conformance check per §15.1 |
| **Management Review** | [ ] | Status/decision review by authority per §15.1 |

---

## Normative Stage Rules Compliance

| Rule ID | Statement | Compliant? |
|---|---|---|
| **SG-1** | Exit criteria verified by the named verification method. [Ref: §13.3] | [ ] |
| **SG-2** | Outputs classified per Artifact Authority Model (§11). [Ref: §13.3] | [ ] |
| **SG-3** | Re-entry recorded if stage is iterated. [Ref: §13.3] | N/A / [ ] |
| **SG-4** | Separation of duties maintained between production and verification. [Ref: §13.3] | [ ] |

---

## Stage Re-entry Record (SG-3)

> A stage MAY be re-entered (iteration); re-entry MUST be recorded per SG-3. [Ref: §13.3, SG-3]

| Re-entry # | Date | Reason | Authorized By |
|---|---|---|---|
| `[RE-1]` | `[DATE]` | `[REASON]` | `[AUTHORITY]` |

---

> **Placeholder count:** 18 distinct `[PLACEHOLDER]` fields.
