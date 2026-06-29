# Software Engineering Standard (SES)

## Status

| Field | Value |
|---|---|
| **Standard Version** | 0.4.0 |
| **Repository Phase** | Phase 2 — Repository Foundation |
| **SDD Status** | DRAFT — Awaiting review per §15 (Inspection, RV-2) |
| **Phase 2 Authority** | SDD v0.4.0 §10, §24, §45, §48 |

## What This Is

The Software Engineering Standard (SES) is the authoritative, vendor-independent, technology-independent engineering reference that governs how software engineering work is performed across all projects — from receipt of an unknown system, through understanding, modification, validation, and documentation, until maintenance or retirement.

The SES does not produce software. It governs the *process* by which software is understood, built, changed, validated, and evolved.

## Repository Structure

This repository is organized per the Repository Architecture defined in §10 of the SDD:

```
├── standard/        NORMATIVE STANDARD — the governing documents
├── docs/            DERIVED OPERATIONAL DOCS — SOP, stages, checklists (Phases 4-8)
├── references/      REFERENCE MATERIAL — the cited evidence base
├── templates/       TEMPLATES — artifact templates (Phase 8)
└── examples/        EXAMPLES — non-normative illustrations (Phase 9)
```

**Authority rule (§10.4):** The `standard/` region is the only region that may contain `MUST/SHALL` rules. All other regions derive their authority by citing the standard.

## How to Read This Standard

1. Start with `standard/SDD.md` — the Software Design Document (v0.4.0) is the current authoritative architecture.
2. All normative rules use RFC 2119 / RFC 8174 keywords (`MUST`, `SHALL`, `SHOULD`, `MAY`).
3. Every normative rule carries an evidence reference or an `UNSUPPORTED` marker (FR-11).
4. Requirement keywords are defined in §46 (Canonical Engineering Vocabulary).

## Versioning

This standard follows Semantic Versioning 2.0.0 (§18). See `VERSION` and `CHANGELOG.md`.

## Scope of This Repository (Phase 2)

This repository currently contains only the **Phase 2 foundation**:
- Repository metadata (README, LICENSE, VERSION, CHANGELOG)
- Directory structure per §10 architecture
- The frozen SDD v0.4.0 as the normative standard
- Placeholder files for Phase-2 generated artifacts (§45, §48)

**Not yet included** (deferred to later phases per §24):
- SOP, Stage Specifications, Checklists
- Templates
- Examples
- Engineering Workflows
- Validation Rules

---

*This README is a repository artifact, not a normative standard document. On any conflict, `standard/SDD.md` governs.*
