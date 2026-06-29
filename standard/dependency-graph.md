# Engineering Dependency Graph

> **Authority Class:** Generated (§11.1)
> **§45 Phase-2 Artifact:** Machine-readable dependency graph
> **Status:** PLACEHOLDER — structure seeded; full population deferred to tooling
> **Source:** Derived from §45 Dependency Graph declarations
> **Version:** 0.4.0

## About This File

This file is a **Phase-2 generated artifact** per §45 of the SDD:

> "§45 declares the standard's derivation dependencies; the generated machine-readable graph is a Phase-2 artifact."

It SHALL be regenerated from the authoritative standard content (§10, §45). It MUST NOT be hand-edited (§11.1, RA-4).

## Dependency Declaration (§45.2)

### Global Drivers

Sections depended on by all: §1–§9 (esp. §7 Principles), §42 Meta-Model, §46 Vocabulary.

### Cross-Cutting

Apply to all: §17 Governance, §18 Versioning, §19 Extension, §40 Integrity, §49 Consistency.

### Topological Layers

A section MAY depend only on equal-or-lower layers:

| Layer | Sections |
|---|---|
| **L0 Foundations** | §7, §42, §43, §44, §46 |
| **L1 Evidence/Knowledge** | §11, §14, §26, §28, §31, §47, §29, §48 |
| **L2 Initiation/Discovery** | §32, §33, §34, §25, §30 |
| **L3 Reasoning** | §35, §36, §37, §12, §13 |
| **L4 Assurance** | §15, §16, §38 |
| **L5 Gates** | §27, §41, §50 |
| **Cross** | §17, §18, §19, §40, §49 |

### Principal Dependency Table (Meta Layer)

| Section | Depends On | Produces | Required By |
|---|---|---|---|
| **§42 Meta-Model** | §7, §46 | entity set | all model sections |
| **§43 Object Model** | §42, §11 | object schema | §44, §48, §49 |
| **§44 Relationship Model** | §42, §43 | edge types | §45, §48, §49 |
| **§45 Dependency Graph** | §42, §44 | order | §50, governance |
| **§46 Vocabulary** | §7 | canonical terms | all sections, App. B |
| **§47 Information Model** | §28, §26 | transition rules | §16, §48 |
| **§48 Traceability Graph** | §43, §44, §29 | trace graph | §49, §50, App. C |
| **§49 Consistency Rules** | §43, §44, §48 | invariants | §41, §50 |
| **§50 Completeness Model** | §27, §41, §49 | completeness metrics | Mission close |

## Invariants

- **Acyclicity (DEP-2):** The dependency graph MUST be acyclic at the authority level.
- **Explicit Declaration (DEP-1):** Every architectural section MUST declare its dependencies.
- **Topological Order (DEP-3):** Derivation/execution order MUST respect the topological order.

## Population Status

| Element | Status | Notes |
|---|---|---|
| Layer definitions | POPULATED | §45.2 table transcribed |
| Meta-layer dependencies | POPULATED | §45.2 principal table transcribed |
| Full section-level graph | PENDING | All 50 sections × dependencies |
| Machine-readable format | PENDING | JSON/YML/GraphML serialization |
| Cycle validation | PENDING | Automated check per DEP-2 |

---

*Last updated: 2026-06-30. This is a generated artifact; edit the authoritative SDD (standard/SDD.md) and regenerate.*
