# Software Design Document (SDD)

## Software Engineering Standard (SES)

---

| Field | Value |
|---|---|
| **Document Title** | Software Design Document for the Software Engineering Standard (SES) |
| **Document Type** | Software Design Document (SDD) |
| **Subject System** | The Software Engineering Standard (SES) itself |
| **Phase** | Phase 1 — Design the standard itself |
| **Document Status** | DRAFT — Awaiting review |
| **Document Version** | 0.4.0 |
| **Conforms To (format)** | IEEE Std 1016-2009 (Software Design Descriptions); ISO/IEC/IEEE 42010:2022 (Architecture description) |
| **Requirement Keywords** | RFC 2119 / RFC 8174 (MUST, MUST NOT, SHALL, SHALL NOT, SHOULD, SHOULD NOT, MAY, OPTIONAL) |
| **Authoring Discipline** | Engineering standards committee posture |

### Revision History

| Version | Status | Change | Basis |
|---|---|---|---|
| 0.1.0 | DRAFT | Initial SDD — 24 sections + Appendices A–C. | Phase 1 assignment |
| 0.2.0 | DRAFT | Review extension: appended architectural models §25–§31 (Engineering Discovery Model, Evidence Confidence Model, Engineering Completion Criteria, Engineering Evidence Chain, Engineering Traceability Expansion, Reverse Engineering Architecture, Repository Knowledge Architecture). No existing section was rewritten, restructured, renumbered, or removed; all existing requirement IDs are preserved. Backward-compatible additive change. | Engineering Review Order; §18 VS-1/VS-2 (MINOR increment + changelog), dogfooded |
| 0.3.0 | DRAFT | Completion extension: appended architectural models §32–§41 (Engineering Mission Model, Engineering State Model, Engineering Operation Model, Engineering Decision Model, Engineering Impact Analysis Model, Engineering Comparison Model, Engineering Documentation Model, Repository Evolution Model, Engineering Integrity Rules, Repository Readiness Criteria) making the standard executable; performed a full document consistency pass (terminology, IDs, RFC 2119 wording, forward/appendix/traceability references). No existing section rewritten, restructured, renumbered, or removed; all existing requirement IDs preserved. Backward-compatible additive change. | Final Phase-1 Completion Order; §18 VS-1/VS-2 (MINOR increment + changelog), dogfooded |
| 0.4.0 | DRAFT | Meta-architecture extension: appended §42–§50 (Engineering Meta-Model, Object Model, Relationship Model, Dependency Graph, Canonical Vocabulary, Information Model, Traceability Graph, Consistency Rules, Completeness Model) establishing the canonical architectural root, unified object/relationship/graph models, and repository-level structural integrity & completeness. Appendix B re-designated a derived view of §46. Full consistency pass performed (numbering, references, IDs, RFC 2119, relationship/dependency/object/vocabulary/traceability consistency). No existing section rewritten, restructured, renumbered, or removed; all existing requirement IDs preserved. Backward-compatible additive change. | Engineering Review Order — Phase 1 Final Completion; §18 VS-1/VS-2 (MINOR increment + changelog), dogfooded |

> **Reading note on authority of keywords.** Throughout this document the capitalized terms **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**, **SHOULD**, **SHOULD NOT**, **MAY**, and **OPTIONAL** are to be interpreted as described in **RFC 2119** as updated by **RFC 8174** (i.e., they carry their special meaning only when in uppercase). [Ref: RFC 2119; RFC 8174]

> **Evidence convention.** Every normative rule is followed by a bracketed reference to its evidence base, e.g. `[Ref: IEEE 1016-2009]`. Where a rule reflects converged industry practice that is real but **not** traceable to a formal standard, it is marked `[Ref: Converged practice — <source>]`. Where a claim cannot be supported by any citable source, it is explicitly marked **UNSUPPORTED** and is non-normative. Assumptions are never silently promoted to rules; they live only in §22.

> **Scope-of-phase note.** This SDD is the *architecture of the Standard*. It defines the **models and meta-models** that later phases populate. Sections that describe the Engineering Lifecycle (§12), Stage Model (§13), Knowledge Model (§14), Review Model (§15), and Validation Model (§16) define **frameworks and their rationale only**; the *full normative specification* of each is explicitly deferred to the Development Order phase named in that section. Specifying that detail here would violate the mandated phase boundaries and is therefore out of scope for Phase 1.

---

## Table of Contents

1. [Vision](#1-vision)
2. [Problem Statement](#2-problem-statement)
3. [Objectives](#3-objectives)
4. [Scope](#4-scope)
5. [Non-Goals](#5-non-goals)
6. [Stakeholders](#6-stakeholders)
7. [Engineering Principles](#7-engineering-principles)
8. [Functional Requirements](#8-functional-requirements)
9. [Non-Functional Requirements](#9-non-functional-requirements)
10. [Repository Architecture](#10-repository-architecture)
11. [Artifact Architecture](#11-artifact-architecture)
12. [Engineering Lifecycle](#12-engineering-lifecycle)
13. [Stage Model](#13-stage-model)
14. [Knowledge Model](#14-knowledge-model)
15. [Review Model](#15-review-model)
16. [Validation Model](#16-validation-model)
17. [Governance Model](#17-governance-model)
18. [Versioning Strategy](#18-versioning-strategy)
19. [Extension Policy](#19-extension-policy)
20. [Success Criteria](#20-success-criteria)
21. [Risks](#21-risks)
22. [Assumptions](#22-assumptions)
23. [Constraints](#23-constraints)
24. [Future Work](#24-future-work)
25. [Engineering Discovery Model](#25-engineering-discovery-model)
26. [Evidence Confidence Model](#26-evidence-confidence-model)
27. [Engineering Completion Criteria](#27-engineering-completion-criteria)
28. [Engineering Evidence Chain](#28-engineering-evidence-chain)
29. [Engineering Traceability Expansion](#29-engineering-traceability-expansion)
30. [Reverse Engineering Architecture](#30-reverse-engineering-architecture)
31. [Repository Knowledge Architecture](#31-repository-knowledge-architecture)
32. [Engineering Mission Model](#32-engineering-mission-model)
33. [Engineering State Model](#33-engineering-state-model)
34. [Engineering Operation Model](#34-engineering-operation-model)
35. [Engineering Decision Model](#35-engineering-decision-model)
36. [Engineering Impact Analysis Model](#36-engineering-impact-analysis-model)
37. [Engineering Comparison Model](#37-engineering-comparison-model)
38. [Engineering Documentation Model](#38-engineering-documentation-model)
39. [Repository Evolution Model](#39-repository-evolution-model)
40. [Engineering Integrity Rules](#40-engineering-integrity-rules)
41. [Repository Readiness Criteria](#41-repository-readiness-criteria)
42. [Engineering Meta-Model](#42-engineering-meta-model)
43. [Engineering Object Model](#43-engineering-object-model)
44. [Engineering Relationship Model](#44-engineering-relationship-model)
45. [Engineering Dependency Graph](#45-engineering-dependency-graph)
46. [Canonical Engineering Vocabulary](#46-canonical-engineering-vocabulary)
47. [Engineering Information Model](#47-engineering-information-model)
48. [Engineering Traceability Graph](#48-engineering-traceability-graph)
49. [Engineering Consistency Rules](#49-engineering-consistency-rules)
50. [Engineering Completeness Model](#50-engineering-completeness-model)
- [Appendix A — Evidence Base (Normative References)](#appendix-a--evidence-base-normative-references)
- [Appendix B — Glossary](#appendix-b--glossary)
- [Appendix C — Requirements Traceability Index](#appendix-c--requirements-traceability-index)

---

## 1. Vision

### 1.1 Vision Statement

The Software Engineering Standard (SES) **SHALL** be the authoritative, vendor-independent, technology-independent engineering reference that governs how software engineering work is performed across all future projects of this organization — from the first moment an unknown system is received, through understanding, modification, validation, and documentation, until the system is maintained years later or retired.

The SES does not produce software. It governs the *process* by which software is understood, built, changed, validated, and evolved. Projects are **users** of the standard; the standard is **superordinate** to every project.

### 1.2 What the Standard Aspires To Be

The SES aspires to be, for this organization, what a published engineering standard is for a regulated discipline: a stable, citable, evidence-based body of rules that survives the turnover of people, the replacement of tools, and the obsolescence of technologies.

The governing analogy is the relationship between an international standard (e.g., ISO/IEC/IEEE 12207 for software life cycle processes) and the projects that conform to it: the standard defines *what process properties must hold*; the project decides *how to realize them in its context*. [Ref: ISO/IEC/IEEE 12207:2017, which deliberately specifies process outcomes rather than a fixed method]

### 1.3 Durability Requirement

The SES **MUST** remain valid and usable even if every current AI system, IDE, vendor, programming language, and framework is replaced. The engineering process the SES describes is a property of the *discipline of software engineering*, not of any tool that assists it. [Ref: SWEBOK V3/V4 treats software engineering knowledge as discipline-level and tool-independent — IEEE Computer Society Guide to the Software Engineering Body of Knowledge]

> **Rationale.** The repository — not the conversation, not the tool, not the model — is the only permanent engineering artifact. Therefore the standard that governs engineering must reside in the repository and depend on nothing transient. This rationale is consistent with Lehman's observation that software in active use is subject to continuing change and that organizational/engineering knowledge decays unless it is externalized. [Ref: Lehman, "Programs, Life Cycles, and Laws of Software Evolution," Proc. IEEE, 1980]

---

## 2. Problem Statement

### 2.1 The Core Problem

Software engineering work performed across many projects, sessions, people, and tools loses **engineering continuity**. Each engagement reconstructs a different, often incomplete, mental model of the same system. Over time, implementations drift from their contracts, documentation drifts from implementation, and architectural intent is lost. The result is architectural decay that is no single person's fault and that no individual tool can prevent.

### 2.2 Documented Manifestations

The following are recognized, evidence-supported failure modes that the SES exists to counter:

- **P-1 — Continuing change and decay.** Software that is used must change; as it changes, its complexity increases unless deliberate work is done to reduce it. Without an externalized, governing process, this manifests as decay. [Ref: Lehman's Laws of Software Evolution — Laws of Continuing Change and Increasing Complexity]
- **P-2 — Loss of decision rationale.** Decisions are made and then forgotten; people leave, the rationale is not recorded, and later engineers cannot tell which constraints are essential. [Ref: Nygard, "Documenting Architecture Decisions," 2011 — the problem ADRs were created to solve]
- **P-3 — Organizational coupling and divergence.** System structure mirrors the communication structure of the organization that builds it; uncoordinated, session-by-session work produces interfaces that diverge. [Ref: Conway, "How Do Committees Invent?", Datamation, 1968]
- **P-4 — Drift between artifacts.** API diverges from core, frontend from API, schema from repository, documentation from implementation — none intentionally wrong. [Ref: Converged practice — the "documentation drift" problem; Forsgren/Humble/Kim, *Accelerate*, on the cost of unmanaged change]
- **P-5 — Tool/vendor volatility.** The tools that assist engineering (including AI systems) change faster than engineering principles do; a process coupled to a specific tool dies with that tool. [Ref: Converged practice — vendor-neutrality is a standing principle of open standards bodies (IETF, ISO)]

### 2.3 Why Existing Solutions Are Insufficient (in this organization's context)

- File access alone (e.g., SSH, RAG retrieval) provides *files*, not *reconstructed engineering understanding* — it cannot recover why architecture exists, which contracts cannot change, or which invariants must hold. [Ref: Converged practice — Chikofsky & Cross, "Reverse Engineering and Design Recovery," IEEE Software, 1990, distinguishes raw artifacts from *recovered design*]
- Larger context windows and tool memory defer the problem rather than solving it: conversation is transient, the repository is permanent. **UNSUPPORTED** as a formally-cited claim about specific tools; supported in principle by the general engineering observation that durable knowledge must be externalized into version-controlled artifacts. [Ref: Converged practice — docs-as-code; Winters et al., *Software Engineering at Google*, 2020]

### 2.4 Problem Statement (Formal)

> There exists no single, evidence-based, vendor-independent engineering standard, resident in the repository and superordinate to all projects, that defines how software engineering work MUST be performed such that engineering continuity, decision rationale, contract integrity, and architectural intent are preserved across people, sessions, tools, and years.

The SES exists to be that standard.

---

## 3. Objectives

Each objective is stated to be **testable** (per the document-wide requirement that every requirement be verifiable). Objective IDs are `OBJ-n`. Verification of objectives is via the Success Criteria in §20.

| ID | Objective | Verification (see §20) |
|---|---|---|
| **OBJ-1** | Provide a single authoritative engineering standard that governs all future projects regardless of language, framework, architecture, or platform. | SC-1: A project of an arbitrary technology stack can be assessed for conformance using only the SES. |
| **OBJ-2** | Base every normative rule on citable engineering evidence, or mark it UNSUPPORTED. | SC-2: 100% of normative rules carry an evidence reference or an UNSUPPORTED marker. |
| **OBJ-3** | Reconstruct and formalize *existing proven practice*, not invent methodology. | SC-3: Each practice traces to at least one source in the approved evidence base (Appendix A). |
| **OBJ-4** | Remain valid under total replacement of any vendor, tool, language, or AI system. | SC-4: No normative rule names or requires a specific commercial product, language, or AI model. |
| **OBJ-5** | Make the repository the permanent engineering memory; nothing essential lives only in conversation or tooling. | SC-5: Every authoritative artifact class is defined as a version-controlled repository file. |
| **OBJ-6** | Make every engineering claim **traceable to evidence in the subject repository** (provenance), preventing assumption-as-fact. | SC-6: The Knowledge Model (§14) requires provenance for every recorded engineering fact. |
| **OBJ-7** | Make conformance **objectively verifiable**, not a matter of opinion. | SC-7: The Validation Model (§16) defines verification methods for each requirement class. |
| **OBJ-8** | Make the standard **evolvable under governance** without becoming unstable. | SC-8: Versioning (§18) and Governance (§17) define a controlled change path; projects cannot mutate the standard ad hoc (§19). |
| **OBJ-9** | Be readable and executable by **both human engineers and automated agents** without privileging either. | SC-9: All artifacts are plain-text, structured, and tool-agnostic (NFR class "Interoperability"). |

> **Rationale.** Objectives are deliberately phrased as outcomes with named verification, in keeping with the standards-engineering principle that a requirement that cannot be verified is not a requirement. [Ref: ISO/IEC/IEEE 29148:2018, §5.2.5 — requirements shall be verifiable]

---

## 4. Scope

### 4.1 In Scope

The SES governs the **engineering process** applied to software systems. Specifically, the SES **SHALL** define:

- **S-1** The engineering lifecycle from receipt of an unknown system to its maintenance and retirement (framework in §12; full specification deferred to Phase 3).
- **S-2** The artifacts that engineering work produces and consumes, and their authority classification (framework in §11; full specification deferred to Phase 4).
- **S-3** The stages of engineering work and their entry/exit conditions (framework in §13; full specification deferred to Phase 5).
- **S-4** The review process applied to engineering work and to the standard itself (framework in §15).
- **S-5** The validation process by which conformance is verified (framework in §16; full specification deferred to Phase 6).
- **S-6** The governance process by which the standard itself is changed (framework in §17; full specification deferred to Phase 7).
- **S-7** The knowledge model by which engineering facts, decisions, contracts, and invariants are recorded with provenance (framework in §14).

### 4.2 Domains the SES Must Cover

The SES **MUST** be applicable, without modification of its core, to at least the following engineering contexts, because these are the declared user systems of the standard:

backend APIs; frontend applications; infrastructure projects; ERP systems; analysis systems; RADIUS / network servers; reverse engineering; legacy modernization; and system integration. [Ref: Mission Statement, this initiative]

### 4.3 Scope Boundary Statement

The SES governs **how** engineering is performed. It does **not** govern **what product** is built (that is each project's concern), nor **which business outcomes** are pursued (that is the organization's concern). This boundary mirrors the standard/project separation in §1.2. [Ref: ISO/IEC/IEEE 12207:2017 — process standard, not product standard]

### 4.4 Phase-1 Document Scope

The deliverable of the current assignment is **exactly one artifact**: this `SDD.md`. The SOP, Stage Specifications, Templates, Checklists, Workflows, Examples, and all other repository files are **out of scope for Phase 1** and **MUST NOT** be produced in this phase. [Ref: Development Order, this initiative]

---

## 5. Non-Goals

The following are explicitly **out of scope** for the SES. Declaring non-goals is a recognized design-document discipline because unstated non-goals are a primary source of scope creep. [Ref: Converged practice — Google design-doc convention, *Software Engineering at Google*, 2020, §"Goals and Non-Goals"]

- **NG-1** The SES is **NOT** a methodology invention. It reconstructs proven practice; it does not create a novel framework. [Ref: Mission Statement]
- **NG-2** The SES is **NOT** optimized for any AI system, nor for any specific tool, and **MUST NOT** be. (§7 Principle PR-3.)
- **NG-3** The SES is **NOT** a product specification, requirements document, or design document for any user system (Radius1, SAS4, ERP, etc.). Those are produced *by projects using* the SES.
- **NG-4** The SES is **NOT** a coding standard, style guide, or language convention. Language-specific conventions are an *extension point* (§19), not part of the core.
- **NG-5** The SES does **NOT** prescribe a single fixed software development methodology (e.g., it does not mandate Scrum, Waterfall, or a specific branching model) where the evidence base shows multiple valid context-dependent approaches; instead it requires that the chosen approach satisfy stated process outcomes. [Ref: ISO/IEC/IEEE 12207:2017; Boehm & Turner, *Balancing Agility and Discipline*, 2003]
- **NG-6** The SES does **NOT** guarantee project success; it raises the floor of engineering rigor. Success depends on factors outside process. **UNSUPPORTED** to claim otherwise.
- **NG-7** Phase 1 does **NOT** define implementation, repository file layout beyond architecture, templates, or examples. (Per Development Order.)

---

## 6. Stakeholders

Stakeholders and their concerns are identified per **ISO/IEC/IEEE 42010:2022**, which requires an architecture description to identify stakeholders and the concerns the architecture must address. [Ref: ISO/IEC/IEEE 42010:2022, §5.3]

| ID | Stakeholder | Primary Concerns | Addressed By |
|---|---|---|---|
| **STK-1** | **Standard Owner / Authority** (the organization adopting SES) | Authority, durability, evidence basis, governance integrity | §1, §2, §17, §18 |
| **STK-2** | **Engineers (human)** applying the standard on projects | Clarity, applicability across stacks, testable rules, low ambiguity | §7, §8, §9, §12–§16 |
| **STK-3** | **Automated agents** (AI systems, CI tools) executing or checking the standard | Machine-readability, determinism, unambiguous verification criteria | §9 (NFR), §14, §16 |
| **STK-4** | **Reviewers / Auditors** of engineering work | Objective conformance criteria, traceability, review process | §15, §16, Appendix C |
| **STK-5** | **Project teams** (the user systems: Radius1, SAS4, ERP, etc.) | Extensibility for their context without forking the standard | §19 |
| **STK-6** | **Maintainers of the standard** | Controlled evolution, backward compatibility, change provenance | §17, §18 |
| **STK-7** | **Future engineers** inheriting systems years later | Preserved rationale, contracts, invariants; continuity | §2, §14 |
| **STK-8** | **External certifiers / partners** (potential) | Recognizable conformance to mainstream standards (IEEE/ISO) | §1.2, Appendix A |

> **Rationale for including automated agents as first-class stakeholders (STK-3).** The standard must be followed by humans *and* machines without privileging either (OBJ-9). Treating agents as stakeholders — not as authors — keeps the standard tool-independent (NG-2) while ensuring it is mechanically checkable. The standard is *authored for engineering correctness*; agents are *users*, never the *measure*, of correctness. [Ref: Converged practice — docs-as-code and "executable specifications," Fowler]

---

## 7. Engineering Principles

These principles are the **constitutional** foundation of the SES. Every functional and non-functional requirement traces to at least one principle. Principles are stated normatively and carry evidence.

| ID | Principle | Statement | Evidence |
|---|---|---|---|
| **PR-1** | **Evidence over opinion** | Every normative rule **MUST** be supported by citable engineering evidence, or marked UNSUPPORTED. | SWEBOK; OBJ-2. The discipline of basing rules on a recognized body of knowledge. [Ref: SWEBOK V3/V4] |
| **PR-2** | **Reconstruct, do not invent** | The SES **MUST** formalize existing proven practice rather than create novel methodology. | [Ref: Chikofsky & Cross, 1990 — design *recovery*; Mission Statement] |
| **PR-3** | **Vendor / tool / language / AI independence** | No normative rule **SHALL** depend on a specific vendor, tool, language, framework, or AI model. | [Ref: Converged practice — IETF/ISO vendor-neutrality; OBJ-4] |
| **PR-4** | **Repository as permanent memory** | Authoritative engineering knowledge **MUST** reside in version-controlled repository artifacts, never solely in conversation or tooling. | [Ref: Winters et al., *SE at Google* (docs-as-code); Lehman (externalized knowledge)] |
| **PR-5** | **Provenance / traceability** | Every recorded engineering fact, decision, and contract **MUST** be traceable to its source evidence. | [Ref: ISO/IEC/IEEE 29148:2018 (traceability); Chikofsky & Cross (provenance of recovered design)] |
| **PR-6** | **Single source of truth; derived artifacts are generated** | For any fact, exactly one artifact **SHALL** be authoritative; all other representations **MUST** be derived/generated from it and **MUST NOT** be edited by hand. | [Ref: Converged practice — docs-as-code; Twelve-Factor (config); ADR immutability, Nygard] |
| **PR-7** | **Verifiability** | Every requirement **MUST** be stated such that conformance can be objectively verified. | [Ref: ISO/IEC/IEEE 29148:2018, §5.2.5] |
| **PR-8** | **Separation of concerns between phases of work** | Distinct engineering responsibilities (e.g., execution vs. validation; design vs. implementation) **MUST NOT** be merged. | [Ref: ISO/IEC/IEEE 1012-2016 (V&V as independent activity); IEEE 1028-2008] |
| **PR-9** | **Determinism / reproducibility** | Given the same inputs (repository, commit, mission), the engineering process **SHOULD** produce the same artifacts and conformance verdict. | [Ref: Converged practice — reproducible builds; hermetic/deterministic engineering, *SE at Google*]. Marked SHOULD, not MUST, because full determinism over human/creative steps is **UNSUPPORTED** as universally achievable. |
| **PR-10** | **Controlled evolution** | The standard **MUST** change only through governance and only on verified evidence; projects **MUST NOT** mutate the standard. | [Ref: §17; semantic versioning discipline] |
| **PR-11** | **Minimal but sufficient** | The standard **SHOULD** specify the least that is necessary to achieve its objectives, deferring context-specific detail to extension points. | [Ref: Converged practice — "as simple as possible," arc42 minimalism; ISO 12207 outcome-based specification] |
| **PR-12** | **Context-sensitivity over dogma** | Where the evidence base shows multiple valid approaches, the SES **MUST** present them, compare them, and bind the choice to context rather than mandating one. | [Ref: Boehm & Turner, *Balancing Agility and Discipline*, 2003] |

> **Conflict-resolution rule among principles.** When two principles conflict in a concrete case, **PR-1 (evidence)** and **PR-7 (verifiability)** take precedence, because the standard's authority derives from them. This precedence is itself a design decision; its rationale is that an unverifiable or unevidenced rule cannot be authoritative regardless of its other merits. [Ref: PR-1; PR-7]

---

## 8. Functional Requirements

Functional requirements (`FR-n`) describe **what the standard, as an artifact system, must do or contain**. Each is testable and traces to a principle and an objective. Verification methods: **I** = Inspection, **A** = Analysis, **D** = Demonstration, **T** = Test (per ISO/IEC/IEEE 29148 verification method taxonomy). [Ref: ISO/IEC/IEEE 29148:2018]

| ID | Requirement | Traces To | Verify |
|---|---|---|---|
| **FR-1** | The SES **SHALL** define a complete engineering lifecycle covering: receipt of an unknown system, understanding, reverse engineering/reconstruction, analysis, planning, implementation, validation, documentation, maintenance, evolution, and retirement. | OBJ-1, PR-2 | I |
| **FR-2** | The SES **SHALL** define a closed set of **artifact classes**, each with: purpose, authority classification (authoritative / derived / generated), owner, and lifecycle. | OBJ-5, PR-6 | I |
| **FR-3** | The SES **SHALL** classify every artifact as **authoritative**, **derived**, or **generated**, and **SHALL** state that generated/derived artifacts **MUST NOT** be hand-edited. | PR-6 | I |
| **FR-4** | The SES **SHALL** define **stages** of engineering work, each with explicit **entry criteria**, **activities**, **exit criteria**, **produced evidence**, and **verification criteria**. | OBJ-7, PR-7 | I |
| **FR-5** | The SES **SHALL** define a **knowledge model** that records engineering facts, decisions (ADR-style), contracts, and invariants, each with mandatory **provenance** to source evidence. | OBJ-6, PR-5 | I |
| **FR-6** | The SES **SHALL** define a **review model** identifying review types (e.g., inspection, technical review, walkthrough, audit) and when each applies. | STK-4, PR-8 | I |
| **FR-7** | The SES **SHALL** define a **validation model** specifying, for each requirement class, an objective verification method and pass/fail criteria. | OBJ-7, PR-7 | I |
| **FR-8** | The SES **SHALL** define a **governance model** specifying how the standard is proposed, reviewed, approved, versioned, and superseded, and **SHALL** prohibit projects from modifying the core standard. | OBJ-8, PR-10 | I |
| **FR-9** | The SES **SHALL** define a **versioning strategy** with a defined compatibility contract for consuming projects. | OBJ-8, PR-10 | I |
| **FR-10** | The SES **SHALL** define an **extension policy** allowing projects to add context-specific rules (e.g., language conventions) **without** modifying the core. | STK-5, PR-11 | I |
| **FR-11** | Every normative rule in the SES **SHALL** carry an evidence reference or an explicit **UNSUPPORTED** marker. | OBJ-2, PR-1 | A |
| **FR-12** | The SES **SHALL** present, compare, and context-bind **competing approaches** wherever the evidence base shows more than one valid practice. | PR-12 | I |
| **FR-13** | The SES **SHALL** be expressed entirely in **plain-text, structured, version-controllable** form, with no dependency on a proprietary format or tool to be read or checked. | OBJ-9, PR-3 | D |
| **FR-14** | The SES **SHALL** maintain a **requirements traceability** mechanism linking principles → requirements → verification. | PR-5, PR-7 | I |
| **FR-15** | The SES **SHALL** define how **conformance of a project** to the standard is asserted, evidenced, and recorded (a conformance/certification concept). | OBJ-7 | I |
| **FR-16** | The SES core **MUST NOT** contain any rule that names a specific commercial product, programming language, framework, or AI model as a requirement. | OBJ-4, PR-3 | A |
| **FR-17** | The SES **SHALL** be organized as a repository whose structure separates: the standard, derived operational documents, references, templates, and examples (architecture in §10; population deferred to later phases). | OBJ-5 | I |

> **Note on FR-1, FR-4, FR-5, FR-6, FR-7, FR-8.** These require the *existence and shape* of the respective models. Their **full normative content** is produced in later Development-Order phases (3–7). This SDD satisfies them at the architectural level (§12–§17) and **MUST NOT** be read as already specifying their detail.

---

## 9. Non-Functional Requirements

Non-functional requirements (`NFR-n`) constrain the **qualities** of the standard. The quality categories are drawn from **ISO/IEC 25010** (product quality model), adapted from "software product" to "standard as product." [Ref: ISO/IEC 25010:2011 / :2023] Each NFR states a **measure** so it is testable (PR-7).

| ID | Quality | Requirement | Measure / Test |
|---|---|---|---|
| **NFR-1** | **Tool/vendor independence** (Portability) | The standard **MUST** be fully usable with only a text editor and version control. | Test: standard is read, navigated, and conformance-checked using no proprietary tool. (D) |
| **NFR-2** | **Technology independence** (Portability) | No core rule **MAY** assume a language, framework, runtime, or architecture style. | Analysis: zero core rules reference a specific technology. (A) |
| **NFR-3** | **Evidence integrity** (Functional correctness) | ≥ 99% of normative rules carry a valid evidence reference; the remainder are explicitly UNSUPPORTED. Target is 100%; 99% tolerates pending citation verification. | Analysis: count of unmarked, unevidenced rules = 0. (A) |
| **NFR-4** | **Unambiguity** (Maintainability/Analysability) | Every requirement uses RFC 2119 keywords and has exactly one defensible interpretation. | Review: reviewer cannot produce a second valid reading. (I) |
| **NFR-5** | **Verifiability** (Testability) | Every requirement has a stated verification method (I/A/D/T). | Inspection: requirements with no method = 0. (I) |
| **NFR-6** | **Machine-readability** (Interoperability) | The standard's structure **SHOULD** be parseable by automated tooling (consistent headings, IDs, tables). | Demonstration: an automated parser extracts all requirement IDs. (D) |
| **NFR-7** | **Durability** (Reliability/Maturity) | The standard **MUST** remain valid under replacement of any tool/vendor/AI; no rule's validity depends on a transient external service. | Analysis: removal of any named tool from context invalidates 0 core rules. (A) |
| **NFR-8** | **Traceability** (Maintainability) | Every requirement is traceable forward (to verification) and backward (to principle/objective). | Inspection: Appendix C completeness. (I) |
| **NFR-9** | **Stability / controlled change** (Maintainability/Modifiability) | Changes to the standard **MUST** follow governance + semantic versioning; no silent change. | Inspection: every change has a version bump + changelog + rationale. (I) |
| **NFR-10** | **Readability for dual audience** (Usability) | The standard **MUST** be comprehensible to both a competent human engineer and an automated agent without privileging either. | Review: human reviewer + automated extraction both succeed. (I/D) |
| **NFR-11** | **Internal consistency** (Functional correctness) | No two normative rules **MUST** contradict; conflicts are resolved by stated precedence (PR conflict rule). | Analysis: contradiction scan returns 0 unresolved conflicts. (A) |
| **NFR-12** | **Minimality** (Maintainability) | The standard **SHOULD** contain no rule that is not necessary to meet an objective. | Review: each rule traces to ≥1 objective. (I) |
| **NFR-13** | **Longevity of references** (Maintainability) | Evidence references **SHOULD** prefer durable, citable sources (standards, books, archival papers) over volatile URLs. | Inspection: ratio of durable to volatile references. (I) |

> **Rationale for ISO/IEC 25010 as the quality frame.** Using a recognized product-quality taxonomy (rather than an ad-hoc list) ensures the standard's own qualities are themselves evidence-based and comparable to mainstream engineering practice. The adaptation from "software product" to "standard as product" is a documented technique: ISO 25010 is routinely applied to non-code work products. [Ref: ISO/IEC 25010] The application to a *standard document* specifically is a reasonable extension and is marked **converged practice**, not formal standard.

---

## 10. Repository Architecture

> **Phase boundary.** §10 defines the **architectural principles** of the repository (the *why* and the *separation*). The **concrete directory/file layout** is the deliverable of **Phase 2** and is **NOT** specified here. [Ref: Development Order]

### 10.1 Architectural Drivers

The repository architecture is driven by: PR-4 (repository as memory), PR-6 (single source of truth), FR-17 (separation of artifact kinds), and NFR-1/NFR-7 (tool/vendor independence and durability).

### 10.2 Architectural Decisions (with rationale)

- **RA-1 — The standard is plain text under version control.** The repository **MUST** store the standard as plain-text, structured files (e.g., Markdown) in a version-control system. *Rationale:* satisfies NFR-1, NFR-7, PR-4; version control provides history, review, and provenance "for free." [Ref: Converged practice — docs-as-code, *SE at Google*]
- **RA-2 — Authority layering.** The repository **MUST** separate, at the top architectural level, the following *kinds* of content, each in its own region: (a) **Normative Standard** (this SDD and its successors), (b) **Derived Operational Documents** (SOP, stages, checklists — later phases), (c) **Reference Material** (the evidence base), (d) **Templates**, (e) **Examples**. *Rationale:* prevents the most common documentation failure — mixing authoritative and derived content so that readers cannot tell which governs (PR-6). [Ref: Converged practice — arc42 separation of concerns; ISO/IEC/IEEE 26515 doc structuring]
- **RA-3 — One fact, one authoritative location.** No fact **SHALL** be authoritative in two places. Cross-references **MUST** point to the single authoritative artifact. *Rationale:* PR-6; eliminates drift (P-4). [Ref: Converged practice — DRY for documentation; Twelve-Factor]
- **RA-4 — Derived/generated content is regenerable.** Any derived or generated artifact **MUST** be reproducible from its authoritative source by a documented, tool-agnostic procedure. *Rationale:* PR-6, NFR-7; a derived artifact that cannot be regenerated has silently become a second source of truth. [Ref: Converged practice — generated docs, OpenAPI/codegen patterns]
- **RA-5 — Standard precedes derivation.** The normative standard region is **authoritative over** all other regions; in any conflict, the standard governs. *Rationale:* PR-10, §1.2 superordination.

### 10.3 Architectural View (logical)

```
Repository (permanent engineering memory)
│
├── NORMATIVE STANDARD            (authoritative; governs everything)
│      └── SDD (this document) → later: Lifecycle, Stages, Validation, Governance specs
│
├── DERIVED OPERATIONAL DOCS      (generated/derived from the standard) [Phases 4–8]
│      └── SOP, Stage Specs, Checklists, Review Rules, Validation Rules
│
├── REFERENCE MATERIAL            (the cited evidence base) [supporting]
│
├── TEMPLATES                     (derived; instantiate artifacts) [Phase 8]
│
└── EXAMPLES                      (illustrative; non-normative) [Phase 9]
```

*This diagram is architectural and illustrative; it is **not** the Phase-2 directory specification.*

### 10.4 Authority Rule

The **Normative Standard** region is the only region that may contain `MUST/SHALL` rules. Operational documents, templates, and examples **MUST** derive their authority by citing the standard and **MUST NOT** introduce new normative rules. [Ref: PR-6, RA-5]

---

## 11. Artifact Architecture

### 11.1 The Artifact Authority Model

Every artifact the SES recognizes **SHALL** be classified into exactly one of three authority classes. This tri-class model is the structural core that prevents documentation drift. [Ref: Converged practice — distinction between source-of-truth and generated artifacts: Nygard (ADR immutability), Twelve-Factor (config), docs-as-code]

| Class | Definition | Editing Rule | Examples (illustrative, defined fully in Phase 4) |
|---|---|---|---|
| **Authoritative** | The single source of truth for some fact or decision. Hand-authored. | **MAY** be edited by humans through review + governance. | The SDD; ADRs; contract specifications; invariants register |
| **Derived** | Produced by transforming one or more authoritative artifacts; carries no independent truth. | **MUST NOT** be hand-edited; **MUST** be regenerated from source. | SOP derived from lifecycle; checklists derived from stages |
| **Generated** | Mechanically produced from authoritative sources or from the system under engineering. | **MUST NOT** be hand-edited; **MUST** be reproducible. | Dependency graphs; API reference from contracts; traceability indexes |

### 11.2 Mandatory Artifact Metadata

Every artifact **SHALL** carry, at minimum: a unique identifier, an authority class (§11.1), an owner, a version, a status, and — for derived/generated artifacts — a pointer to the authoritative source(s) from which it is produced. *Rationale:* PR-5 (provenance), PR-6 (single source of truth). [Ref: ISO/IEC/IEEE 26515; IEEE 1016-2009 §"identification"]

### 11.3 Special Artifact Types (architectural placeholders)

The following artifact *types* are recognized as constitutionally important and **SHALL** be specified in Phase 4. They are named here only to fix their authority class:

- **Architecture Decision Record (ADR)** — Authoritative; **immutable once accepted** (superseded, never edited). [Ref: Nygard, 2011]
- **Contract Specification** — Authoritative; the agreed interface + semantics across a boundary. [Ref: OpenAPI/AsyncAPI/proto; Meyer, Design by Contract]
- **Invariant Register** — Authoritative; the constraints that **MUST** remain true.
- **Provenance Record** — links any recorded fact to its source evidence. [Ref: PR-5]
- **Traceability Index** — Generated; links principles → requirements → verification. [Ref: ISO/IEC/IEEE 29148]

### 11.4 Forward Reference

The **full catalog** of artifacts, with templates and field-level schemas, is the deliverable of **Phase 4 (Define artifacts)** and **Phase 8 (Templates)**. §11 fixes only the *architecture* (the three classes, metadata, and authority rules).

---

## 12. Engineering Lifecycle

> **Phase boundary.** This section defines the **lifecycle model and its rationale** as the architecture of the standard. The **full normative specification of each lifecycle phase** (objectives, inputs, activities, outputs, evidence, verification, tools, mistakes, references) is the deliverable of **Phase 3 (Define engineering lifecycle)**. [Ref: Development Order]

### 12.1 Lifecycle Frame

The SES **SHALL** adopt a lifecycle that is **process-based and outcome-defined**, not method-prescriptive, consistent with **ISO/IEC/IEEE 12207:2017**. The lifecycle **SHALL** describe *what outcomes and evidence each phase produces*, leaving *how* to the project (PR-12). [Ref: ISO/IEC/IEEE 12207:2017]

### 12.2 Canonical Phase Set (architectural)

The lifecycle **SHALL** comprise the following phases. The ordering is a **dependency ordering of artifacts**, **not** a claim that work is performed once, linearly. Iteration is expected and is supported by the evidence base. [Ref: Demeyer/Ducasse/Nierstrasz, *Object-Oriented Reengineering Patterns*, 2002; Chikofsky & Cross, 1990]

```
Unknown System
   ↓
Understanding  ───────────────► (recover the system as it actually is)
   ↓
Reverse Engineering / Reconstruction
   ↓
Analysis (dependencies, execution flow, contracts, gaps)
   ↓
Planning (design docs, ADRs, risk, sequencing)
   ↓
Implementation (small, isolated, reviewed, reversible changes)
   ↓
Validation (static → unit → integration → contract → regression → system → runtime → review)
   ↓
Documentation (authoritative + generated; docs-as-code)
   ↓
Maintenance (corrective / adaptive / perfective / preventive)
   ↓
Evolution (controlled change under fitness/governance)
   ↓
Retirement (deliberate disposal, archival, deprecation)
```

### 12.3 Normative Properties of the Lifecycle

- **LC-1** Each phase **SHALL** define explicit **inputs**, **outputs**, **evidence produced**, and **verification criteria**. [Ref: ISO/IEC/IEEE 12207 process structure]
- **LC-2** No phase **MAY** assert a conclusion that is not backed by evidence from the subject system (PR-5). [Ref: Chikofsky & Cross; Feathers (characterization tests)]
- **LC-3** The lifecycle **SHALL** treat understanding/analysis as **iterative**, not single-pass. The linear diagram is an artifact-dependency DAG, **not** a waterfall. Asserting a fixed single-pass sequence is **UNSUPPORTED** as universal practice. [Ref: Demeyer et al., 2002; ISO 12207 non-prescription of sequence]
- **LC-4** Maintenance **SHALL** recognize the four maintenance categories: corrective, adaptive, perfective, preventive. [Ref: ISO/IEC/IEEE 14764:2022; Lientz & Swanson, 1980]
- **LC-5** Retirement **SHALL** be an explicit, planned phase, not an implicit event (data archival, consumer notification, deprecation policy). [Ref: ISO/IEC/IEEE 12207 Disposal process; RFC 8594 (Sunset header) for API deprecation]

### 12.4 Competing Approaches (presented per PR-12, FR-12)

The Phase-3 lifecycle specification **MUST** present and context-bind, rather than dogmatically choose between, the following documented tensions:

- **Plan-driven / architecture-first** vs **evolutionary / emergent design**. Context decides: high cost-of-change/regulated/safety-critical favors architecture-first; high-uncertainty/reversible favors evolutionary. [Ref: Bass/Clements/Kazman, *Software Architecture in Practice*; Ford/Parsons/Kua, *Building Evolutionary Architectures*; reconciliation: Boehm & Turner, 2003]
- **Rewrite** vs **incremental modernization (Strangler Fig)**. Incremental is the documented default at scale. [Ref: Fowler, "StranglerFigApplication"; Brodie & Stonebraker, *Migrating Legacy Systems*, 1995]
- **Monolith-first** vs **microservices**. [Ref: Fowler, "MonolithFirst"; Newman, *Building Microservices*, 2nd ed.]

---

## 13. Stage Model

> **Phase boundary.** §13 defines the **meta-model of a stage**. The **catalog of concrete stages and their full specifications** is the deliverable of **Phase 5 (Define stages)**. [Ref: Development Order]

### 13.1 What a Stage Is

A **stage** is a bounded unit of engineering work within the lifecycle, defined by **gates**. The SES adopts an **entry/exit-criteria (gated) stage model**, consistent with stage-gate and phase-entry/exit conventions in mainstream process standards. [Ref: ISO/IEC/IEEE 12207 (activities with outcomes); IEEE 1028 (review as a gate)]

### 13.2 Mandatory Stage Schema

Every stage specified in Phase 5 **SHALL** define, at minimum:

| Field | Meaning | Evidence basis |
|---|---|---|
| **Entry Criteria** | Preconditions that **MUST** hold before the stage may begin | Stage-gate practice |
| **Inputs** | Authoritative artifacts consumed | ISO 12207 |
| **Activities** | Work performed | ISO 12207 |
| **Outputs** | Artifacts produced, with authority class | §11 |
| **Evidence Produced** | Verifiable evidence of the work | PR-5 |
| **Exit Criteria** | Postconditions that **MUST** hold to leave the stage | Stage-gate practice |
| **Verification Criteria** | How exit is objectively checked | PR-7, §16 |
| **Review Type** | Which review (§15) gates the stage | IEEE 1028 |

### 13.3 Normative Stage Rules

- **SG-1** A stage **MUST NOT** be declared complete unless its **exit criteria are verified** by the verification method named in its schema. [Ref: PR-7; IEEE 1028]
- **SG-2** Stage outputs **MUST** be classified per the Artifact Authority Model (§11). [Ref: PR-6]
- **SG-3** A stage **MAY** be re-entered (iteration); re-entry **MUST** be recorded. [Ref: LC-3]
- **SG-4** Separation of duties: where a stage produces a change and another verifies it, the SES **SHOULD** keep these as distinct responsibilities. [Ref: PR-8; ISO/IEC/IEEE 1012 (independent V&V)]

---

## 14. Knowledge Model

> This section is **architecturally complete** for Phase 1 because the knowledge model is constitutional to the standard's purpose (P-2, OBJ-6). Detailed templates are deferred to Phase 4/8.

### 14.1 Purpose

The Knowledge Model defines how engineering knowledge is **captured, structured, and preserved** so that it survives people, sessions, and tools (P-2, P-3, PR-4).

### 14.2 Knowledge Categories

The SES **SHALL** recognize these categories of durable engineering knowledge, each an authoritative artifact (§11):

| Category | Definition | Evidence basis |
|---|---|---|
| **Facts** | Verified statements about the system, each with provenance | Chikofsky & Cross (recovered facts); Moose/Rigi fact-extraction tradition |
| **Decisions** | Architecture/engineering decisions, ADR-format, immutable once accepted | Nygard, 2011 |
| **Contracts** | Agreed interfaces + semantics across boundaries | OpenAPI/AsyncAPI/proto; Meyer (Design by Contract) |
| **Invariants** | Constraints that MUST remain true | Converged practice — invariants/contracts; Meyer |
| **Rationale** | Why a decision was made; alternatives considered | Google design-doc convention; ADR "consequences" |
| **Provenance** | Link from any fact to its source evidence | PR-5; ISO/IEC/IEEE 29148 traceability |

### 14.3 Normative Knowledge Rules

- **KN-1** Every recorded **fact MUST carry provenance** — a reference to the source evidence (file, trace, schema, commit) from which it was derived. A fact without provenance is **non-authoritative**. [Ref: PR-5; Chikofsky & Cross]
- **KN-2** Decisions **MUST** be recorded in an immutable, append/supersede format (ADR). An accepted decision **MUST NOT** be silently edited; it is **superseded** by a new record. [Ref: Nygard, 2011]
- **KN-3** A **hypothesis MUST be marked as a hypothesis** until verified by evidence; it **MUST NOT** be recorded as a fact. [Ref: von Mayrhauser & Vans, integrated comprehension model, IEEE Computer, 1995; Feathers (characterization tests)]
- **KN-4** Contracts and invariants are **authoritative** and changes to them **MUST** pass through governance + versioning (§17–§18). [Ref: PR-10]
- **KN-5** Knowledge **MUST** reside in the repository (PR-4), never solely in conversation, model memory, or tooling state. [Ref: PR-4]
- **KN-6** Triangulation: where feasible, a fact **SHOULD** be corroborated by more than one source class (static, dynamic, human) before being recorded as authoritative. [Ref: Demeyer et al., 2002 — triangulation in reverse engineering]

### 14.4 Anti-Assumption Discipline

The combination KN-1 + KN-3 + KN-6 is the standard's structural defense against converting assumptions into facts (the central failure mode of §2). This **MUST** be preserved in all later phases. [Ref: PR-1, PR-5]

---

## 15. Review Model

> §15 defines the **review framework**; detailed review checklists are deferred to Phase 6/8.

### 15.1 Review Types

The SES **SHALL** adopt the review taxonomy of **IEEE Std 1028-2008 (Software Reviews and Audits)**, because it is the recognized standard for distinguishing review forms. [Ref: IEEE 1028-2008]

| Review Type | Purpose | When applied |
|---|---|---|
| **Inspection** | Formal, rigorous defect detection against criteria | Gating high-risk artifacts (contracts, ADRs, the standard itself) |
| **Technical Review** | Evaluate fitness for purpose by qualified reviewers | Design docs, plans |
| **Walkthrough** | Author-led, educational, early feedback | Early-stage understanding/recovery |
| **Audit** | Independent conformance check against the standard | Conformance/certification |
| **Management Review** | Status/decision review by authority | Governance gates |

### 15.2 Normative Review Rules

- **RV-1** Every **authoritative artifact MUST** pass at least one review of an appropriate type before it becomes effective. [Ref: IEEE 1028; PR-8]
- **RV-2** Changes to the **standard itself MUST** undergo **Inspection** (the most rigorous form), because the standard is the highest authority. [Ref: IEEE 1028; PR-10]
- **RV-3** Review **MUST** be against **explicit, written criteria** (checklists/verification criteria), not reviewer preference. [Ref: IEEE 1028 §"entry criteria"; PR-7]
- **RV-4** Review of work **SHOULD** be performed by someone other than its sole author where independence adds value (separation of duties). [Ref: PR-8; IEEE 1012 (independent V&V); Google code-review practice]
- **RV-5** Review outcomes (findings, disposition) **MUST** be recorded as evidence (PR-5). [Ref: IEEE 1028]

### 15.3 Relationship to Validation

Review (§15) is **human/criteria-based examination**; validation (§16) is **objective conformance verification**. They are complementary and **MUST NOT** be merged (PR-8). [Ref: ISO/IEC/IEEE 1012 distinguishes review, analysis, and test as distinct V&V activities]

---

## 16. Validation Model

> **Phase boundary.** §16 defines the **validation framework and its rationale**. The **full validation rules and conformance procedure** are the deliverable of **Phase 6 (Define validation)**. [Ref: Development Order]

### 16.1 Verification vs Validation

The SES **SHALL** preserve the formal distinction: **verification** = "are we building it right" (conformance to specification); **validation** = "are we building the right thing" (fitness for intended use). [Ref: ISO/IEC/IEEE 1012-2016; SWEBOK V&V KA]

### 16.2 Verification Methods

Every requirement in the SES (and in projects governed by it) **SHALL** be assigned one or more verification methods from the standard taxonomy: **Inspection, Analysis, Demonstration, Test**. [Ref: ISO/IEC/IEEE 29148:2018]

### 16.3 Validation Ordering Principle (for projects)

For software *produced under* the standard, the SES **SHALL** adopt a **fast-feedback-first** validation ordering, presented as converged practice (not as an ISO-mandated sequence): static analysis → unit → integration → contract → regression → system/E2E → non-functional (performance/security/resilience) → runtime verification (canary + observability) → review (in parallel). [Ref: Converged practice — Cohn/Fowler test pyramid; Pact (contract testing); Google SRE (canarying/SLOs); ISO/IEC/IEEE 29119 (test process)]

> **Honesty marker.** The *existence* of these verification layers is standardized (ISO 29119, 1012); the *specific ordering and weighting* is **converged practice, not a formal standard**, and competing weightings exist (e.g., "testing trophy"). This **MUST** be presented as such in Phase 6 (FR-12). [Ref: Dodds (testing trophy) vs Cohn (pyramid)]

### 16.4 Normative Validation Rules

- **VL-1** Conformance of a project to the SES **MUST** be expressed as **objective pass/fail against stated criteria**, never as subjective judgment. [Ref: PR-7]
- **VL-2** Each requirement class **MUST** have a defined verification method (§16.2). [Ref: ISO 29148]
- **VL-3** Validation evidence **MUST** be recorded and reproducible. [Ref: PR-9; ISO 29119 test records]
- **VL-4** A conformance verdict **MUST** cite the evidence on which it rests (PR-5). [Ref: PR-5]
- **VL-5** Validation **MUST** be a responsibility distinct from implementation/execution (PR-8). [Ref: ISO/IEC/IEEE 1012 — independence of V&V]

### 16.5 Conformance / Certification Concept

The SES **SHALL** define (in Phase 6) a **conformance assertion**: a recorded, evidenced statement that a project satisfies the applicable SES requirements at a stated standard version. This is the mechanism by which "the standard governs projects" becomes verifiable rather than aspirational (OBJ-7, FR-15). [Ref: Converged practice — conformance clauses in ISO/IEEE standards]

---

## 17. Governance Model

> §17 defines the **governance framework**; the operational governance procedure is detailed in **Phase 7 (Define governance)**.

### 17.1 Governing Premise

The standard is **superordinate** to projects. Projects conform to and provide feedback to the standard; **only verified engineering evidence may change the standard**. [Ref: Mission Statement; §1.2]

### 17.2 Normative Governance Rules

- **GV-1** Projects **MUST NOT** modify the core standard. They **MAY** submit change proposals with evidence (feedback path). [Ref: PR-10; Mission Statement]
- **GV-2** A change to the standard **MUST** originate as a proposal containing: the problem, the evidence, the proposed change, the impact on existing requirements, and the affected versions. [Ref: Converged practice — RFC process, IETF; ADR for the change itself]
- **GV-3** A change **MUST** be approved by the designated **Standard Authority** (STK-1) after **Inspection** (RV-2). [Ref: IEEE 1028; §15]
- **GV-4** A change **MUST** be supported by evidence from the approved evidence base (Appendix A) or be explicitly marked UNSUPPORTED; unevidenced changes **MUST NOT** be accepted as normative. [Ref: PR-1]
- **GV-5** Every accepted change **MUST** produce: a version increment (§18), a changelog entry, and an ADR recording the decision and its rationale. [Ref: PR-5; Nygard; Keep a Changelog convention]
- **GV-6** The standard **MUST** maintain a single, identifiable **current authoritative version**; superseded versions are retained for history but are non-governing. [Ref: PR-6; semantic versioning]
- **GV-7** Roles **MUST** be defined (at minimum: Standard Authority, Maintainer, Reviewer, Contributor/Project). Detailed RACI is a Phase-7 deliverable. [Ref: Converged practice — open-source governance models, e.g., Linux kernel maintainer hierarchy; Apache/CNCF governance]

### 17.3 Governance Model Options (presented per PR-12)

Phase 7 **MUST** compare and select among documented governance models and justify the choice in context: **BDFL/single-authority**, **maintainer-hierarchy** (Linux kernel), and **committee/foundation** (Apache, CNCF, IETF). Each is appropriate to a different scale and trust structure. [Ref: Linux kernel development process docs; Apache Software Foundation governance; IETF RFC process]

---

## 18. Versioning Strategy

### 18.1 Versioning Scheme

The SES **SHALL** be versioned using **Semantic Versioning 2.0.0** semantics (`MAJOR.MINOR.PATCH`), interpreted for a standard as follows. [Ref: Semantic Versioning 2.0.0, semver.org]

| Increment | Meaning for the SES | Compatibility for projects |
|---|---|---|
| **MAJOR** | A normative change that can break existing project conformance (e.g., a rule made stricter, a requirement removed/redefined). | Projects **MAY** need rework to remain conformant. |
| **MINOR** | A backward-compatible addition (new optional rule, new guidance, new artifact type) that does not invalidate existing conformance. | Existing conformant projects remain conformant. |
| **PATCH** | Editorial/clarification/typo/evidence-citation fixes with no normative effect. | No conformance impact. |

### 18.2 Normative Versioning Rules

- **VS-1** Every release of the standard **MUST** carry a unique semantic version. [Ref: SemVer 2.0.0]
- **VS-2** Every change **MUST** be recorded in a **changelog** that states what changed and why. [Ref: Keep a Changelog convention; PR-5]
- **VS-3** A project's conformance assertion (§16.5) **MUST** name the **standard version** it conforms to. [Ref: PR-5]
- **VS-4** A MAJOR change **MUST** include a **migration note** describing what conforming projects must do. [Ref: Converged practice — API deprecation/migration; RFC 8594 spirit]
- **VS-5** Backward-incompatible changes **MUST NOT** be released as MINOR or PATCH. [Ref: SemVer 2.0.0]
- **VS-6** The standard **SHOULD** define a **deprecation period** for rules being removed, rather than immediate deletion, to give projects time to adapt. [Ref: Converged practice — deprecation policy]

> **Rationale.** Semantic versioning gives consuming projects a *compatibility contract* with the standard — the same contract a library gives its callers. Without it, "the standard governs projects" would mean "the standard can break projects without warning," which contradicts NFR-9 (stability). [Ref: SemVer 2.0.0]

---

## 19. Extension Policy

### 19.1 The Extension Problem

The standard must be **stable and singular** (PR-10) yet **applicable to diverse contexts** (S-2: backend, frontend, infra, reverse engineering, etc.). These pull in opposite directions. The Extension Policy resolves the tension. [Ref: PR-11, PR-12]

### 19.2 Core vs Extension

- **EX-1** The SES **SHALL** distinguish a **stable core** (technology-independent, governs all projects) from **extensions** (context-specific: language conventions, framework rules, domain specifics). [Ref: Converged practice — profiles/extensions in standards, e.g., language bindings of a protocol]
- **EX-2** Projects **MAY** define **extensions** for their context (e.g., a "Python conventions" extension, a "REST API" extension). [Ref: PR-12]
- **EX-3** An extension **MUST NOT** contradict the core. In any conflict, the **core governs**. [Ref: RA-5; PR-10]
- **EX-4** An extension **MUST NOT** weaken a core `MUST/SHALL` rule; it **MAY** only **add** or **strengthen**. [Ref: Converged practice — standards profiles may constrain but not relax the base]
- **EX-5** Extensions **MUST** declare which standard version and which core rules they extend (traceability). [Ref: PR-5]
- **EX-6** Where a context genuinely requires deviating from a core rule, this **MUST** be raised as a governance change proposal (§17), not implemented as a silent local override. [Ref: GV-1]

### 19.3 Mechanism

Extensions are **separate artifacts** that reference the core; they are the sanctioned path by which projects adapt without forking the standard. This preserves "projects do not modify the standard" (Mission Statement) while making the standard usable across every declared domain. [Ref: §17; PR-10]

---

## 20. Success Criteria

Success criteria (`SC-n`) are the **objective tests** of whether the standard meets its objectives (§3). Each is verifiable.

| ID | Success Criterion | Method | Tied To |
|---|---|---|---|
| **SC-1** | A project of an arbitrary, previously-unseen technology stack can be assessed for conformance using only the SES (no tool/language assumptions). | Demonstration | OBJ-1 |
| **SC-2** | 100% of normative rules carry an evidence reference or an explicit UNSUPPORTED marker (tolerance 99% pending citation verification). | Analysis | OBJ-2 |
| **SC-3** | Every formalized practice traces to ≥1 source in the approved evidence base (Appendix A). | Inspection | OBJ-3 |
| **SC-4** | No core normative rule names or requires a specific product, language, framework, or AI model. | Analysis | OBJ-4 |
| **SC-5** | Every authoritative artifact class is defined as a version-controlled repository artifact. | Inspection | OBJ-5 |
| **SC-6** | The Knowledge Model requires provenance for every recorded fact (KN-1 present and enforced). | Inspection | OBJ-6 |
| **SC-7** | Every requirement class has a defined, objective verification method and pass/fail criteria. | Inspection | OBJ-7 |
| **SC-8** | A controlled change path exists (governance + semantic versioning); no mechanism permits a project to mutate the core. | Inspection | OBJ-8 |
| **SC-9** | All artifacts are plain-text, structured, and parseable by both humans and automated tooling. | Demonstration | OBJ-9 |
| **SC-10** | The standard contains zero unresolved internal contradictions (or all are resolved by stated precedence). | Analysis | NFR-11 |

> **Phase-1 acceptance.** For the current assignment specifically, success is: this `SDD.md` exists, contains all 24 required sections, satisfies FR-11 (evidence or UNSUPPORTED on normative rules), and is internally consistent (NFR-11). [Ref: Required SDD Sections, this initiative]

---

## 21. Risks

Risks are recorded with likelihood (L), impact (I), and mitigation, per risk-management practice. [Ref: Boehm, "Software Risk Management," IEEE Software, 1991; ISO 31000 framing]

| ID | Risk | L | I | Mitigation |
|---|---|---|---|---|
| **RK-1** | **Over-engineering the standard** — it becomes so heavy that projects ignore it. | Med | High | PR-11 (minimal but sufficient); NFR-12; extension policy keeps core small. |
| **RK-2** | **Assumption creep** — unevidenced rules slip in as facts. | Med | High | FR-11 + PR-1 enforcement; UNSUPPORTED marking; Inspection (RV-2). |
| **RK-3** | **Tool/AI coupling** — convenience leads to embedding a tool dependency. | Med | High | FR-16, NFR-1/NFR-7; analysis test SC-4. |
| **RK-4** | **Drift between standard and derived docs** — operational docs diverge from the core. | High | Med | PR-6 + RA-4 (derived artifacts regenerable); generated traceability index. |
| **RK-5** | **Governance capture / stagnation** — the change process is too slow or too loose. | Med | Med | §17 model selection; semantic versioning; deprecation periods (VS-6). |
| **RK-6** | **Citation fragility** — references decay or are mis-attributed. | Med | Med | NFR-13 (prefer durable sources); verification of citations before MAJOR release. |
| **RK-7** | **Standard ignored in practice** — adopted on paper, bypassed in work. | Med | High | Conformance assertion (§16.5) + audit (RV-4) make non-conformance visible. |
| **RK-8** | **Ambiguity** — rules interpreted differently by different readers/agents. | Med | High | RFC 2119 keywords (NFR-4); single-interpretation review test. |
| **RK-9** | **Scope bleed across phases** — later-phase content authored prematurely. | Med | Med | Explicit phase-boundary notes; Phase-1 scope clause (§4.4). |
| **RK-10** | **Determinism overclaim** — promising reproducibility the discipline cannot guarantee for human/creative steps. | Med | Med | PR-9 stated as SHOULD; overclaim marked UNSUPPORTED. |

---

## 22. Assumptions

Assumptions are recorded separately from requirements and **MUST NOT** be treated as rules (PR-1). Each should be validated before it is relied upon.

- **AS-1** The organization will designate a **Standard Authority** (STK-1) empowered to approve changes. *If false:* governance (§17) cannot function.
- **AS-2** Engineering work products are kept under **version control**. *Basis:* PR-4. *If false:* repository-as-memory fails.
- **AS-3** The declared user systems (Radius1, SAS4, ERP, etc.) will become **consumers** of the standard, not co-owners of it. *Basis:* Mission Statement.
- **AS-4** Competent human engineers and/or capable automated agents are available to **apply and review** the standard. *If false:* review/validation models degrade.
- **AS-5** The evidence base in Appendix A is **accessible** to authors and reviewers for citation verification. *Note:* exact clause numbers/editions **SHOULD** be confirmed against primary sources before MAJOR releases (RK-6).
- **AS-6** Plain-text + version control will remain a viable, durable substrate for the foreseeable life of the standard. *Basis:* NFR-7. Reasonable but **UNSUPPORTED** as a guarantee.

---

## 23. Constraints

Constraints are non-negotiable boundaries imposed on the design. [Ref: ISO/IEC/IEEE 42010 — constraints as architectural context]

- **CN-1** The standard **MUST** be vendor-, tool-, language-, framework, technology-, and AI-independent. (Hard constraint; PR-3.)
- **CN-2** The standard **MUST** remain valid even if all AI systems disappear. (Hard constraint; §1.3.)
- **CN-3** The standard **MUST** be evidence-based; unevidenced rules **MUST** be marked UNSUPPORTED. (PR-1.)
- **CN-4** The standard **MUST NOT** invent a novel methodology; it reconstructs proven practice. (NG-1, PR-2.)
- **CN-5** Phase boundaries in the Development Order **MUST** be respected; Phase 1 produces **only** this SDD. (§4.4.)
- **CN-6** The repository **MUST** be the authoritative location of the standard (repository-as-memory). (PR-4.)
- **CN-7** Projects **MUST NOT** modify the core standard. (GV-1.)
- **CN-8** All artifacts **MUST** be plain-text and version-controllable. (NFR-1.)
- **CN-9** Every requirement **MUST** be testable/verifiable. (PR-7.)

---

## 24. Future Work

The following are **explicitly deferred** to later Development-Order phases. They are listed to fix scope, not to begin them.

| Item | Development-Order Phase | Notes |
|---|---|---|
| Concrete repository directory/file structure | **Phase 2** | Populates §10 architecture into a layout. |
| Full lifecycle specification (per-phase objectives/inputs/activities/outputs/evidence/verification/tools/mistakes/references) | **Phase 3** | Populates §12. |
| Full artifact catalog + schemas | **Phase 4** | Populates §11. |
| Stage catalog + full stage specifications | **Phase 5** | Populates §13. |
| Validation rules + conformance procedure + checklists | **Phase 6** | Populates §16. |
| Operational governance procedure + roles (RACI) + model selection | **Phase 7** | Populates §17. |
| Templates (ADR, contract, design doc, stage, checklist, etc.) | **Phase 8** | Derived from §11/§13. |
| Worked examples across domains (backend, frontend, infra, reverse engineering, legacy modernization) | **Phase 9** | Non-normative illustrations. |
| Tooling to mechanically check conformance (parsers, traceability generators) | Post-standard | Must remain optional and tool-independent (CN-1). |
| Verification of exact clause numbers/editions of all Appendix-A references against primary sources | Before first MAJOR release | Addresses RK-6 / AS-5. |

---

> **Editorial note (v0.2.0–v0.4.0 — Review extensions).** Sections 25–50 were added under successive Engineering Review Orders to close architectural gaps identified during Phase-1 review. Per those orders' execution rules, existing sections (1–24) and every existing requirement ID are **unchanged and not renumbered**; the new architectural models are therefore **appended** here (after §24) rather than inserted, *solely* to preserve existing numbering. Each defines an **architectural model only**; detailed specification remains deferred to the Development-Order phases named within. These sections are normative (rule-dense) by design, consistent with the review orders' instruction to favor rules over narrative. [Ref: Engineering Review Orders; §18 VS-2; IEEE 1016-2009 identification continuity]

---

## 25. Engineering Discovery Model

> **Phase boundary.** §25 defines the **architecture** of discovery — the model by which an *Unknown System* becomes an *Understood System*. The **detailed specification** of each discovery activity (objectives, inputs, activities, outputs, evidence, verification, tools, mistakes) is the deliverable of **Phase 3 (lifecycle)** and **Phase 5 (stages)**. This section defines the model only. [Ref: Development Order]

### 25.1 Position in the Standard

Discovery realizes the **Understanding** and **Reverse Engineering / Reconstruction** phases of the Engineering Lifecycle (§12.2) at the architectural level, and feeds the Knowledge Model (§14), the Evidence Confidence Model (§26), the Engineering Evidence Chain (§28), and the Repository Knowledge Architecture (§31).

### 25.2 Discovery Model (architectural)

Discovery is a **goal-directed, iterative, evidence-producing** transformation from an unknown system to a verified understanding. It is organized into evidence layers; layers are **dependency-ordered, not strictly sequential** (LC-3). Full comprehension is not the objective; sufficiency for the mission is. [Ref: Demeyer/Ducasse/Nierstrasz, 2002 ("First Contact", "Initial Understanding"); Lehman's Laws]

```
UNKNOWN SYSTEM
  │
  ├─ Inventory Layer   : Asset · Repository · Technology · Build-System · Runtime-Environment detection
  ├─ Structure Layer   : Dependency · Module · API · Database · Configuration discovery
  ├─ Security Layer    : Security · Authentication · Authorization discovery
  ├─ Behavior Layer    : Event · Workflow · Execution-Flow Recovery · Runtime Observation
  │
  ├─ Analysis Methods  : Static Analysis · Dynamic Analysis · Cross-Validation (triangulation)
  ├─ Synthesis         : Architecture Recovery · Knowledge Extraction · Evidence Collection
  └─ Output            : Documentation · Verification  →  DISCOVERY COMPLETE (§27)
```

### 25.3 Mandated Discovery Activities (coverage)

The discovery model **SHALL** account for all of the following activities (each specified in detail in later phases): Asset Inventory; Repository Inventory; Technology Detection; Build System Detection; Runtime Environment Detection; Dependency Discovery; Module Discovery; API Discovery; Database Discovery; Configuration Discovery; Security Discovery; Authentication Discovery; Authorization Discovery; Event Discovery; Workflow Discovery; Execution Flow Recovery; Runtime Observation; Static Analysis; Dynamic Analysis; Cross Validation; Architecture Recovery; Knowledge Extraction; Evidence Collection; Documentation; Verification; Discovery Complete. [Ref: Engineering Review Order — coverage requirement]

### 25.4 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **DSC-1** | An unknown system **SHALL** pass through Discovery before any modification. | [Ref: Chikofsky & Cross 1990; Feathers 2004] |
| **DSC-2** | Every discovery output **MUST** carry provenance (KN-1) and a confidence level (§26). | [Ref: PR-5; §26] |
| **DSC-3** | Discovery **MUST** combine static and dynamic analysis and **cross-validate** (triangulate); disagreements **MUST** be recorded, not silently resolved. | [Ref: Demeyer et al. 2002] |
| **DSC-4** | Discovery is goal-directed and **iterative**; complete comprehension is **NOT** required — only sufficiency for the mission. | [Ref: Lehman's Laws; Demeyer 2002] |
| **DSC-5** | Discovery is complete only when the "Discovery Complete" criteria (§27) are objectively met. | [Ref: §27; IEEE 1028 exit criteria] |
| **DSC-6** | No discovery conclusion **MAY** assert confidence exceeding its evidence (§26). | [Ref: PR-1; PR-5] |

---

## 26. Evidence Confidence Model

### 26.1 Purpose & Relationship

This model **refines** the Knowledge Model (§14): every engineering fact (KN-1) **SHALL** additionally carry a graded confidence. Grading facts by evidence strength is established practice in evidence-based software engineering. [Ref: Kitchenham, Dybå, Jørgensen, "Evidence-Based Software Engineering," ICSE 2004; GRADE evidence-grading analog]

### 26.2 Confidence Levels

| Level | Definition | Relative strength |
|---|---|---|
| **A** | Observed directly at runtime (actual behavior). | Highest |
| **B** | Confirmed by implementation (source code). | High |
| **C** | Confirmed by official documentation. | Medium |
| **D** | Derived from multiple independent evidence sources (triangulation / inference). | Medium-low |
| **E** | Engineering hypothesis (unverified). | Lowest |

> **Rationale.** Level A ranks highest because dynamic evidence reveals *actual* behavior, not intended behavior — a core reverse-engineering principle. [Ref: Chikofsky & Cross 1990] Level D is inferential and is therefore ranked below directly-confirmed evidence even though it aggregates sources. **Marked status:** the *principle* of confidence grading is evidence-based; the **specific A–E enumeration is the SES-adopted classification (converged practice)**, not a verbatim external standard.

### 26.3 Mandatory Fact Fields

Every recorded engineering fact **SHALL** contain: **Confidence Level**; **Evidence Source**; **Verification Status**; **Timestamp**; **Repository Reference**. [Ref: NIST SP 800-86 chain-of-custody fields; PR-5]

### 26.4 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **EVC-1** | Every engineering fact **MUST** carry a confidence level (A–E). | [Ref: PR-1; EBSE 2004] |
| **EVC-2** | Every fact **MUST** record all five fields (§26.3). | [Ref: NIST SP 800-86; PR-5] |
| **EVC-3** | A Level-E fact is a hypothesis and **MUST NOT** be treated as authoritative (consistent with KN-3). | [Ref: von Mayrhauser & Vans 1995; KN-3] |
| **EVC-4** | No fact **MAY** become authoritative without a confidence classification. | [Ref: PR-1; Engineering Review Order] |
| **EVC-5** | Confidence **MAY** be raised only by recording additional evidence/provenance; it **MUST NOT** be raised by assertion. | [Ref: Demeyer 2002 (triangulation); PR-5] |
| **EVC-6** | Where Level-A evidence conflicts with B/C, the conflict **MUST** be recorded as a finding/risk; the higher-fidelity (runtime) evidence governs the recorded behavior. | [Ref: Chikofsky & Cross; Demeyer 2002] |

---

## 27. Engineering Completion Criteria

### 27.1 Purpose

Defines **when a body of engineering work is complete**. Builds on stage exit criteria (§13) and the Validation Model (§16). Objective, criteria-based completion is established practice as the "Definition of Done" and as stage-gate exit criteria. [Ref: The Scrum Guide — Definition of Done; IEEE 1028-2008 exit criteria; ISO/IEC/IEEE 12207:2017 process outcomes]

### 27.2 Completion States

The SES **SHALL** define objective exit criteria for, at minimum: **Discovery Complete; Knowledge Complete; Dependency Complete; Architecture Complete; Execution Flow Complete; API Complete; Database Complete; Security Complete; Workflow Complete; Runtime Complete; Documentation Complete; Validation Complete; Engineering Complete.** [Ref: Engineering Review Order]

### 27.3 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **CMP-1** | Each completion state **MUST** define **objective, verifiable** exit criteria; subjective "done" is prohibited. | [Ref: PR-7; IEEE 1028-2008] |
| **CMP-2** | A completion state is reached only when its exit criteria are verified by a method in §16.2. | [Ref: §16; ISO/IEC/IEEE 29148] |
| **CMP-3** | "Engineering Complete" **MUST NOT** be asserted unless all subordinate completion states are complete and evidenced. | [Ref: PR-8; stage-gate practice] |
| **CMP-4** | Completion **MUST** be evidenced and recorded (provenance). | [Ref: PR-5] |
| **CMP-5** | Detailed per-state criteria are deferred to Phase 5/6; §27 defines the model only. | [Ref: Development Order] |

---

## 28. Engineering Evidence Chain

### 28.1 Purpose

Defines the ordered, **provenance-preserving** path that produces engineering knowledge and **prevents assumptions from becoming facts** (the central failure mode of §2; reinforces §14.4). [Ref: W3C PROV-DM / PROV-O, 2013; NIST SP 800-86 chain of custody]

### 28.2 The Chain

```
Unknown Observation → Evidence → Verification → Engineering Fact → Knowledge
→ Architecture → Decision → Implementation → Validation → Documentation → Maintenance
```

Each arrow is a **provenance link**: the downstream node **MUST** be justified by the upstream node.

### 28.3 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **ECH-1** | An observation **MUST NOT** be recorded as an engineering fact without passing Evidence → Verification. | [Ref: §14.4; Chikofsky & Cross 1990] |
| **ECH-2** | Each link **MUST** preserve provenance to its predecessor (unbroken chain of custody). | [Ref: W3C PROV; NIST SP 800-86] |
| **ECH-3** | Every Decision **MUST** trace backward to verified facts and forward to Implementation, Validation, and Documentation. | [Ref: PR-5; §29] |
| **ECH-4** | Asserting a downstream node without its upstream evidence (a **broken chain**) is non-conformant. | [Ref: PR-1] |
| **ECH-5** | Hypotheses (confidence E, §26) **MUST NOT** pass the Verification link until verified. | [Ref: EVC-3; KN-3] |

---

## 29. Engineering Traceability Expansion

### 29.1 Purpose

Extends traceability from **requirements** (Appendix C) to **engineering work**. Bidirectional traceability is established requirements-engineering practice, here generalized to the engineering work chain. [Ref: Gotel & Finkelstein, "An Analysis of the Requirements Traceability Problem," ICRE 1994; ISO/IEC/IEEE 29148:2018; SWEBOK]

### 29.2 The Engineering Traceability Chain

```
Repository → Artifact → Module → Component → Function → Execution Flow
→ Evidence → Decision → Implementation → Test → Documentation
```

### 29.3 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **TRC-1** | The SES **SHALL** maintain **bidirectional** traceability across the engineering work chain (§29.2). | [Ref: ISO 29148; Gotel & Finkelstein 1994] |
| **TRC-2** | Every engineering decision **MUST** be traceable backward (evidence/facts) and forward (implementation, test, documentation). | [Ref: PR-5; ECH-3] |
| **TRC-3** | Traceability links **SHOULD** be **generated** artifacts (§11), not hand-maintained, to prevent drift. | [Ref: PR-6] |
| **TRC-4** | A change to any node **MUST** be propagable to its linked nodes (change-impact analysis). | [Ref: ISO 29148 — change impact] |
| **TRC-5** | This expands Appendix C from requirement-only to engineering-work traceability; the operational link schema is deferred to later phases. | [Ref: Development Order] |

---

## 30. Reverse Engineering Architecture

### 30.1 Purpose & Taxonomy

Defines reverse engineering as **engineering activities only** (not tools, per CN-1). The activity taxonomy follows the canonical reference distinguishing **reverse engineering** (examination), **design recovery**, **restructuring**, and **reengineering**. [Ref: Chikofsky & Cross 1990; Demeyer et al. 2002; Feathers 2004]

### 30.2 Activity Model

```
Unknown System → Discovery → Recovery → Understanding → Documentation
→ Planning → Modification → Validation → Knowledge Preservation
```

### 30.3 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **REV-1** | Reverse engineering up to and including Recovery is **examination only**; it **MUST NOT** alter the subject system. | [Ref: Chikofsky & Cross 1990 (definition)] |
| **REV-2** | Recovery **MUST** produce higher-level abstractions from lower-level artifacts, each evidenced (§26) and provenanced (§28). | [Ref: Chikofsky & Cross; §26; §28] |
| **REV-3** | Understanding **MUST** precede Planning; Planning **MUST** precede Modification. | [Ref: LC-2; Demeyer 2002] |
| **REV-4** | Modification **MUST** follow the implementation discipline (§12) and the Validation Model (§16). | [Ref: §12; §16] |
| **REV-5** | Knowledge Preservation **MUST** persist recovered knowledge into repository memory (§31) so recovery is not repeated. | [Ref: PR-4; §31] |
| **REV-6** | This section defines **activities only**; tool/technique selection is out of core scope (CN-1) and **MAY** be an extension (§19). | [Ref: CN-1; §19] |

### 30.4 Competing Contexts (per PR-12)

Source-available reverse engineering (static + dynamic analysis on source) and binary/protocol reverse engineering differ in technique and in legal constraint; the **activity model is common to both**, while technique is context-bound and extension-defined. Legal/authorization constraints on reverse engineering are real engineering constraints and **MUST** be confirmed per engagement. [Ref: Chikofsky & Cross (general activities); binary-RE literature — Eilam, *Reversing*, 2005; Converged practice on authorization]

---

## 31. Repository Knowledge Architecture

### 31.1 Purpose

Defines how repository knowledge is **classified and how it evolves**, realizing "repository as permanent engineering memory" (PR-4). It **refines** the Artifact Authority Model (§11) and the Knowledge Model (§14) by adding a knowledge-evolution dimension. The progression from raw observation to knowledge follows the established DIKW knowledge-management hierarchy, applied here **by analogy**. [Ref: Ackoff, "From Data to Wisdom," 1989 (analogy); §11; §14]

### 31.2 Knowledge Classes

| Class | Definition | Authority (§11) / Confidence (§26) |
|---|---|---|
| **Observed Facts** | Raw facts captured during discovery, pre-verification. | Non-authoritative; confidence A/B/E |
| **Verified Facts** | Facts that passed the Evidence Chain (§28). | Candidate-authoritative; verified confidence |
| **Engineering Knowledge** | Synthesized understanding from verified facts. | Authoritative |
| **Design Decisions** | Recorded design choices + rationale. | Authoritative (immutable / superseded) |
| **Architecture Decisions** | ADRs (§11.3). | Authoritative (immutable / superseded) |
| **Operational Knowledge** | Runbooks, operational behavior. | Authoritative |
| **Historical Knowledge** | Superseded but retained knowledge. | Authoritative-historical (non-governing) |
| **Deprecated Knowledge** | Marked obsolete, retained for traceability. | Non-governing |
| **Generated Knowledge** | Mechanically produced (§11). | Generated; not hand-edited |
| **Derived Knowledge** | Transformed from authoritative sources (§11). | Derived; not hand-edited |
| **Authoritative Knowledge** | Single source of truth (§11). | Authoritative |

### 31.3 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **RKA-1** | Repository knowledge **MUST** be organized into the defined classes (§31.2), each with an authority class (§11) and, for facts, a confidence level (§26). | [Ref: §11; §26] |
| **RKA-2** | Knowledge **MUST** progress Observed → Verified → Engineering Knowledge only via the Evidence Chain (§28). | [Ref: §28; ECH-1] |
| **RKA-3** | Superseded knowledge **MUST** be retained as Historical; deprecated knowledge **MUST** be marked, **not** deleted. | [Ref: Nygard (ADR supersede); RFC 8594] |
| **RKA-4** | Generated and Derived knowledge **MUST NOT** be hand-edited; they **MUST** be reproducible from authoritative sources. | [Ref: PR-6; RA-4] |
| **RKA-5** | Authoritative knowledge **MUST** carry provenance (§28) and, where it is a fact, confidence (§26). | [Ref: PR-5; §26] |
| **RKA-6** | This architecture realizes repository-as-permanent-memory (PR-4) and **MUST** remain valid under tool/session/vendor change. | [Ref: PR-4; NFR-7] |

### 31.4 Forward Reference

The **concrete storage layout** of these knowledge classes is a **Phase-2** concern; **templates** are **Phase-8**. §31 defines the architecture only.

---

## 32. Engineering Mission Model

> **Phase boundary.** §32 defines the **Mission as an architectural element**. Mission *templates and instances* are Phase-8 / per-project artifacts. Architecture only. [Ref: Development Order]

### 32.1 Purpose

Every engineering task is initiated and bounded by a **Mission**. The Mission is the authorizing input already referenced by the determinism principle (PR-9) and by the conformance concept (§16.5); §32 formalizes it. It corresponds to project planning / work authorization in life-cycle process standards. [Ref: ISO/IEC/IEEE 12207:2017 Project Planning process; SWEBOK Software Engineering Management KA]

### 32.2 Mission Structure

A Mission **SHALL** contain, at minimum: **Objective; Scope; Constraints; Expected Deliverables; Success Criteria; Allowed Operations; Forbidden Operations; Evidence Requirements.** [Ref: ISO/IEC/IEEE 12207 Project Planning outcomes; §3; §4; §5]

### 32.3 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **MIS-1** | No engineering activity **MAY** start without an **active** Mission. | [Ref: ISO 12207 (Project Planning); Engineering Review Order] |
| **MIS-2** | A Mission **MUST** define all eight elements (§32.2); an incomplete Mission is **NOT** active. | [Ref: ISO 12207; PR-7] |
| **MIS-3** | Allowed/Forbidden Operations **MUST** be drawn from the Operation Model (§34). | [Ref: §34] |
| **MIS-4** | Engineering activity **MUST NOT** exceed the Mission Scope or violate its Constraints; deviations **REQUIRE** a new or amended Mission. | [Ref: §17 governance; PR-10] |
| **MIS-5** | Mission Success Criteria **MUST** be objective and verifiable (§16). | [Ref: PR-7; §16] |
| **MIS-6** | Every produced artifact **MUST** trace to the Mission that authorized it (§29). | [Ref: §29; PR-5] |

---

## 33. Engineering State Model

> **Phase boundary.** §33 defines the **state-machine architecture**; per-state operational procedures are Phase-3 / Phase-5. Architecture only. [Ref: Development Order]

### 33.1 Purpose

Defines the canonical engineering state machine through which a subject system progresses under a Mission. States align with the Engineering Lifecycle phases (§12.2) and with life-cycle stage standards. [Ref: ISO/IEC/IEEE 15288:2023 life-cycle stages; ISO/IEC/IEEE 12207:2017; OMG UML 2.x State Machines (formalism)]

### 33.2 State Machine

```
UNKNOWN → DISCOVERING → UNDERSTOOD → DOCUMENTED → PLANNED → IMPLEMENTING
→ VALIDATING → COMPLETED → MAINTAINING → ARCHIVED
```

State-to-lifecycle mapping: DISCOVERING ↔ Discovery/Understanding (§25); DOCUMENTED ↔ Documentation (§38); PLANNED ↔ Planning (§7, §35); IMPLEMENTING ↔ Implementation (§12); VALIDATING ↔ Validation (§16); COMPLETED ↔ "Engineering Complete" (§27); MAINTAINING ↔ Maintenance (LC-4); ARCHIVED ↔ Retirement (LC-5).

### 33.3 Per-State Definition Requirement

Each state **SHALL** define: **Entry Conditions; Exit Conditions; Required Evidence; Produced Artifacts.** A state's Exit Conditions **MUST** equal the corresponding Completion-State criteria (§27); the state machine and the completion model are **two views of one gate set** (no duplication). [Ref: §27; §13]

### 33.4 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **STA-1** | A subject system **MUST** occupy exactly one state at a time under a given Mission. | [Ref: OMG UML state-machine semantics] |
| **STA-2** | A transition **MUST NOT** occur unless the source state's Exit Conditions are verified (§16, §27). | [Ref: §16; §27; CMP-2] |
| **STA-3** | Each state **MUST** define its four elements (§33.3). | [Ref: ISO 12207; PR-7] |
| **STA-4** | Transitions **MUST** be recorded as evidence (provenance) and are traceable (§29). | [Ref: PR-5; §29] |
| **STA-5** | An INT (§40) violation **MUST** block the transition out of its originating state. | [Ref: §40; INT enforcement] |

---

## 34. Engineering Operation Model

> **Phase boundary.** §34 defines the **operation set and contracts**; operation *procedures* are Phase-3 / Phase-5. Architecture only. [Ref: Development Order]

### 34.1 Purpose

Defines the closed set of engineering **operations**. Operations are specified by **preconditions and postconditions**, making them composable and verifiable. [Ref: Meyer, *Design by Contract*; ISO/IEC/IEEE 12207 activities and tasks]

### 34.2 Operations and Governing Sections

| Operation | Realized / governed by |
|---|---|
| **DISCOVER** | §25 |
| **ANALYZE** | §12 Analysis; feeds §36 |
| **TRACE** | §29 |
| **VERIFY** | §16 |
| **DOCUMENT** | §38 |
| **COMPARE** | §37 |
| **PLAN** | §35; §12 Planning |
| **IMPLEMENT** | §12 Implementation |
| **VALIDATE** | §16 |
| **REVIEW** | §15 |

### 34.3 Per-Operation Definition Requirement

Each operation **SHALL** define **Inputs; Outputs; Preconditions; Postconditions.** [Ref: Meyer, Design by Contract]

### 34.4 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **OPS-1** | Only operations in this model **MAY** be performed; a Mission's Allowed Operations are a subset (§32). | [Ref: §32; MIS-3] |
| **OPS-2** | An operation **MUST NOT** execute unless its Preconditions hold; it **MUST** establish its Postconditions or fail explicitly. | [Ref: Meyer (Design by Contract)] |
| **OPS-3** | Every operation's outputs **MUST** carry provenance (§28) and, for facts, confidence (§26). | [Ref: §26; §28] |
| **OPS-4** | Examination operations (DISCOVER, TRACE, COMPARE, VERIFY) **MUST NOT** alter the subject system (consistent with REV-1). | [Ref: REV-1; §30] |

---

## 35. Engineering Decision Model

> **Phase boundary.** §35 defines the **Decision as an architecture element**; the decision-record template is Phase-8. Architecture only. [Ref: Development Order]

### 35.1 Purpose

Elevates every engineering decision to a first-class, traceable architecture element, **generalizing the ADR** (§11.3, KN-2) from architecture decisions to all engineering decisions. [Ref: Nygard, 2011; ISO/IEC/IEEE 42010:2022 (architecture decisions and rationale); IEEE 1016-2009 (design rationale)]

### 35.2 Decision Structure

A Decision **SHALL** record: **Decision; Decision Context; Alternatives; Evidence; Impact; Dependencies; Approval; Status; Superseded By.** [Ref: Nygard ADR; MADR template; ISO 42010 rationale]

### 35.3 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **DEC-1** | Every engineering decision **MUST** be recorded with all nine fields (§35.2). | [Ref: Nygard; ISO 42010] |
| **DEC-2** | A Decision **MUST** cite the Evidence (§26/§28) and the Impact Analysis (§36) that justify it. | [Ref: §26; §28; §36] |
| **DEC-3** | A Decision is **immutable once Approved**; change occurs only by a new Decision setting *Superseded By* (consistent with KN-2). | [Ref: KN-2; Nygard] |
| **DEC-4** | Every Implementation **MUST** trace back to **exactly one** engineering Decision. | [Ref: PR-5; §29; Engineering Review Order] |
| **DEC-5** | Architecture Decisions are the ADR subtype (§11.3) and inherit these rules. | [Ref: §11.3] |

---

## 36. Engineering Impact Analysis Model

> **Phase boundary.** §36 defines the **impact-analysis architecture**; the analysis procedure is Phase-3 / Phase-5. Architecture only. [Ref: Development Order]

### 36.1 Purpose

Defines mandatory **change impact analysis** prior to any modification. Impact analysis is an established maintenance activity. [Ref: ISO/IEC/IEEE 14764:2022 (impact analysis within the maintenance process); Bohner & Arnold, *Software Change Impact Analysis*, IEEE CS Press, 1996]

### 36.2 Impact Propagation Model

```
Requested Change → Affected Components → Dependencies → Execution Flow
→ Database → API → Security → Tests → Documentation → Deployment → Validation
```

### 36.3 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **IMP-1** | Every Implementation **MUST** begin with an impact analysis spanning the §36.2 dimensions. | [Ref: ISO 14764; Bohner & Arnold 1996] |
| **IMP-2** | Impact analysis **MUST** use the dependency view (§12 Analysis) and traceability (§29). | [Ref: §12; §29; TRC-4] |
| **IMP-3** | Identified impacts **MUST** be recorded as evidence and **MUST** feed the authorizing Decision (§35). | [Ref: §35; DEC-2] |
| **IMP-4** | A change whose impact cannot be determined **MUST** be treated as high-risk (§21) and **MUST NOT** proceed without explicit Mission authorization (§32). | [Ref: §21; §32] |
| **IMP-5** | Impact analysis **MUST** precede the IMPLEMENTING state (§33) in the Lifecycle (§12). | [Ref: §33; §12] |

---

## 37. Engineering Comparison Model

> **Phase boundary.** §37 defines the **comparison architecture**; comparison procedures/tools are out of core scope (CN-1) and deferred. Architecture only. (Code **CPM** = Comparison; **not** to be confused with **CMP**, Completion §27.) [Ref: Development Order]

### 37.1 Purpose

Reverse engineering and validation require **objective comparison** that yields engineering evidence, never opinion. Architecture-conformance comparison is established practice. [Ref: Murphy, Notkin, Sullivan, "Software Reflexion Models," IEEE TSE 2001; Fowler, ConsumerDrivenContracts]

### 37.2 Comparison Pairs

The model **SHALL** support comparison between: **System vs Documentation; System vs System; Version vs Version; Implementation vs Contract; Database vs ORM; Runtime vs Source; API vs Documentation; Configuration vs Runtime.** [Ref: Engineering Review Order; Reflexion Models; Pact]

### 37.3 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **CPM-1** | Every comparison **MUST** produce engineering evidence (differences with provenance), **never** subjective judgment. | [Ref: PR-1; PR-5] |
| **CPM-2** | Comparison results **MUST** be assigned a confidence level (§26); Runtime-vs-Source disagreements follow EVC-6. | [Ref: §26; EVC-6] |
| **CPM-3** | Divergences **MUST** be recorded as findings and **MAY** raise Decisions (§35) or Risks (§21); they **MUST NOT** be silently reconciled. | [Ref: §35; §21; DSC-3] |
| **CPM-4** | Comparison is an examination operation (COMPARE, §34) and **MUST NOT** alter either subject. | [Ref: OPS-4; REV-1] |

---

## 38. Engineering Documentation Model

> **Phase boundary.** §38 defines the **documentation architecture**; documentation templates are Phase-8. Architecture only. [Ref: Development Order]

### 38.1 Purpose

Defines documentation as **categorized, non-mixed** content, aligned to the Artifact Authority Model (§11) and the Repository Knowledge classes (§31). It introduces **no new authority**; it is a documentation *view* of those models. [Ref: ISO/IEC/IEEE 26515; arc42; docs-as-code]

### 38.2 Documentation Categories

Each documentation unit **SHALL** be classified as exactly one of: **Observed; Verified; Planned; Implemented; Validated; Historical; Deprecated; Generated; Authoritative.** These map to §31 knowledge classes and §11 authority classes. [Ref: §11; §31]

### 38.3 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **DOC-1** | Documentation **MUST NOT** mix the §38.2 categories within one authoritative unit. | [Ref: PR-6; ISO 26515] |
| **DOC-2** | Each documentation unit **MUST** declare its category (§38.2) and its authority class (§11.2). | [Ref: §11.2] |
| **DOC-3** | Generated documentation **MUST NOT** be hand-edited and **MUST** be reproducible. | [Ref: RA-4; PR-6] |
| **DOC-4** | Observed/Planned documentation **MUST NOT** be presented as Verified/Validated without passing the Evidence Chain (§28) / Validation (§16). | [Ref: §28; §16] |
| **DOC-5** | Deprecated/Historical documentation **MUST** be retained and marked, **not** deleted. | [Ref: RKA-3; RFC 8594] |

---

## 39. Repository Evolution Model

> **Phase boundary.** §39 defines **how repository knowledge grows**; the storage mechanics are Phase-2. Architecture only. [Ref: Development Order]

### 39.1 Purpose

Defines how repository knowledge grows with each engineering cycle, realizing repository-as-memory (PR-4) and the continuing-change reality of software (Lehman). [Ref: Lehman's Laws (continuing growth); PR-4; PR-9]

### 39.2 Per-Cycle Outputs

Every engineering cycle **SHALL** produce (those that apply): **New Knowledge; Updated Knowledge; Deprecated Knowledge; Generated Knowledge; Review Records; Validation Records; Decision Records; Traceability Updates.** [Ref: §15; §16; §35; §29]

### 39.3 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **EVO-1** | Each cycle **MUST** emit the applicable §39.2 outputs, each as a classified Repository Knowledge artifact (§31). | [Ref: §31] |
| **EVO-2** | Repository growth **SHOULD** be deterministic: the same Mission and same repository state yield the same knowledge deltas (SHOULD, not MUST, where human steps intervene — consistent with PR-9). | [Ref: PR-9] |
| **EVO-3** | Updates **MUST** preserve history; superseded knowledge becomes Historical (RKA-3) and **MUST NOT** be overwritten silently. | [Ref: RKA-3; KN-2] |
| **EVO-4** | Cycle outputs that change authoritative knowledge **MUST** be governed (§17) and versioned (§18). | [Ref: §17; §18] |

---

## 40. Engineering Integrity Rules

> **Constitutional.** §40 rules are completeness invariants that make the standard executable. They consolidate PR-5 (provenance) and §29 (traceability) into hard invariants. **Marked status:** the *principle* (completeness/provenance) is evidence-based; the specific invariant list is **SES-constitutional (converged practice)**, consistent with the cited principles. [Ref: PR-5; §29; ISO/IEC/IEEE 12207 (documentation of work products)]

### 40.1 Constitutional Rules

| ID | Rule | Evidence |
|---|---|---|
| **INT-1** | **No undocumented implementation.** Every implementation **MUST** trace to a Decision (§35) and documentation (§38). | [Ref: DEC-4; §38] |
| **INT-2** | **No undocumented decision.** Every decision **MUST** be recorded (§35). | [Ref: DEC-1] |
| **INT-3** | **No undocumented dependency.** Every dependency **MUST** be discovered (§25) and recorded. | [Ref: §25; §12 Analysis] |
| **INT-4** | **No undocumented API.** Every API **MUST** have a contract (§11.3). | [Ref: §11.3] |
| **INT-5** | **No undocumented database object.** | [Ref: §25; §11.3] |
| **INT-6** | **No undocumented configuration.** | [Ref: §25] |
| **INT-7** | **No undocumented workflow.** | [Ref: §25] |
| **INT-8** | **No undocumented security rule.** | [Ref: §25 (Security/AuthN/AuthZ discovery)] |
| **INT-9** | **No undocumented assumption.** Every assumption **MUST** be recorded (per the §22 pattern) and marked; it **MUST NOT** be silently relied upon. | [Ref: §22; PR-1] |
| **INT-10** | **No undocumented evidence.** Every evidence item **MUST** carry provenance (§28) and confidence (§26). | [Ref: §26; §28] |

### 40.2 Enforcement

Violation of any INT rule renders the affected work **non-conformant** (§16), **MUST** block state transition (STA-2), and **MUST** block Repository Readiness (§41). INT rules **MAY** be waived only through governance (§17). [Ref: §16; §41; §17]

---

## 41. Repository Readiness Criteria

> **Phase boundary.** §41 defines **readiness gates as composition**; the per-state criteria themselves are §27 (Phase 5/6). Architecture only. [Ref: Development Order]

### 41.1 Purpose

Defines objective **gates** determining when a repository is ready for implementation. Readiness is the **aggregate of Completion States (§27)**; it introduces no new criteria, only their composition. [Ref: §27; Converged practice — agile "Definition of Ready"; stage-gate entry criteria]

### 41.2 Readiness Gates

| Gate | Satisfied when |
|---|---|
| **Architecture Complete** | §27 *Architecture Complete* met |
| **Knowledge Complete** | §27 *Knowledge Complete* met |
| **Discovery Complete** | §27 *Discovery Complete* met |
| **Decision Complete** | All required Decisions recorded and Approved (§35) |
| **Documentation Complete** | §27 *Documentation Complete* met; §38 satisfied |
| **Traceability Complete** | §29 chain complete; no INT (§40) violations |
| **Validation Ready** | §16 preconditions met |
| **Implementation Ready** | All above met **and** Mission Allowed Operations include IMPLEMENT (§32, §34) |
| **Repository Ready** | All gates above satisfied |

### 41.3 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **RDY-1** | "Implementation Ready" **MUST NOT** be asserted unless all subordinate gates (§41.2) are objectively satisfied. | [Ref: §27; PR-7] |
| **RDY-2** | Readiness gates **MUST** be evidenced (provenance) and recorded. | [Ref: PR-5] |
| **RDY-3** | Any INT (§40) violation **MUST** block "Repository Ready". | [Ref: §40] |
| **RDY-4** | Readiness is re-evaluated each cycle (§39); prior readiness **MUST NOT** persist across material change (§36). | [Ref: §39; §36] |
| **RDY-5** | Detailed gate criteria are the per-state criteria of §27; §41 defines composition only. | [Ref: §27; Development Order] |

---

## 42. Engineering Meta-Model

> **Phase boundary & positioning.** §42 is the **logical/architectural root** of the standard — the canonical model from which all engineering concepts and all later-phase specifications derive. Per the append-only execution rules it is **physically positioned** after §41 to preserve existing numbering; this placement is editorial only and does **not** subordinate it. Sections §1–§41 are **instances of, and consistent with,** this meta-model. Detailed schemas are deferred to Phases 2–8; §42 defines the meta-model only. [Ref: OMG MOF (Meta-Object Facility); ISO/IEC/IEEE 42010:2022 (architecture models & correspondences); Development Order]

### 42.1 Purpose

Defines the engineering entities and their relationships as one canonical meta-model, so every later artifact, stage, and rule derives from a single architecture. [Ref: OMG MOF; ISO 42010]

### 42.2 Canonical Entities

For each entity: Purpose, Inputs→Outputs, Key Relationships, Authority, Lifecycle Position (defining section).

| Entity | Purpose | Inputs → Outputs | Key Relationships | Authority | Defined in |
|---|---|---|---|---|---|
| **Mission** | Authorize & bound a task | goal → bounded task | owns Operations; requires Evidence | Authoritative | §32 |
| **State** | Position in the engineering state machine | conditions → transition | contains Stages; gated by Validation | Authoritative | §33 |
| **Stage** | Gated unit of work | entry → exit | produces Artifacts | Authoritative | §13 |
| **Operation** | Defined engineering action | inputs → outputs | produces Evidence/Artifacts | Authoritative | §34 |
| **Artifact** | Work product | source → product | carries Knowledge; classified by Authority | Auth/Derived/Generated | §11 |
| **Evidence** | Justifying observation/result | observation → verified item | verifies Fact; provenance link | Carries confidence | §26, §28 |
| **Observation** | Raw captured datum | system → datum | becomes Evidence | Non-authoritative | §28 |
| **Fact** | Verified statement | evidence → fact | derives Knowledge | Candidate-authoritative | §14, §26 |
| **Knowledge** | Synthesized understanding | facts → knowledge | informs Decision | Authoritative | §14, §31 |
| **Decision** | Recorded engineering choice | knowledge+impact → decision | drives Implementation | Authoritative (immutable) | §35 |
| **Requirement** | Stated obligation | need → requirement | governed/verified | Authoritative | §8, §9 |
| **Constraint** | Non-negotiable boundary | context → constraint | bounds Mission/Decision | Authoritative | §23 |
| **Review** | Criteria-based examination | artifact → findings | gates Artifacts | Authoritative record | §15 |
| **Validation** | Objective conformance check | change → verdict | verifies Implementation | Authoritative record | §16 |
| **Documentation** | Categorized recorded knowledge | knowledge → document | documents Objects | Auth/Derived/Generated | §38 |
| **Repository** | Permanent engineering memory | all → versioned store | contains all Objects | Authoritative root store | §10, §31 |

### 42.3 Canonical Relationship Graph

```
Mission → Operation → Evidence → Fact → Knowledge → Decision
→ Implementation → Validation → Documentation → Repository
```

Governing cross-cuts: **Requirement** and **Constraint** govern; **Review** and **Validation** gate; **State** and **Stage** sequence; **Artifact** carries; **Repository** contains.

### 42.4 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **MM-1** | Every engineering concept in the standard **MUST** be an instance of a §42.2 entity. | [Ref: OMG MOF; PR-2] |
| **MM-2** | Entity relationships **MUST** conform to the Relationship Model (§44). | [Ref: §44] |
| **MM-3** | The meta-model is authoritative; later specifications **MUST** derive from it and **MUST NOT** introduce entities outside §42.2 without governance (§17). | [Ref: §17; RA-5] |
| **MM-4** | §1–§41 concepts are bound to §42.2 entities (§42.2 mapping); no contradiction **MAY** exist (NFR-11). | [Ref: NFR-11] |
| **MM-5** | Each entity **MUST** occupy a defined Lifecycle Position (§12 phase / §33 state). | [Ref: §12; §33] |

---

## 43. Engineering Object Model

> **Phase boundary.** §43 defines the **object schema**; storage/templates are Phase-2/Phase-8. Architecture only. [Ref: Development Order]

### 43.1 Purpose

A unified object model: every engineering object is an instance with mandatory fields, **generalizing** the Artifact metadata (§11.2). [Ref: OMG UML class model; ISO 42010; extends §11]

### 43.2 Mandatory Object Fields

| Field | Meaning | Source |
|---|---|---|
| **Object ID** | Unique identifier | §11.2 |
| **Object Type** | A §42.2 entity | §42 |
| **Authority Class** | Authoritative / Derived / Generated | §11.1 |
| **Owner** | Single accountable owner | §11.2 |
| **Lifecycle State** | Current §33 state | §33 |
| **Status** | Draft/Accepted/Superseded/Deprecated | §11.2 |
| **Version** | Semantic version | §18 |
| **Parent Objects** | Containing/owning objects | §44 (contains/owns) |
| **Child Objects** | Contained objects | §44 |
| **Incoming Relationships** | Edges into the object | §44 |
| **Outgoing Relationships** | Edges out of the object | §44 |
| **Evidence References** | Provenance links | §26, §28 |
| **Decision References** | Authorizing decision(s) | §35 |
| **Repository Location** | Canonical location | §10 |
| **Traceability Links** | Graph node links | §48 |

### 43.3 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **OM-1** | Every engineering object **MUST** carry all fifteen fields (§43.2). | [Ref: §11.2 (superset); PR-5] |
| **OM-2** | No engineering object **MAY** exist outside this model. | [Ref: Engineering Review Order; MM-1] |
| **OM-3** | Object Type **MUST** be a §42.2 entity; Authority Class **MUST** be from §11.1. | [Ref: §42; §11.1] |
| **OM-4** | Incoming/outgoing relationships **MUST** be Relationship Model (§44) types. | [Ref: §44] |
| **OM-5** | These fields are a **superset of, and consistent with,** §11.2 artifact metadata (artifacts are objects). | [Ref: §11.2; NFR-11] |
| **OM-6** | Generated/Derived objects **MUST** remain reproducible (RA-4); their fields **MUST NOT** be hand-forged. | [Ref: RA-4; PR-6] |

---

## 44. Engineering Relationship Model

> **Phase boundary.** §44 defines canonical **edge types**; link schemas are Phase-4/Phase-8. Architecture only. [Ref: Development Order]

### 44.1 Purpose

Canonical relationship (edge) types connecting objects (§43); consolidates relationships dispersed across §11/§29/§31/§35. [Ref: Chen, ER Model, 1976; OMG UML associations/dependencies; ISO 42010 correspondences]

### 44.2 Relationship Types

| Relationship | Direction · Cardinality | Allowed (from → to) | Constraint / Traceability |
|---|---|---|---|
| **depends_on** | directed · n:n | object → object | acyclic at authority level (§45, §49); dependency trace |
| **produces** | directed · 1:n | Operation/Stage → Artifact/Evidence | forward trace |
| **consumes** | directed · n:n | Operation → Artifact/Evidence | backward trace |
| **owns** | directed · 1:n | Owner → object | exactly one owner (CON-3) |
| **implements** | directed · 1:1+ | Implementation → Decision | each impl → one Decision (DEC-4) |
| **validates** | directed · n:1 | Validation → Implementation | verdict recorded |
| **documents** | directed · n:1 | Documentation → object | category declared (§38) |
| **references** | directed · n:n | object → object | must resolve (CON-4) |
| **supersedes** | directed · 1:1 | new → old | old retained as Historical (RKA-3) |
| **derives_from** | directed · n:1 | Derived → Authoritative | not hand-edited (PR-6) |
| **generated_from** | directed · n:1 | Generated → source | reproducible (RA-4) |
| **verified_by** | directed · 1:n | Fact → Evidence/Validation | confidence (§26) |
| **reviewed_by** | directed · n:n | Artifact → Review | review recorded (§15) |
| **approved_by** | directed · n:1 | Decision → Authority | governance (§17) |
| **blocks** | directed · n:n | object → object | blocks transition (STA-2) |
| **requires** | directed · n:n | object → object | must resolve (CON-5) |
| **contains** | directed · 1:n | container → member | parent/child (§43) |
| **extends** | directed · n:1 | Extension → Core | may only add/strengthen (EX-4) |

### 44.3 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **REL-1** | Every object relationship **MUST** be one of the §44.2 types. | [Ref: §43; ER/UML] |
| **REL-2** | A relationship **MUST** connect existing objects (no dangling endpoint) — referential integrity. | [Ref: Codd referential integrity; §49] |
| **REL-3** | derives_from / generated_from **MUST** point to authoritative sources; the dependent object **MUST NOT** be hand-edited. | [Ref: PR-6; RA-4] |
| **REL-4** | supersedes **MUST** preserve the superseded object as Historical (RKA-3); it **MUST NOT** delete it. | [Ref: RKA-3; KN-2] |
| **REL-5** | depends_on **MUST NOT** form prohibited authority/dependency cycles (§45, §49). | [Ref: Acyclic Dependencies Principle; §45; §49] |
| **REL-6** | Each relationship's traceability behavior **MUST** support the trace directions of §48. | [Ref: §48] |

---

## 45. Engineering Dependency Graph

> **Phase boundary.** §45 declares the standard's **derivation dependencies**; the generated machine-readable graph is a Phase-2 artifact. Architecture only. [Ref: Development Order]

### 45.1 Purpose

Formal dependency declaration making derivation/execution order deterministic. [Ref: Graph theory (DAG / topological order); R. C. Martin, Acyclic Dependencies Principle; Dependency Structure Matrix]

### 45.2 Dependency Declaration

**Global drivers** (depended on by all): §1–§9 (esp. §7 Principles), §42 Meta-Model, §46 Vocabulary.
**Cross-cutting** (apply to all): §17 Governance, §18 Versioning, §19 Extension, §40 Integrity, §49 Consistency.

**Topological layers** (a section MAY depend only on equal-or-lower layers):

| Layer | Sections |
|---|---|
| **L0 Foundations** | §7, §42, §43, §44, §46 |
| **L1 Evidence/Knowledge** | §11, §14, §26, §28, §31, §47, §29, §48 |
| **L2 Initiation/Discovery** | §32, §33, §34, §25, §30 |
| **L3 Reasoning** | §35, §36, §37, §12, §13 |
| **L4 Assurance** | §15, §16, §38 |
| **L5 Gates** | §27, §41, §50 |
| **Cross** | §17, §18, §19, §40, §49 |

**Principal dependency table (meta layer):**

| Section | Depends On | Produces | Consumes | Required By | Blocks · Enables |
|---|---|---|---|---|---|
| **§42 Meta-Model** | §7, §46 | entity set | — | all model sections | enables all derivation |
| **§43 Object Model** | §42, §11 | object schema | §11.2 | §44, §48, §49 | enables object integrity |
| **§44 Relationship Model** | §42, §43 | edge types | — | §45, §48, §49 | enables graph traceability |
| **§45 Dependency Graph** | §42, §44 | order | §44 | §50, governance | enables deterministic order |
| **§46 Vocabulary** | §7 | canonical terms | — | all sections, App. B | blocks term redefinition |
| **§47 Information Model** | §28, §26 | transition rules | §28 | §16, §48 | enables flow control |
| **§48 Traceability Graph** | §43, §44, §29 | trace graph | §29 | §49, §50, App. C | enables impact/trace |
| **§49 Consistency Rules** | §43, §44, §48 | invariants | — | §41, §50 | blocks non-conformant repo |
| **§50 Completeness Model** | §27, §41, §49 | completeness metrics | §49 | Mission close | gates repository done |

### 45.3 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **DEP-1** | Every architectural section **MUST** declare its dependencies (§45.2); no implicit dependency **MAY** remain. | [Ref: Engineering Review Order; DSM] |
| **DEP-2** | The dependency graph **MUST** be acyclic at the authority level (no circular authority). | [Ref: Acyclic Dependencies Principle; CON-6] |
| **DEP-3** | Derivation/execution order **MUST** respect the topological order (§45.2). | [Ref: Graph theory] |
| **DEP-4** | Adding a section **MUST** update the graph under governance (§17) and versioning (§18). | [Ref: §17; §18] |

---

## 46. Canonical Engineering Vocabulary

> **Authority note.** §46 is the **authoritative** vocabulary. **Appendix B (Glossary) is a derived convenience view** of §46 and introduces no independent authority (prevents duplicate authority, CON-2). On conflict, §46 governs. [Ref: ISO/IEC/IEEE 24765 SEVOCAB; Evans, DDD — Ubiquitous Language; PR-6]

### 46.1 Purpose

Defines the official engineering language; no later document may redefine these terms. [Ref: ISO/IEC/IEEE 24765; DDD ubiquitous language]

### 46.2 Canonical Terms

| Term | Definition | Forbidden synonyms | Related | Status |
|---|---|---|---|---|
| **Artifact** | A versioned engineering work product (§11). | "doc", "file" (when meaning a work product) | Object, Documentation | Normative |
| **Evidence** | A provenance-bearing item justifying a fact (§26/§28). | "proof" | Observation, Fact | Normative |
| **Fact** | A verified statement with confidence (§14/§26). | "truth" (informal) | Evidence, Knowledge | Normative |
| **Observation** | A raw, pre-verification datum (§28). | "finding" (when unverified) | Evidence | Normative |
| **Knowledge** | Synthesized understanding from facts (§14/§31). | "info" | Fact, Decision | Normative |
| **Decision** | An immutable-once-approved engineering choice (§35). | "choice", "call" | ADR, Rationale | Normative |
| **Mission** | The authorizing, bounded task definition (§32). | "ticket", "task" (informal) | Operation, Scope | Normative |
| **Repository** | The permanent engineering memory (§10/§31). | "repo" (informal), "codebase" | Object, Knowledge | Normative |
| **Validation** | Objective conformance check — "right thing" (§16). | "testing" (narrow) | Verification, Review | Normative |
| **Verification** | Conformance to specification — "built right" (§16). | "validation" (must not conflate) | Validation | Normative |
| **Discovery** | Unknown→understood transformation (§25). | "exploration" | Recovery, Analysis | Normative |
| **Recovery** | Producing higher-level abstractions from artifacts (§30). | "reverse" (informal) | Discovery | Normative |
| **Analysis** | Examination producing engineering conclusions (§12). | "investigation" | Discovery, Impact | Normative |
| **Planning** | Producing decisions/plans before change (§7/§35). | "design" (narrow) | Decision | Normative |
| **Implementation** | Realizing an approved decision (§12). | "coding" | Decision, Validation | Normative |
| **Review** | Criteria-based examination (§15). | "approval" (narrow) | Validation | Normative |
| **Constraint** | A non-negotiable boundary (§23). | "limit" | Requirement | Normative |
| **Requirement** | A stated, verifiable obligation (§8/§9). | "feature", "spec" | Constraint | Normative |
| **Operation** | A defined action with pre/postconditions (§34). | "step", "action" | Mission, Stage | Normative |
| **State** | A position in the engineering state machine (§33). | "status" (must not conflate) | Stage, Transition | Normative |
| **Stage** | A gated unit of work (§13). | "phase" (informal) | State, Operation | Normative |

> **Reserved / deprecated:** terms not in §46.2 used for these concepts are **deprecated**; "Status" is **reserved** for the object field (§43) and **MUST NOT** be used as a synonym for "State".

### 46.3 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **VOC-1** | The §46.2 terms are canonical; no later document **MAY** redefine them. | [Ref: ISO 24765; PR-6] |
| **VOC-2** | Forbidden synonyms **MUST NOT** be used for a canonical concept in authoritative artifacts. | [Ref: DDD ubiquitous language] |
| **VOC-3** | Appendix B is **derived** from §46 and **MUST NOT** diverge; on conflict, §46 governs. | [Ref: PR-6; CON-2] |
| **VOC-4** | New or changed terms **MUST** pass governance (§17) and versioning (§18). | [Ref: §17; §18] |

---

## 47. Engineering Information Model

> **Phase boundary.** §47 defines information-flow **architecture**; the operational flow procedure is Phase-3. Architecture only. [Ref: Development Order]

### 47.1 Purpose

Defines how information transforms from observation to repository, **generalizing the Evidence Chain (§28)** with per-transition attributes. The chain (§28) is its backbone; §47 is consistent with it. [Ref: §28; W3C PROV; DIKW (§31)]

### 47.2 Information Transitions

```
Observation → Evidence → Verification → Fact → Knowledge → Decision
→ Implementation → Validation → Documentation → Repository
```

| Transition | Input → Output | Required Evidence | Authority | Confidence | Verification | Blocking Condition |
|---|---|---|---|---|---|---|
| Observation→Evidence | datum → evidence | provenance | non-auth | A/B/E | recorded | missing provenance |
| Evidence→Fact | evidence → fact | verification pass | candidate | ≥ verified | §16/§28 | unverified |
| Fact→Knowledge | facts → knowledge | corroboration | auth | triangulated | review (§15) | single-source where multi required |
| Knowledge→Decision | knowledge+impact → decision | impact analysis (§36) | auth | — | approval (§17) | no impact analysis |
| Decision→Implementation | decision → change | approved decision | auth | — | §16 | unapproved decision |
| Implementation→Validation | change → verdict | tests/checks | auth | — | §16 | validation not run |
| Validation→Documentation | verdict → document | passing verdict | auth/derived | — | §15 | failed validation |
| Documentation→Repository | document → stored | category (§38) | per §11 | — | §17/§18 | uncategorized/ungoverned |

### 47.3 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **INF-1** | Information **MUST** progress only through the §47.2 transitions; skipping a transition is non-conformant. | [Ref: §28; ECH-4] |
| **INF-2** | Each transition **MUST** satisfy its Required Evidence, Authority, Confidence, and Verification before producing its Output. | [Ref: §16; §26; §28] |
| **INF-3** | A transition's Blocking Condition **MUST** halt progression until cleared. | [Ref: §40; §49] |
| **INF-4** | This model is consistent with the Evidence Chain (§28); on overlap, the §28 backbone governs ordering. | [Ref: §28; NFR-11] |

---

## 48. Engineering Traceability Graph

> **Phase boundary.** §48 defines the **graph architecture**; the generated graph is a Phase-2 artifact. Architecture only. [Ref: Development Order]

### 48.1 Purpose

Generalizes Appendix C and §29 from requirements to **all** engineering objects (§43) connected by relationships (§44). [Ref: Gotel & Finkelstein 1994; ISO/IEC/IEEE 29148; §29; §43; §44]

### 48.2 Node Types & Trace Directions

```
Mission → State → Stage → Operation → Evidence → Fact → Knowledge
→ Decision → Artifact → Implementation → Validation → Documentation → Repository
```

Each node **SHALL** support: **Forward Trace; Backward Trace; Impact Trace; Dependency Trace; Evidence Trace; Decision Trace.**

### 48.3 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **TGR-1** | Every engineering object **MUST** be a node in the traceability graph; no object **MAY** be orphaned. | [Ref: CON-1; Gotel & Finkelstein 1994] |
| **TGR-2** | The graph **MUST** support all six trace directions (§48.2) bidirectionally. | [Ref: §29; TRC-1] |
| **TGR-3** | The graph is built from Object nodes (§43) and Relationship edges (§44); it introduces no new node/edge types. | [Ref: §43; §44] |
| **TGR-4** | The traceability graph **SHOULD** be a generated artifact (§11), not hand-maintained. | [Ref: PR-6; TRC-3] |
| **TGR-5** | Appendix C is a requirements-scoped **view** of this graph and **MUST** remain consistent with it. | [Ref: CON-4; Appendix C] |

---

## 49. Engineering Consistency Rules

> **Constitutional / repository invariants.** Violation renders the repository **non-conformant** (§16). §49 complements §40 (documentation completeness) with **structural** integrity. **Marked status:** the invariants restate established integrity principles (referential integrity; acyclic dependencies; single source of truth); the specific list is **SES-constitutional (converged practice)**. [Ref: Codd referential integrity; R. C. Martin Acyclic Dependencies Principle; ISO 42010 correspondence consistency; PR-6]

### 49.1 Invariants

| ID | Invariant | Evidence |
|---|---|---|
| **CON-1** | **No orphan object** (artifact/decision/evidence/requirement/validation): every object **MUST** have ≥1 valid relationship and a traceability node (§48). | [Ref: §48; Gotel & Finkelstein] |
| **CON-2** | **No duplicate authority:** each fact has **exactly one** authoritative object (§11/§46). | [Ref: PR-6; RA-3] |
| **CON-3** | **No duplicate ownership:** each object has **exactly one** Owner (§43). | [Ref: §43] |
| **CON-4** | **No broken traceability:** every traceability link **MUST** resolve to an existing node. | [Ref: §48; referential integrity] |
| **CON-5** | **No broken dependency:** every depends_on / requires **MUST** resolve (§45). | [Ref: §45; referential integrity] |
| **CON-6** | **No circular authority:** the authority/dependency graph **MUST** be acyclic. | [Ref: §45; Acyclic Dependencies Principle] |
| **CON-7** | **No conflicting lifecycle state:** an object **MUST** be in exactly one State (§33). | [Ref: STA-1] |
| **CON-8** | **No invalid relationship:** every relationship **MUST** be a §44 type with allowed endpoints. | [Ref: §44; REL-1] |

### 49.2 Enforcement

| ID | Rule | Evidence |
|---|---|---|
| **CON-9** | Any invariant violation renders the repository **non-conformant** (§16) and **MUST** block Readiness (§41) and Completeness (§50). | [Ref: §16; §41; §50] |

---

## 50. Engineering Completeness Model

> **Phase boundary.** §50 defines **repository-level completeness dimensions**; metric thresholds are Phase-6 (validation). Architecture only. [Ref: Development Order]

### 50.1 Purpose

Defines **repository-level** completeness — beyond per-work completion (§27) and readiness (§41) — including the meta-structures. [Ref: ISO/IEC 25012 (completeness as a data-quality characteristic); ISO/IEC/IEEE 29148 (requirements completeness); §27; §41]

### 50.2 Completeness Dimensions

| Dimension | Objective metric (architecture-level) | Source |
|---|---|---|
| **Repository** | All mandatory object classes present & governed | §10, §31 |
| **Knowledge** | §27 *Knowledge Complete* met | §27 |
| **Architecture** | §27 *Architecture Complete* met | §27 |
| **Documentation** | §27 *Documentation Complete*; §38 categories satisfied | §38 |
| **Traceability** | §48 graph complete; no orphans (CON-1) | §48, §49 |
| **Validation** | §27 *Validation Complete* met | §16, §27 |
| **Discovery** | §27 *Discovery Complete* met | §25, §27 |
| **Dependencies** | §45 graph declared & acyclic (CON-6) | §45 |
| **Evidence** | All facts carry confidence + provenance (INT-10) | §26, §28 |
| **Decisions** | Every implementation traces to a Decision (DEC-4) | §35 |
| **Relationships** | All relationships valid (CON-8) | §44 |
| **Objects** | All objects carry mandatory fields (OM-1) | §43 |
| **Vocabulary** | All canonical terms defined; no redefinition (VOC-1) | §46 |
| **Meta-Model** | All concepts bound to §42.2 entities (MM-1) | §42 |

### 50.3 Normative Rules

| ID | Rule | Evidence |
|---|---|---|
| **CPL-1** | Repository Completeness **REQUIRES** every mandatory completeness dimension (§50.2) to pass. | [Ref: §27; ISO/IEC 25012] |
| **CPL-2** | Each dimension's metric **MUST** be objective and verifiable (§16). | [Ref: PR-7; §16] |
| **CPL-3** | Completeness **MUST NOT** be asserted while any §49 invariant is violated or any §40 integrity rule fails. | [Ref: §40; §49] |
| **CPL-4** | Repository Completeness is a precondition of "Repository Ready" (§41) where the Mission requires it. | [Ref: §41; §32] |
| **CPL-5** | Detailed metric thresholds are deferred to Phase 6; §50 defines dimensions only. | [Ref: Development Order] |

---

## Appendix A — Evidence Base (Normative References)

This appendix is the approved citation base for the standard. Per RK-6/AS-5, **exact clause numbers, editions, and pagination SHOULD be re-verified against the primary documents before a MAJOR release.** Sources are real and citable; recalled edition details are flagged where uncertain.

**Standards & bodies of knowledge**
- ISO/IEC/IEEE 12207:2017 — Systems and software engineering — Software life cycle processes.
- ISO/IEC/IEEE 15288:2023 — System life cycle processes.
- ISO/IEC/IEEE 42010:2022 — Software, systems and enterprise — Architecture description.
- ISO/IEC/IEEE 29148:2018 — Requirements engineering.
- ISO/IEC 25010:2011 (and :2023 revision) — Systems and software Quality Requirements and Evaluation (SQuaRE) — Quality model.
- ISO/IEC/IEEE 14764:2022 — Software maintenance.
- ISO/IEC/IEEE 1012-2016 — System, software, and hardware verification and validation.
- ISO/IEC/IEEE 29119 (Parts 1–4) — Software testing.
- ISO/IEC/IEEE 26515 — Developing information for users in an agile environment (doc structuring).
- IEEE Std 1016-2009 — Software Design Descriptions.
- IEEE Std 1028-2008 — Software Reviews and Audits.
- IEEE Computer Society, SWEBOK Guide (V3, 2014; V4, 2024).
- RFC 2119; RFC 8174 — Requirement keyword usage.
- RFC 9110 — HTTP Semantics.
- RFC 8594 — The Sunset HTTP Header Field (deprecation signaling).
- Semantic Versioning 2.0.0 — semver.org.
- "Keep a Changelog" — changelog convention.
- OpenAPI Specification; AsyncAPI Specification; Protocol Buffers / gRPC — contract formats.

**Foundational papers**
- E. Chikofsky, J. Cross, "Reverse Engineering and Design Recovery: A Taxonomy," IEEE Software, 1990.
- M. M. Lehman, "Programs, Life Cycles, and Laws of Software Evolution," Proc. IEEE, 1980.
- M. Conway, "How Do Committees Invent?", Datamation, 1968.
- A. von Mayrhauser, A. Vans, "Program Comprehension During Software Maintenance and Evolution," IEEE Computer, 1995.
- B. Lientz, E. Swanson, *Software Maintenance Management*, 1980 (maintenance categories).
- B. Boehm, "Software Risk Management: Principles and Practices," IEEE Software, 1991.

**Practitioner literature**
- L. Bass, P. Clements, R. Kazman, *Software Architecture in Practice*, 4th ed., 2021.
- M. Feathers, *Working Effectively with Legacy Code*, 2004.
- E. Evans, *Domain-Driven Design*, 2003.
- M. Fowler, *Refactoring*, 2nd ed., 2018; and martinfowler.com patterns: StranglerFigApplication, ConsumerDrivenContracts, MonolithFirst, TestPyramid, ParallelChange.
- S. Newman, *Building Microservices*, 2nd ed., 2021; *Monolith to Microservices*, 2019.
- N. Ford, R. Parsons, P. Kua, *Building Evolutionary Architectures*, 2017/2022.
- M. Nygard, *Release It!*, 2nd ed.; "Documenting Architecture Decisions," 2011 (ADR).
- B. Beyer et al., *Site Reliability Engineering*, Google, 2016; *The Site Reliability Workbook*, 2018.
- N. Forsgren, J. Humble, G. Kim, *Accelerate*, 2018; DORA "State of DevOps" reports.
- T. Winters, T. Manshreck, H. Wright, *Software Engineering at Google*, 2020; Google Engineering Practices (eng-practices, public).
- S. Demeyer, S. Ducasse, O. Nierstrasz, *Object-Oriented Reengineering Patterns*, 2002.
- B. Meyer, *Object-Oriented Software Construction* (Design by Contract).
- B. Boehm, R. Turner, *Balancing Agility and Discipline*, 2003.
- M. Brodie, M. Stonebraker, *Migrating Legacy Systems*, 1995.
- The Twelve-Factor App — 12factor.net.
- arc42 architecture documentation template — arc42.org.
- C4 model — c4model.com (S. Brown).
- Linux kernel development process documentation; Apache Software Foundation / CNCF governance; IETF RFC process — as governance-model references.

**Evidence for Phase-1 review extensions (§25–§31)**
- B. Kitchenham, T. Dybå, M. Jørgensen, "Evidence-Based Software Engineering," Proc. ICSE 2004 — evidence hierarchies in software engineering (basis for the §26 confidence-grading *principle*).
- GRADE Working Group (Guyatt et al., BMJ 2008) — "confidence in evidence" grading (cross-domain analog for §26; the A–E tiers are the SES-adopted scheme, **not** the GRADE tiers).
- NIST SP 800-86, "Guide to Integrating Forensic Techniques into Incident Response," 2006 — evidence handling and chain of custody (basis for §26 fact fields and §28 chain).
- W3C PROV-DM / PROV-O (W3C Recommendation, 2013) — provenance data model (basis for §28 provenance links).
- O. Gotel, A. Finkelstein, "An Analysis of the Requirements Traceability Problem," Proc. ICRE 1994 — seminal traceability reference (basis for §29 bidirectional traceability).
- K. Schwaber, J. Sutherland, *The Scrum Guide* — "Definition of Done" (converged-practice basis for §27 completion criteria; the completion-state set is the SES-adopted model).
- E. Eilam, *Reversing: Secrets of Reverse Engineering*, 2005 — binary/protocol reverse-engineering context for §30.4 (activities only; tools out of core scope).
- R. Ackoff, "From Data to Wisdom," J. Applied Systems Analysis, 1989 — DIKW hierarchy (knowledge-management **analogy** for §31 knowledge progression; not a software-engineering standard).

**Evidence for Phase-1 completion extensions (§32–§41)**
- ISO/IEC/IEEE 12207:2017 — Project Planning process (basis for §32 Mission elements; reused from the standards list).
- ISO/IEC/IEEE 15288:2023 — life-cycle stages (basis for §33 state model; reused from the standards list).
- OMG, *Unified Modeling Language (UML) 2.x Specification* — State Machines (formalism for §33).
- B. Meyer, *Object-Oriented Software Construction* — Design by Contract: pre/postconditions (basis for §34 operation contracts; reused).
- ISO/IEC/IEEE 42010:2022 — architecture decisions and rationale (basis for §35 Decision fields; reused). MADR (Markdown Architecture Decision Records) template, adr.github.io — converged-practice field set for §35.
- S. Bohner, R. Arnold, *Software Change Impact Analysis*, IEEE CS Press, 1996; ISO/IEC/IEEE 14764:2022 (impact analysis in maintenance) — basis for §36.
- G. Murphy, D. Notkin, K. Sullivan, "Software Reflexion Models: Bridging the Gap Between Source and High-Level Models," IEEE TSE, 2001 — basis for §37 conformance comparison.
- "Definition of Ready" — agile community converged practice (basis for §41 readiness gates; the gate set is the SES-adopted composition of §27).

**Evidence for Phase-1 meta-architecture extensions (§42–§50)**
- OMG, *Meta-Object Facility (MOF) Specification* — meta-modeling (basis for §42 meta-model; the layered "model of models" concept).
- OMG, *Unified Modeling Language (UML) 2.x Specification* — class/object modeling and association/dependency/generalization (basis for §43 object model, §44 relationship types).
- P. Chen, "The Entity-Relationship Model — Toward a Unified View of Data," ACM TODS, 1976 — entity/relationship modeling (basis for §44).
- ISO/IEC/IEEE 42010:2022 — architecture models, **correspondences and correspondence rules** (basis for §44 relationships and §49 consistency).
- E. F. Codd, relational model — referential integrity (basis for §49 "no broken/orphan reference" invariants).
- R. C. Martin — Acyclic Dependencies Principle (basis for §45/§49 acyclicity; "no circular authority"). Dependency Structure Matrix (DSM) — dependency representation.
- Graph theory — directed acyclic graphs and topological ordering (basis for §45 deterministic order).
- ISO/IEC/IEEE 24765 — Systems and Software Engineering Vocabulary (SEVOCAB) (basis for §46 canonical vocabulary); E. Evans, *Domain-Driven Design* — Ubiquitous Language (reused).
- W3C PROV-DM / PROV-O (reused) — provenance for §47 information transitions.
- O. Gotel, A. Finkelstein, ICRE 1994 (reused); ISO/IEC/IEEE 29148:2018 (reused) — basis for §48 traceability graph.
- ISO/IEC 25012 — data quality model, **completeness** characteristic (basis for §50 completeness dimensions); ISO/IEC/IEEE 29148 — requirements completeness (reused).

**Marked status notes**
- The *fast-feedback validation ordering* (§16.3): the layers are standardized; the specific ordering is **converged practice**, with competing weightings (testing trophy vs pyramid).
- The application of ISO/IEC 25010 to a *standard-as-product* (§9): **converged practice**, a reasonable extension, not a formal mandate.
- Any claim about specific AI tools' memory/context limitations (§2.3): **UNSUPPORTED** as formally cited; supported only in the general principle of externalizing durable knowledge.
- The **five-tier confidence scheme A–E** (§26): the *principle* of grading engineering facts by evidence strength is **evidence-based** (Kitchenham/EBSE; GRADE analog; forensic chain of custody); the **specific tier labels and ordering** are the **SES-adopted classification (converged practice)**, not a verbatim external standard.
- The **completion-state set** (§27) and **knowledge-class set** (§31): **converged practice** — the underlying principles (objective exit criteria / Definition of Done; DIKW progression; artifact authority) are cited; the specific enumerations are SES-adopted models consistent with those principles.
- The **DIKW hierarchy** (§31) is a knowledge-management model used by **analogy**; its application to repository engineering memory is **converged practice**, not a software-engineering standard.
- The **Mission element set** (§32), the **state set** (§33), the **operation set** (§34), the **comparison-pair set** (§37), the **documentation-category set** (§38), the **per-cycle output set** (§39), the **integrity-invariant set** (§40), and the **readiness-gate set** (§41): in each case the underlying *principle* is cited and evidence-based; the **specific enumeration is the SES-adopted model (converged practice)** consistent with that principle.
- The **"Definition of Ready"** (§41) is agile **converged practice**, not a formal standard; §41 binds it to the objective Completion States of §27.
- The **entity set** (§42.2), **object-field set** (§43.2), **relationship-type set** (§44.2), **canonical-term set** (§46.2), **information-transition set** (§47.2), **trace-direction set** (§48.2), **consistency-invariant set** (§49), and **completeness-dimension set** (§50.2): in each case the underlying *principle* (MOF/UML/ER modeling; referential integrity; acyclic dependencies; SEVOCAB vocabulary control; ISO 25012 completeness) is cited and evidence-based; the **specific enumeration is the SES-adopted model (converged practice)** consistent with that principle.

---

## Appendix B — Glossary

> **Authority note (added v0.4.0).** This glossary is a **derived** convenience view of the **authoritative** Canonical Engineering Vocabulary (§46). It introduces no independent authority; on any conflict, **§46 governs** (VOC-3, CON-2).

| Term | Definition |
|---|---|
| **SES** | Software Engineering Standard — the subject of this SDD. |
| **Authoritative artifact** | The single source of truth for some fact/decision; hand-authored. |
| **Derived artifact** | Produced by transforming authoritative artifacts; not hand-edited. |
| **Generated artifact** | Mechanically produced; reproducible; not hand-edited. |
| **Provenance** | A link from a recorded fact to the source evidence that justifies it. |
| **Invariant** | A constraint that must remain true across changes. |
| **Contract** | An agreed interface plus its semantics across a boundary. |
| **ADR** | Architecture Decision Record; immutable once accepted. |
| **Conformance assertion** | A recorded, evidenced statement that a project satisfies the SES at a stated version. |
| **Core / Extension** | The technology-independent base of the standard vs context-specific additions. |
| **UNSUPPORTED** | Marker for a statement that cannot be backed by the evidence base; non-normative. |
| **Confidence Level (A–E)** | The graded strength of evidence behind an engineering fact (§26). |
| **Evidence Chain** | The ordered, provenance-preserving path from observation to maintenance (§28). |
| **Discovery** | The process by which an unknown system becomes an understood system (§25). |
| **Recovery** | Production of higher-level abstractions from lower-level artifacts during reverse engineering (§30). |
| **Completion state** | A named point whose objective, verifiable exit criteria define when a body of engineering work is complete (§27). |
| **Repository memory** | The permanent, version-controlled engineering-knowledge classes that survive sessions, tools, and people (§31). |
| **Mission** | The authorizing, bounded definition of an engineering task; no activity starts without one (§32). |
| **Engineering state** | A named position in the engineering state machine, gated by entry/exit conditions (§33). |
| **Operation** | A defined engineering action specified by pre/postconditions (§34). |
| **Decision (engineering)** | A first-class, immutable-once-approved record of an engineering choice and its rationale (§35). |
| **Impact analysis** | The mandatory pre-modification assessment of a change's propagation across components, data, APIs, security, tests, docs, and deployment (§36). |
| **Comparison** | An examination that produces difference-evidence between two subjects, never opinion (§37). |
| **Integrity invariant** | A constitutional "no undocumented X" completeness rule (§40). |
| **Readiness gate** | An objective composition of completion states determining fitness for implementation (§41). |

---

## Appendix C — Requirements Traceability Index

This index (a **generated** artifact per §11) links Principles → Requirements → Verification → Success Criteria. It is reproduced here for Phase 1; in operation it **MUST** be generated, not hand-maintained (PR-6).

| Requirement | Traces to Principle(s) | Verified by | Success Criterion |
|---|---|---|---|
| FR-1 | PR-2 | Inspection | SC-1 |
| FR-2, FR-3 | PR-6 | Inspection | SC-5 |
| FR-4 | PR-7, PR-8 | Inspection | SC-7 |
| FR-5 | PR-5 | Inspection | SC-6 |
| FR-6 | PR-8 | Inspection | SC-7 |
| FR-7 | PR-7 | Inspection | SC-7 |
| FR-8 | PR-10 | Inspection | SC-8 |
| FR-9 | PR-10 | Inspection | SC-8 |
| FR-10 | PR-11, PR-12 | Inspection | SC-1 |
| FR-11 | PR-1 | Analysis | SC-2 |
| FR-12 | PR-12 | Inspection | SC-3 |
| FR-13 | PR-3 | Demonstration | SC-9 |
| FR-14 | PR-5, PR-7 | Inspection | SC-7 |
| FR-15 | PR-7 | Inspection | SC-8 |
| FR-16 | PR-3 | Analysis | SC-4 |
| FR-17 | PR-4, PR-6 | Inspection | SC-5 |
| NFR-1..NFR-13 | PR-1,3,5,6,7,10,11 | A/D/I per §9 | SC-2,4,9,10 |
| DSC-1..DSC-6 (§25) | PR-2, PR-5, PR-12 | Inspection / Analysis | SC-1, SC-6 |
| EVC-1..EVC-6 (§26) | PR-1, PR-5 | Inspection / Analysis | SC-2, SC-6 |
| CMP-1..CMP-5 (§27) | PR-7, PR-8 | Inspection | SC-7 |
| ECH-1..ECH-5 (§28) | PR-5 | Inspection / Analysis | SC-6 |
| TRC-1..TRC-5 (§29) | PR-5, PR-7 | Inspection | SC-7 |
| REV-1..REV-6 (§30) | PR-2, PR-5 | Inspection | SC-1, SC-3 |
| RKA-1..RKA-6 (§31) | PR-4, PR-6 | Inspection | SC-5 |
| MIS-1..MIS-6 (§32) | PR-7, PR-10, PR-5 | Inspection | SC-7 |
| STA-1..STA-5 (§33) | PR-7, PR-5 | Inspection | SC-7 |
| OPS-1..OPS-4 (§34) | PR-5, PR-8 | Inspection | SC-7 |
| DEC-1..DEC-5 (§35) | PR-5 | Inspection | SC-6 |
| IMP-1..IMP-5 (§36) | PR-5, PR-7 | Inspection | SC-7 |
| CPM-1..CPM-4 (§37) | PR-1, PR-5 | Inspection / Analysis | SC-2, SC-6 |
| DOC-1..DOC-5 (§38) | PR-6 | Inspection | SC-5 |
| EVO-1..EVO-4 (§39) | PR-4, PR-9 | Inspection | SC-5 |
| INT-1..INT-10 (§40) | PR-5 | Inspection / Analysis | SC-6 |
| RDY-1..RDY-5 (§41) | PR-7 | Inspection | SC-7 |
| MM-1..MM-5 (§42) | PR-2, PR-10 | Inspection | SC-1, SC-3 |
| OM-1..OM-6 (§43) | PR-5, PR-6 | Inspection | SC-5, SC-6 |
| REL-1..REL-6 (§44) | PR-5, PR-6 | Inspection | SC-6 |
| DEP-1..DEP-4 (§45) | PR-7, PR-10 | Inspection / Analysis | SC-7, SC-10 |
| VOC-1..VOC-4 (§46) | PR-6 | Inspection | SC-9, SC-10 |
| INF-1..INF-4 (§47) | PR-5 | Inspection | SC-6 |
| TGR-1..TGR-5 (§48) | PR-5, PR-6 | Inspection | SC-6 |
| CON-1..CON-9 (§49) | PR-5, PR-6 | Inspection / Analysis | SC-6, SC-10 |
| CPL-1..CPL-5 (§50) | PR-7 | Inspection | SC-7, SC-10 |

---

**END OF SDD — Phase 1 deliverable.**

*Status: DRAFT v0.4.0. Awaiting review per the Review Model (§15, Inspection per RV-2). No further phase artifacts (SOP, stages, templates, examples) are produced until this SDD is reviewed and accepted. Revisions 0.2.0–0.4.0 add architectural models §25–§50 under successive Engineering Review Orders; existing sections 1–24 and all existing requirement IDs are preserved unchanged.*
