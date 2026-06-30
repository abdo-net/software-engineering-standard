# Verification Methods

> **Authority Class:** Authoritative
> **SDD Authority:** §16.2, FR-7, SC-7
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 6

## 1. Purpose

This document assigns **verification methods** to every requirement in the Software Engineering Standard (SES), per the taxonomy defined in §16.2. It populates the validation model architecture defined in §16 with specific, objective verification assignments for each functional and non-functional requirement. [Ref: §16.2; FR-7; SC-7]

Every requirement **SHALL** be assigned one or more verification methods from the standard taxonomy: **Inspection (I), Analysis (A), Demonstration (D), Test (T)**. [Ref: §16.2; ISO/IEC/IEEE 29148:2018]

## 2. Verification Method Taxonomy

The four verification methods are drawn from ISO/IEC/IEEE 29148:2018 and are the **complete** set used by the SES. [Ref: ISO/IEC/IEEE 29148:2018]

### 2.1 Inspection

**Inspection** is the visual examination of an artifact against defined criteria. It is the primary method for verifying structural, documentary, and rule-based requirements. [Ref: §16.2; ISO/IEC/IEEE 29148:2018]

- Applicable to: authoritative artifacts, documentation, records, rule compliance.
- Not applicable to: runtime behavior, performance characteristics.

### 2.2 Analysis

**Analysis** is the mathematical, logical, or algorithmic evaluation of an artifact or claim. It is the primary method for verifying independence, consistency, and structural properties. [Ref: §16.2; ISO/IEC/IEEE 29148:2018]

- Applicable to: algorithm correctness, constraint satisfaction, independence proofs, contradiction scans.
- Not applicable to: human-readable qualities, operational demonstrations.

### 2.3 Demonstration

**Demonstration** is the execution or operation of a system to show that a requirement is satisfied. It is the primary method for verifying operational and machine-readable qualities. [Ref: §16.2; ISO/IEC/IEEE 29148:2018]

- Applicable to: machine-readability, usability, operational qualities.
- Not applicable to: structural properties that require formal analysis.

### 2.4 Test

**Test** is the execution of a system against predefined inputs with expected outputs. It is the primary method for verifying measurable, functional qualities. [Ref: §16.2; ISO/IEC/IEEE 29148:2018]

- Applicable to: functional correctness, measurable quality attributes.
- Not applicable to: documentary or structural inspection requirements.

## 3. Functional Requirement Verification

Each functional requirement (FR-1..FR-17) from §8 **SHALL** be verified by the method(s) assigned below. [Ref: §8]

| ID | Requirement Summary | Verification Method | Rationale |
|---|---|---|---|
| **FR-1** | Lifecycle definition | **I** (Inspection) | Verify that the lifecycle definition exists and covers all mandated phases in §12.2. |
| **FR-2** | Artifact classes | **I** (Inspection) | Verify that the artifact class catalog exists and defines purpose, authority, owner, and lifecycle per §11. |
| **FR-3** | Authority classification | **I** (Inspection) | Verify that every artifact carries an authority classification (authoritative/derived/generated) per §11.1. |
| **FR-4** | Stages with gates | **I** (Inspection) | Verify that stages define entry criteria, activities, exit criteria, evidence, and verification per §13.2. |
| **FR-5** | Knowledge model | **I** (Inspection) | Verify that the knowledge model defines facts, decisions, contracts, and invariants with mandatory provenance per §14. |
| **FR-6** | Review model | **I** (Inspection) | Verify that the review model identifies review types and their applicability per §15.1. |
| **FR-7** | Validation model | **I** (Inspection) | Verify that the validation model specifies verification methods and pass/fail criteria per §16. |
| **FR-8** | Governance model | **I** (Inspection) | Verify that the governance model specifies proposal, review, approval, versioning, and supersession per §17. |
| **FR-9** | Versioning strategy | **I** (Inspection) | Verify that the versioning strategy defines MAJOR/MINOR/PATCH semantics per §18.1. |
| **FR-10** | Extension policy | **I** (Inspection) | Verify that the extension policy defines core vs extension rules per §19. |
| **FR-11** | Evidence reference | **A** (Analysis) | Verify by analysis that ≥99% of normative rules carry evidence or UNSUPPORTED markers; count unmarked rules. |
| **FR-12** | Competing approaches | **I** (Inspection) | Verify that competing approaches are presented and context-bound per §12.4, §17.3. |
| **FR-13** | Plain-text structured | **D** (Demonstration) | Verify by demonstration that the standard is readable with only a text editor and version control per NFR-1. |
| **FR-14** | Traceability | **I** (Inspection) | Verify that traceability links exist from principles → requirements → verification per Appendix C. |
| **FR-15** | Conformance assertion | **I** (Inspection) | Verify that the conformance assertion procedure is defined per §16.5. |
| **FR-16** | No vendor dependency | **A** (Analysis) | Verify by analysis that zero core rules name a specific commercial product, language, framework, or AI model. |
| **FR-17** | Repository structure | **I** (Inspection) | Verify that the repository separates standard, derived docs, references, templates, and examples per §10.3. |

## 4. Non-Functional Requirement Verification

Each non-functional requirement (NFR-1..NFR-13) from §9 **SHALL** be verified by the method(s) assigned below. NFR verification methods are as specified in the §9 table. [Ref: §9]

| ID | Quality | Requirement Summary | Verification Method |
|---|---|---|---|
| **NFR-1** | Tool/vendor independence | Standard usable with only text editor and version control | **D** (Demonstration) |
| **NFR-2** | Technology independence | No core rule assumes a language, framework, runtime, or architecture | **A** (Analysis) |
| **NFR-3** | Evidence integrity | >=99% of normative rules carry evidence reference or UNSUPPORTED marker | **A** (Analysis) |
| **NFR-4** | Unambiguity | Every requirement uses RFC 2119 keywords with one defensible interpretation | **I** (Inspection) |
| **NFR-5** | Verifiability | Every requirement has a stated verification method (I/A/D/T) | **I** (Inspection) |
| **NFR-6** | Machine-readability | Structure parseable by automated tooling | **D** (Demonstration) |
| **NFR-7** | Durability | Standard remains valid under replacement of any tool/vendor/AI | **A** (Analysis) |
| **NFR-8** | Traceability | Every requirement traceable forward and backward | **I** (Inspection) |
| **NFR-9** | Stability / controlled change | Changes follow governance + semantic versioning; no silent change | **I** (Inspection) |
| **NFR-10** | Readability for dual audience | Comprehensible to human engineer and automated agent | **I** (Inspection) / **D** (Demonstration) |
| **NFR-11** | Internal consistency | No two normative rules contradict | **A** (Analysis) |
| **NFR-12** | Minimality | No rule unnecessary to meet an objective | **I** (Inspection) |
| **NFR-13** | Longevity of references | Prefer durable sources over volatile URLs | **I** (Inspection) |

### 4.1 Verification Method Distribution Summary

| Method | FR Count | NFR Count | Total |
|---|---|---|---|
| **I** (Inspection) | 15 | 10 | 25 |
| **A** (Analysis) | 2 | 4 | 6 |
| **D** (Demonstration) | 1 | 2 | 3 |
| **T** (Test) | 0 | 0 | 0 |
| **I/D** (Combined) | 0 | 1 | 1 |

**Total requirements verified:** 30 (17 FR + 13 NFR). Every requirement has at least one assigned verification method. [Ref: §16.2 VL-2]

## 5. Completion Criteria

This verification methods document is complete when:

- **CC-1.** All four verification methods (I, A, D, T) are defined. [Ref: §16.2]
- **CC-2.** All 17 functional requirements (FR-1..FR-17) have assigned verification methods. [Ref: §8]
- **CC-3.** All 13 non-functional requirements (NFR-1..NFR-13) have assigned verification methods. [Ref: §9]
- **CC-4.** Every requirement has at least one verification method. [Ref: VL-2]
- **CC-5.** Every normative rule cites its SDD authority. [Ref: FR-11]
