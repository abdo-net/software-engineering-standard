# Conformance Procedure

> **Authority Class:** Authoritative
> **SDD Authority:** §16.5, §16.4, §18 VS-3
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 6

## 1. Purpose

This document defines the **conformance assertion procedure** for the Software Engineering Standard (SES). It specifies how a project declares, evidences, and records its conformance to the SES at a stated standard version. [Ref: §16.5]

The conformance assertion is the mechanism by which "the standard governs projects" becomes **verifiable rather than aspirational**. [Ref: §16.5, OBJ-7, FR-15]

## 2. Scope

This procedure applies to all projects that claim conformance to the SES. It specifies:

- The structure of a conformance assertion.
- The evidence required to support a conformance verdict.
- The obligation to bind the assertion to a specific standard version.
- The objective pass/fail criteria that govern conformance verdicts.

This procedure does **not** specify project-specific implementation details, which remain the responsibility of each project. [Ref: §4.3]

## 3. Normative Rules (VL-1..VL-5)

The following validation rules govern all conformance assertions:

- **VL-1.** Conformance of a project to the SES **MUST** be expressed as **objective pass/fail against stated criteria**, never as subjective judgment. [Ref: §16.4 VL-1; PR-7]
- **VL-2.** Each requirement class **MUST** have a defined verification method (§16.2). [Ref: §16.4 VL-2; ISO/IEC/IEEE 29148:2018]
- **VL-3.** Validation evidence **MUST** be recorded and reproducible. [Ref: §16.4 VL-3; PR-9]
- **VL-4.** A conformance verdict **MUST** cite the evidence on which it rests. [Ref: §16.4 VL-4; PR-5]
- **VL-5.** Validation **MUST** be a responsibility distinct from implementation/execution (PR-8). [Ref: §16.4 VL-5; ISO/IEC/IEEE 1012-2016]

## 4. Conformance Assertion Structure

A conformance assertion is a **recorded, evidenced statement** that a project satisfies the applicable SES requirements at a stated standard version. [Ref: §16.5]

A conformance assertion **SHALL** contain, at minimum, the following fields:

| Field | Description | Authority |
|---|---|---|
| **Project Identifier** | Unique name or identifier of the project asserting conformance | Project |
| **Standard Version** | The semantic version of the SES to which conformance is asserted | §18 VS-3 |
| **Assertion Date** | Date the assertion is made | Project |
| **Scope of Applicability** | Which SES requirements are claimed (core, plus named extensions if any) | §19 |
| **Conformance Verdict** | Pass or fail for each applicable requirement class | VL-1 |
| **Evidence References** | Pointers to recorded evidence supporting each verdict | VL-4 |
| **Validator Identity** | Person or agent performing the validation, distinct from implementer | VL-5 |
| **Evidence Location** | Repository location where evidence is recorded and reproducible | VL-3 |

## 5. Conformance Procedure

### Step 1: Determine Applicable Requirements

The project **MUST** identify the set of SES requirements applicable to its context. The core standard (§1–§50) is always applicable. Extensions (§19) **MAY** be included only if they are explicitly named in the assertion. [Ref: §19 EX-1..EX-6]

### Step 2: Select Verification Methods

For each applicable requirement, the project **MUST** apply the verification method assigned in the Verification Methods document (per §16.2). The four standard verification methods are: Inspection, Analysis, Demonstration, Test. [Ref: §16.2; ISO/IEC/IEEE 29148:2018]

### Step 3: Execute Verification

The project **MUST** execute the verification for each requirement, producing recorded, reproducible evidence. [Ref: VL-3]

### Step 4: Formulate Verdict

For each requirement, the project **MUST** formulate an **objective pass/fail verdict** based on the verification evidence. Subjective judgment **MUST NOT** substitute for evidence-based verdicts. [Ref: VL-1]

### Step 5: Cite Evidence

Every verdict **MUST** cite the specific evidence on which it rests. Evidence **MUST** be locatable in the project's repository or in the standard's repository. [Ref: VL-4]

### Step 6: Record Assertion

The completed conformance assertion **MUST** be recorded as an authoritative artifact in the project's repository. It **MUST** carry the mandatory artifact metadata per §11.2 (unique identifier, authority class, owner, version, status). [Ref: §11.2]

### Step 7: Bind to Standard Version

The conformance assertion **MUST** name the **standard version** to which conformance is asserted. [Ref: §18 VS-3]

## 6. Evidence Requirements

Conformance evidence **MUST** satisfy the following:

- **E-1. Recorded.** Evidence **MUST** exist in a version-controlled repository artifact, never solely in conversation or tooling state. [Ref: VL-3; PR-4]
- **E-2. Reproducible.** Given the same inputs, the evidence **SHOULD** be reproducible. [Ref: VL-3; PR-9]
- **E-3. Cited.** Every evidence item **MUST** be cited by the conformance verdict that depends upon it. [Ref: VL-4]
- **E-4. Provenanced.** Evidence **MUST** carry provenance linking it to the requirement it verifies. [Ref: PR-5; §28]

SDD does not specify the exact file format for conformance evidence. [Ref: §16.5]

## 7. Version Binding (VS-3)

- **VB-1.** A conformance assertion **MUST** name the **standard version** it conforms to, using semantic versioning (§18). [Ref: §18 VS-3]
- **VB-2.** A conformance assertion against version `X.Y.Z` **MUST** be re-evaluated when the standard releases a new **MAJOR** version, because MAJOR changes can break existing conformance. [Ref: §18.1 MAJOR; §18 VS-4]
- **VB-3.** A conformance assertion against version `X.Y.Z` **MAY** remain valid under a new **MINOR** or **PATCH** version of the same MAJOR line, because MINOR and PATCH changes are backward-compatible. [Ref: §18.1 MINOR, PATCH]
- **VB-4.** A project's conformance assertion **MUST** be re-evaluated whenever the project claims conformance to a different standard version. [Ref: §18 VS-3]

## 8. Completion Criteria

This conformance procedure document is complete when:

- **CC-1.** The conformance assertion structure (§4) is defined. [Ref: §16.5]
- **CC-2.** All five validation rules VL-1..VL-5 are incorporated. [Ref: §16.4]
- **CC-3.** Version binding rules per VS-3 are specified. [Ref: §18 VS-3]
- **CC-4.** The procedure is stated as objective pass/fail, with no subjective judgment. [Ref: VL-1]
- **CC-5.** Every normative rule cites its SDD authority. [Ref: FR-11]
