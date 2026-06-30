# Validation Rules

> **Authority Class:** Authoritative
> **SDD Authority:** §16.4, §16.2, §16.1
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 6

## 1. Purpose

This document defines the **normative validation rules** (VL-1 through VL-5) for the Software Engineering Standard (SES). It specifies the criteria by which conformance of a project to the SES is objectively assessed. [Ref: §16.4]

This document also defines the **verification method taxonomy** (§16.2) and the **verification vs validation distinction** (§16.1) that underpin these rules. [Ref: §16.2, §16.1]

## 2. Verification vs Validation Distinction (§16.1)

The SES **SHALL** preserve the formal distinction:

- **Verification** = "Are we building it right?" — conformance to specification. [Ref: §16.1]
- **Validation** = "Are we building the right thing?" — fitness for intended use. [Ref: §16.1]

This distinction is drawn from ISO/IEC/IEEE 1012-2016 and the SWEBOK Verification and Validation Knowledge Area. [Ref: ISO/IEC/IEEE 1012-2016; SWEBOK V&V KA]

In the context of the SES:

- **Verification** is the process of checking that a project conforms to the standard's requirements (the specification).
- **Validation** is the process of checking that the standard's requirements are the right requirements — that is, that conformance to the SES produces engineering outcomes fit for the organization's intended use.

Both activities **MUST** be present and **MUST** be distinct. [Ref: §16.1]

## 3. Verification Methods (§16.2)

Every requirement in the SES (and in projects governed by it) **SHALL** be assigned one or more verification methods from the standard taxonomy. [Ref: §16.2; ISO/IEC/IEEE 29148:2018]

The four standard verification methods are:

| Method | Code | Definition | Applicability |
|---|---|---|---|
| **Inspection** | **I** | Visual examination of an artifact against criteria | Authoritative artifacts, documentation, records |
| **Analysis** | **A** | Mathematical, logical, or algorithmic evaluation | Algorithms, constraints, independence proofs |
| **Demonstration** | **D** | Execution showing the requirement is satisfied | Operational qualities, machine-readability |
| **Test** | **T** | Execution against predefined inputs with expected outputs | Functional correctness, measurable qualities |

Each requirement class **MUST** have a defined verification method. [Ref: VL-2; §16.2]

## 4. Validation Rules (VL-1..VL-5)

### VL-1: Objective Pass/Fail

Conformance of a project to the SES **MUST** be expressed as **objective pass/fail against stated criteria**, never as subjective judgment. [Ref: §16.4 VL-1; PR-7]

**Normative implications:**

- A conformance verdict **MUST NOT** be expressed as a subjective assessment (e.g., "the project seems compliant").
- A conformance verdict **MUST** state a clear pass or fail against each stated criterion.
- The criteria against which conformance is judged **MUST** be written and available before verification begins.

### VL-2: Defined Verification Method Per Requirement Class

Each requirement class **MUST** have a defined verification method (§16.2). [Ref: §16.4 VL-2; ISO/IEC/IEEE 29148:2018]

**Normative implications:**

- No requirement class **MAY** be left without an assigned verification method.
- The verification method **MUST** be one of: Inspection (I), Analysis (A), Demonstration (D), or Test (T).
- A requirement class **MAY** have more than one verification method.

### VL-3: Recorded and Reproducible Evidence

Validation evidence **MUST** be **recorded** and **reproducible**. [Ref: §16.4 VL-3; PR-9]

**Normative implications:**

- Evidence **MUST** exist in a recorded form (version-controlled repository artifact), never solely in conversation or tooling state. [Ref: PR-4]
- Evidence **SHOULD** be reproducible: given the same inputs, the same evidence **SHOULD** be producible again. [Ref: PR-9]
- Evidence **MUST NOT** be transient or ephemeral.

### VL-4: Evidence-Cited Verdict

A conformance verdict **MUST** cite the **evidence on which it rests**. [Ref: §16.4 VL-4; PR-5]

**Normative implications:**

- Every verdict (pass or fail) **MUST** reference the specific evidence that supports it.
- A verdict without cited evidence is **non-conformant**.
- Evidence citations **MUST** be traceable to their source artifacts. [Ref: §28; §48]

### VL-5: Separation of Validation from Implementation

Validation **MUST** be a **responsibility distinct from implementation/execution** (PR-8). [Ref: §16.4 VL-5; ISO/IEC/IEEE 1012-2016]

**Normative implications:**

- The same person or agent **SHOULD NOT** both implement and validate the same work product, where independence adds value.
- Validation findings **MUST** be recorded independently of implementation records.
- Validation **MUST NOT** be subsumed into implementation activities; it **MUST** remain a distinct activity. [Ref: PR-8]

## 5. Validation Evidence Requirements

Validation evidence **MUST** satisfy all of the following:

| ID | Requirement | Authority |
|---|---|---|
| **VE-1** | Evidence **MUST** be recorded in a version-controlled artifact | VL-3, PR-4 |
| **VE-2** | Evidence **MUST** be reproducible | VL-3, PR-9 |
| **VE-3** | Evidence **MUST** cite the requirement it verifies | VL-4, PR-5 |
| **VE-4** | Evidence **MUST** carry provenance (source, date, validator identity) | PR-5, §28 |
| **VE-5** | Evidence **MUST** be distinct from the implementation artifact it validates | VL-5, PR-8 |

## 6. Separation of Duties (VL-5, PR-8)

The separation of validation from implementation is a **constitutional principle** of the SES. [Ref: PR-8; ISO/IEC/IEEE 1012-2016]

### 6.1 Independence Requirements

- **IND-1.** Where feasible, validation **SHOULD** be performed by a person or agent other than the sole author of the work product being validated. [Ref: §15 RV-4]
- **IND-2.** Validation records **MUST** be maintained separately from implementation records. [Ref: VL-5]
- **IND-3.** A validation verdict **MUST NOT** be overridden by the implementer without governance review. [Ref: PR-8; §17]

### 6.2 Boundaries

The following activities **MUST** remain distinct:

- Execution (implementation of a change) and Verification (checking the change).
- Design and Validation (validation checks the outcome, not the process that produced it).
- Review (§15, human/criteria-based examination) and Validation (§16, objective conformance verification). They are complementary and **MUST NOT** be merged. [Ref: §15.3; PR-8]

## 7. Completion Criteria

This validation rules document is complete when:

- **CC-1.** All five validation rules VL-1..VL-5 are defined with normative implications. [Ref: §16.4]
- **CC-2.** The verification method taxonomy (I/A/D/T) is specified. [Ref: §16.2]
- **CC-3.** The verification vs validation distinction is preserved. [Ref: §16.1]
- **CC-4.** Evidence requirements are specified. [Ref: VL-3, VL-4]
- **CC-5.** Separation of duties (VL-5, PR-8) is defined. [Ref: §16.4 VL-5]
- **CC-6.** Every normative rule cites its SDD authority. [Ref: FR-11]
