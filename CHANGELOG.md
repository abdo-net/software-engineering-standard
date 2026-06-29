# Changelog

All notable changes to this standard are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).

## [0.4.0] — 2026-06-30

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
- **Completed Phase 2 governance foundation:**
  - `standard/repository-constitution.md` — Repository purpose, authority hierarchy, regions, document precedence, modification rules, artifact ownership, frozen areas, generated artifacts policy (§10, §11, §17, §18, §40).
  - `standard/repository-rules.md` — Naming conventions, directory ownership, immutability rules, generated file protection, authority boundaries, version control rules, extension rules (§10, §11, §17, §18, §19, §43, §49).
  - `standard/artifact-classification.md` — Official classification system: Authoritative, Derived, Generated, Reference, Template, Example (§11.1, §10.3, §10.4).
  - `standard/artifact-registry.md` — Canonical registry of 38+ artifacts with class, source, owner, lifecycle, and phase introduced (§10, §11, §24).

**Basis:** SDD §24 (Phase 2: "Concrete repository directory/file structure — Populates §10 architecture into a layout").

## [0.3.0] — SDD Revision

### Added
- Completion extension: appended architectural models §32–§41 (Engineering Mission Model, Engineering State Model, Engineering Operation Model, Engineering Decision Model, Engineering Impact Analysis Model, Engineering Comparison Model, Engineering Documentation Model, Repository Evolution Model, Engineering Integrity Rules, Repository Readiness Criteria).
- Full document consistency pass (terminology, IDs, RFC 2119 wording, references).

**Basis:** Final Phase-1 Completion Order; §18 VS-1/VS-2 (MINOR increment + changelog).

## [0.2.0] — SDD Revision

### Added
- Review extension: appended architectural models §25–§31 (Engineering Discovery Model, Evidence Confidence Model, Engineering Completion Criteria, Engineering Evidence Chain, Engineering Traceability Expansion, Reverse Engineering Architecture, Repository Knowledge Architecture).

**Basis:** Engineering Review Order; §18 VS-1/VS-2 (MINOR increment + changelog).

## [0.1.0] — SDD Initial

### Added
- Initial SDD with sections 1–24 and Appendices A–C.
- Vision, Problem Statement, Objectives, Scope, Non-Goals, Stakeholders, Engineering Principles, Functional/Non-Functional Requirements, Repository Architecture, Artifact Architecture, Engineering Lifecycle, Stage Model, Knowledge Model, Review Model, Validation Model, Governance Model, Versioning Strategy, Extension Policy, Success Criteria, Risks, Assumptions, Constraints, Future Work.
- Evidence Base (Appendix A), Glossary (Appendix B), Requirements Traceability Index (Appendix C).

**Basis:** Phase 1 assignment.

---

*This changelog is a repository artifact. The SDD revision history (§0, Revision History table) is the authoritative source for SDD changes; this file mirrors it for repository-level tracking.*
