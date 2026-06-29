# Engineering Traceability Graph

> **Authority Class:** Generated (§11.1)
> **§48 Phase-2 Artifact:** Generated traceability graph
> **Status:** PLACEHOLDER — structure seeded; full population deferred to tooling
> **Source:** Derived from §48 Traceability Graph declarations
> **Version:** 0.4.0

## About This File

This file is a **Phase-2 generated artifact** per §48 of the SDD:

> "the generated graph is a Phase-2 artifact."

It SHALL be regenerated from the authoritative standard content (§43, §44, §48). It MUST NOT be hand-edited (§11.1, TRC-3, RA-4).

## Graph Architecture (§48)

### Node Types

Every engineering object (§43) is a node. Node types are §42.2 entities:

```
Mission → State → Stage → Operation → Evidence → Fact → Knowledge
→ Decision → Artifact → Implementation → Validation → Documentation → Repository
```

### Edge Types

Edges are §44.2 relationship types:

| Relationship | Direction | From → To |
|---|---|---|
| **depends_on** | directed · n:n | object → object |
| **produces** | directed · 1:n | Operation/Stage → Artifact/Evidence |
| **consumes** | directed · n:n | Operation → Artifact/Evidence |
| **owns** | directed · 1:n | Owner → object |
| **implements** | directed · 1:1+ | Implementation → Decision |
| **validates** | directed · n:1 | Validation → Implementation |
| **documents** | directed · n:1 | Documentation → object |
| **references** | directed · n:n | object → object |
| **supersedes** | directed · 1:1 | new → old |
| **derives_from** | directed · n:1 | Derived → Authoritative |
| **generated_from** | directed · n:1 | Generated → source |
| **verified_by** | directed · 1:n | Fact → Evidence/Validation |
| **reviewed_by** | directed · n:n | Artifact → Review |
| **approved_by** | directed · n:1 | Decision → Authority |
| **blocks** | directed · n:n | object → object |
| **requires** | directed · n:n | object → object |
| **contains** | directed · 1:n | container → member |
| **extends** | directed · n:1 | Extension → Core |

### Trace Directions (§48.2)

Each node SHALL support:

1. **Forward Trace** — downstream dependencies
2. **Backward Trace** — upstream provenance
3. **Impact Trace** — change propagation (§36)
4. **Dependency Trace** — depends_on/requires chain
5. **Evidence Trace** — verification and confidence (§26)
6. **Decision Trace** — decision rationale chain (§35)

## Normative Rules

- **TGR-1:** Every engineering object MUST be a node; no orphan objects.
- **TGR-2:** The graph MUST support all six trace directions bidirectionally.
- **TGR-3:** Node types are §43 objects; edge types are §44 relationships.
- **TGR-4:** This graph SHOULD be generated, not hand-maintained (TRC-3).
- **TGR-5:** Appendix C is a requirements-scoped view of this graph.

## Relationship to Appendix C

Appendix C (Requirements Traceability Index) links:
Principles → Requirements → Verification → Success Criteria

This graph generalizes Appendix C to all engineering objects (§43) and all relationship types (§44).

## Population Status

| Element | Status | Notes |
|---|---|---|
| Node type schema | POPULATED | §42.2 entities listed |
| Edge type schema | POPULATED | §44.2 relationships listed |
| Trace direction spec | POPULATED | §48.2 directions listed |
| Object instances | PENDING | All requirement IDs, decisions, etc. |
| Relationship instances | PENDING | All trace links |
| Machine-readable format | PENDING | Graph serialization |
| Orphan check (TGR-1) | PENDING | Automated validation |

---

*Last updated: 2026-06-30. This is a generated artifact; edit the authoritative SDD (standard/SDD.md) and regenerate.*
