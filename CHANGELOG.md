# Changelog

All notable changes to this standard are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).

## [0.4.0] — 2026-06-30

### Phase 7 — Define Governance (COMPLETED)

- Created `docs/governance-procedure.md` — Operational governance procedure implementing GV-1..GV-7 (change proposals, approval process, version management, role definitions). [Ref: §17.1, §17.2, §17.3]
- Created `docs/roles-and-raci.md` — Role definitions for 4 mandated roles (Standard Authority, Maintainer, Reviewer, Contributor/Project) with RACI matrix. [Ref: §17.2 GV-7]
- Created `docs/governance-model-selection.md` — Comparison framework for 3 governance models (BDFL, Maintainer-Hierarchy, Committee/Foundation) per §17.3. [Ref: §17.3]

### Phase 6 — Define Validation (COMPLETED)

- Created `docs/conformance-procedure.md` — Conformance assertion procedure per §16.5 (recorded, evidenced statement of project conformance at stated standard version). [Ref: §16.5, §16.4 VL-1..VL-5, §18 VS-3]
- Created `docs/validation-rules.md` — 5 validation rules (VL-1..VL-5) with verification vs validation distinction and separation of duties. [Ref: §16.4, §16.1, §16.2]
- Created `docs/verification-methods.md` — Verification method assignments (I/A/D/T) for all 17 FRs and 13 NFRs per §16.2. [Ref: §16.2, FR-7, SC-7]
- Created `docs/validation-ordering.md` — Fast-feedback-first validation ordering with 9 layers and honesty marker per §16.3. [Ref: §16.3]
- Created `docs/inspection-checklist.md` — Inspection review checklist for high-risk artifacts (contracts, ADRs, standard). [Ref: §15.1, §15.2 RV-1..RV-5]
- Created `docs/technical-review-checklist.md` — Technical Review checklist for design docs and plans. [Ref: §15.1]
- Created `docs/walkthrough-checklist.md` — Walkthrough checklist for early-stage understanding/recovery. [Ref: §15.1]
- Created `docs/audit-checklist.md` — Audit checklist for independent conformance checks. [Ref: §15.1, §16.5]
- Created `docs/management-review-checklist.md` — Management Review checklist for governance gates. [Ref: §15.1, §17]
- Created `docs/completeness-metrics.md` — 14 completeness dimensions with metric definitions and 5 normative rules (CPL-1..CPL-5). [Ref: §50.2, §50.3]

### Phase 5 — Define Stages (COMPLETED)

- Created `docs/stage-catalog.md` — Stage catalog with 8-field schema per stage and SG-1..SG-4. [Ref: §13.2, §13.3]
- Created `docs/completion-criteria.md` — 13 completion states with objective exit criteria per CMP-1..CMP-5. [Ref: §27.2, §27.3]
- Created `docs/readiness-gates.md` — 9 readiness gates with composition rules per RDY-1..RDY-5. [Ref: §41.2, §41.3]

### Phase 4 — Define Artifacts (COMPLETED)

- Created `docs/artifact-catalog.md` — Full artifact catalog with 3 authority classes, 5 special types, 6 knowledge categories, 15 object fields. [Ref: §11.1-11.4, §14.2, §43.2]
- Created `docs/adr-schema.md`, `docs/contract-specification-schema.md`, `docs/invariant-register-schema.md`, `docs/provenance-record-schema.md`, `docs/traceability-index-schema.md` — Schemas for all 5 special artifact types per §11.3.
- Created `docs/knowledge-model-schemas.md` — Schemas for 6 knowledge categories with KN-1..KN-6. [Ref: §14.2, §14.3]
- Created `docs/documentation-categories.md` — 9 documentation categories with DOC-1..DOC-5. [Ref: §38.2, §38.3]
- Created `docs/object-schema-reference.md` — 15 mandatory object fields with OM-1..OM-6. [Ref: §43.2, §43.3]

### Phase 3 — Define Engineering Lifecycle (COMPLETED)

- Created `docs/engineering-lifecycle.md` — 11 lifecycle phases × 9 fields. [Ref: §12.1]
- Created `docs/discovery-specification.md` — 25 discovery activities × 9 fields. [Ref: §25.3]
- Created `docs/competing-approaches.md` — 4 approach tensions with context-binding. [Ref: §12.4, §30.4]
- Created `docs/mission-specification.md` — Mission Model with 8 elements, MIS-1..MIS-6. [Ref: §32.2]
- Created `docs/state-machine-specification.md` — 9 states with STA-1..STA-5. [Ref: §33.2]
- Created `docs/operation-specification.md` — 10 operations with OPS-1..OPS-4. [Ref: §34.2]

### Phase 2 — Repository Foundation (COMPLETED)

- Created repository with 5 regions per §10.3.
- Governance foundation: `standard/repository-constitution.md`, `standard/repository-rules.md`, `standard/artifact-classification.md`, `standard/artifact-registry.md`.

## [0.3.0] — SDD Revision

### Added
- Architectural models §32–§41.

## [0.2.0] — SDD Revision

### Added
- Architectural models §25–§31.

## [0.1.0] — SDD Initial

### Added
- Initial SDD with sections 1–24 and Appendices A–C.

---

*This changelog is a repository artifact. The SDD revision history (§0) is the authoritative source.*
