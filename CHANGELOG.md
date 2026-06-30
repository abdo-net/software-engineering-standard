# Changelog

All notable changes to this standard are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).

## [0.4.0] — 2026-06-30

### Phase 5 — Define Stages (COMPLETED)

- Created `docs/stage-catalog.md` — Stage catalog with 8-field schema per stage (Entry Criteria, Inputs, Activities, Outputs, Evidence Produced, Exit Criteria, Verification Criteria, Review Type) and 4 normative rules (SG-1..SG-4). [Ref: §13.2, §13.3]
- Created `docs/completion-criteria.md` — 13 completion states with objective exit criteria per CMP-1 and 5 normative rules (CMP-1..CMP-5). [Ref: §27.2, §27.3]
- Created `docs/readiness-gates.md` — 9 readiness gates with composition rules and 5 normative rules (RDY-1..RDY-5). [Ref: §41.2, §41.3]

### Phase 4 — Define Artifacts (COMPLETED)

- Created `docs/artifact-catalog.md` — Full artifact catalog: 3 authority classes, 5 special artifact types, 6 knowledge categories, 15 mandatory object fields. [Ref: §11.1, §11.2, §11.3, §11.4, §14.2, §43.2]
- Created `docs/adr-schema.md` — Architecture Decision Record schema with 9 Decision fields, immutability rules, supersession rules. [Ref: §11.3, §35.2, KN-2]
- Created `docs/contract-specification-schema.md` — Contract Specification schema with format-agnostic design per CN-1. [Ref: §11.3, §14.2, §37.2]
- Created `docs/invariant-register-schema.md` — Invariant Register schema with relationship to INT-1..INT-10 integrity rules. [Ref: §11.3, §14.2, §40.1]
- Created `docs/provenance-record-schema.md` — Provenance Record schema with 5 mandatory fact fields and Evidence Chain linkage. [Ref: §11.3, §14.2, §28, §26.3]
- Created `docs/traceability-index-schema.md` — Traceability Index schema (Generated artifact) with link to Traceability Graph. [Ref: §11.3, §29, §48, Appendix C]
- Created `docs/knowledge-model-schemas.md` — Schemas for all 6 knowledge categories (Facts, Decisions, Contracts, Invariants, Rationale, Provenance) with KN-1..KN-6. [Ref: §14.2, §14.3, §31.2]
- Created `docs/documentation-categories.md` — 9 documentation categories (Observed, Verified, Planned, Implemented, Validated, Historical, Deprecated, Generated, Authoritative) with DOC-1..DOC-5. [Ref: §38.2, §38.3, §31.2]
- Created `docs/object-schema-reference.md` — 15 mandatory object fields per §43.2 with OM-1..OM-6 normative rules. [Ref: §43.2, §43.3, §42.2]

### Phase 3 — Define Engineering Lifecycle (COMPLETED)

- Created `docs/engineering-lifecycle.md` — Full lifecycle specification for 11 phases with 9 mandated fields per phase. [Ref: §12.1, §12.2, §12.3]
- Created `docs/discovery-specification.md` — Full specification for 25 mandated discovery activities across 7 layers. [Ref: §25.3, §25.4]
- Created `docs/competing-approaches.md` — 4 documented approach tensions with context-binding. [Ref: §12.4, §30.4, PR-12, FR-12]
- Created `docs/mission-specification.md` — Mission Model with 8 elements and MIS-1..MIS-6. [Ref: §32.2, §32.3]
- Created `docs/state-machine-specification.md` — 9 engineering states with STA-1..STA-5. [Ref: §33.2, §33.3, §33.4]
- Created `docs/operation-specification.md` — 10 engineering operations with OPS-1..OPS-4. [Ref: §34.2, §34.3, §34.4]

### Phase 2 — Repository Foundation (COMPLETED)

- Created the `software-engineering-standard` repository.
- Established directory structure per SDD §10 Repository Architecture.
- Placed SDD v0.4.0 as the authoritative normative document in `standard/SDD.md`.
- Completed Phase 2 governance foundation:
  - `standard/repository-constitution.md`, `standard/repository-rules.md`
  - `standard/artifact-classification.md`, `standard/artifact-registry.md`

## [0.3.0] — SDD Revision

### Added
- Completion extension: appended architectural models §32–§41.

## [0.2.0] — SDD Revision

### Added
- Review extension: appended architectural models §25–§31.

## [0.1.0] — SDD Initial

### Added
- Initial SDD with sections 1–24 and Appendices A–C.

---

*This changelog is a repository artifact. The SDD revision history (§0) is the authoritative source for SDD changes; this file mirrors it for repository-level tracking.*
