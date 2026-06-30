# Changelog

All notable changes to this standard are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).

## [0.4.0] — 2026-06-30

### Phase 3 — Define Engineering Lifecycle (COMPLETED)

- Created `docs/engineering-lifecycle.md` — Full lifecycle specification for 11 phases with 9 mandated fields per phase (objectives, inputs, activities, outputs, evidence, verification, tools, mistakes, references). [Ref: §12.1, §12.2, §12.3]
- Created `docs/discovery-specification.md` — Full specification for 25 mandated discovery activities across 7 layers with 9 mandated fields per activity. [Ref: §25.3, §25.4]
- Created `docs/competing-approaches.md` — Presentation and context-binding of 4 documented approach tensions per §12.4 and §30.4. [Ref: §12.4, §30.4, PR-12, FR-12]
- Created `docs/mission-specification.md` — Full Mission Model specification with 8 mandatory elements and 6 normative rules (MIS-1..MIS-6). [Ref: §32.2, §32.3]
- Created `docs/state-machine-specification.md` — Full specification of 9 engineering states with 4 mandatory elements per state and 5 normative rules (STA-1..STA-5). [Ref: §33.2, §33.3, §33.4]
- Created `docs/operation-specification.md` — Full specification of 10 engineering operations with 4 mandatory elements per operation and 4 normative rules (OPS-1..OPS-4). [Ref: §34.2, §34.3, §34.4]

### Phase 2 — Repository Foundation (COMPLETED)

- Created the `software-engineering-standard` repository.
- Established directory structure per SDD §10 Repository Architecture:
  - `standard/` — NORMATIVE STANDARD region
  - `docs/` — DERIVED OPERATIONAL DOCS region
  - `references/` — REFERENCE MATERIAL region
  - `templates/` — TEMPLATES region
  - `examples/` — EXAMPLES region
- Placed SDD v0.4.0 as the authoritative normative document in `standard/SDD.md`.
- Created placeholder files for Phase-2 generated artifacts:
  - `standard/dependency-graph.md` (§45)
  - `standard/traceability-graph.md` (§48)
- Added repository metadata: README.md, LICENSE, VERSION, CHANGELOG.md, .gitignore.
- Completed Phase 2 governance foundation:
  - `standard/repository-constitution.md` (§10, §17, §40)
  - `standard/repository-rules.md` (§10, §49)
  - `standard/artifact-classification.md` (§11.1, §10.3)
  - `standard/artifact-registry.md` (§11, §24)

## [0.3.0] — SDD Revision

### Added
- Completion extension: appended architectural models §32–§41.
- Full document consistency pass (terminology, IDs, RFC 2119 wording, references).

## [0.2.0] — SDD Revision

### Added
- Review extension: appended architectural models §25–§31.

## [0.1.0] — SDD Initial

### Added
- Initial SDD with sections 1–24 and Appendices A–C.

---

*This changelog is a repository artifact. The SDD revision history (§0, Revision History table) is the authoritative source for SDD changes; this file mirrors it for repository-level tracking.*
