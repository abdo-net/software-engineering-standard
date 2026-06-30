# Competing Approaches

> **Artifact ID:** CA-SES-001
> **Authority Class:** Authoritative
> **SDD Authority:** §12.4, §30.4, PR-12, FR-12
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 3

## 1. Purpose

This document presents and context-binds the competing engineering approaches that the Phase-3 lifecycle specification MUST address, per PR-12 (context-sensitivity over dogma) and FR-12. [Ref: §12.4; §7 PR-12; §8 FR-12] The SES SHALL NOT dogmatically choose a single approach where the evidence base shows multiple valid context-dependent practices. [Ref: §12.4] Each tension SHALL be presented with its supporting evidence and the context factors that bind the choice. [Ref: PR-12; FR-12]

## 2. Scope

This document covers four documented approach tensions:

1. Plan-driven / architecture-first vs evolutionary / emergent design [Ref: §12.4, Tension 1]
2. Rewrite vs incremental modernization (Strangler Fig) [Ref: §12.4, Tension 2]
3. Monolith-first vs microservices [Ref: §12.4, Tension 3]
4. Source-available reverse engineering vs binary/protocol reverse engineering [Ref: §30.4]

Approach tensions outside these four are outside the scope of this document.

## 3. Normative Rules

- **CA-1** Where the evidence base shows multiple valid approaches, the Phase-3 lifecycle specification MUST present them, compare them, and bind the choice to context rather than mandating one. [Ref: PR-12]
- **CA-2** The SES SHALL present, compare, and context-bind competing approaches wherever the evidence base shows more than one valid practice. [Ref: FR-12]
- **CA-3** Each approach tension MUST cite supporting evidence from the approved evidence base (Appendix A of the SDD). [Ref: FR-11]
- **CA-4** No approach SHALL be presented as universally correct; context-binding rules MUST accompany each tension. [Ref: §12.4; PR-12]

## 4. Approach Tensions

### 4.1 Plan-Driven vs Evolutionary Design

#### 4.1.1 Description

This tension addresses whether system architecture is established comprehensively before implementation (plan-driven / architecture-first) or allowed to emerge through iterative implementation and feedback (evolutionary / emergent design). [Ref: §12.4, Tension 1]

- **Plan-driven / architecture-first approach:** The system's architecture is specified in detail before significant implementation begins. Changes to architecture after implementation starts are treated as high-cost events requiring formal governance. [Ref: Bass/Clements/Kazman, *Software Architecture in Practice*]
- **Evolutionary / emergent design approach:** Architecture emerges through iterative cycles of implementation, feedback, and guided change. Architectural fitness is validated continuously rather than asserted upfront. [Ref: Ford/Parsons/Kua, *Building Evolutionary Architectures*]

#### 4.1.2 Supporting Evidence

- Bass, Clements, and Kazman, *Software Architecture in Practice*: Architecture-first approaches reduce risk in systems where late architectural changes are prohibitively expensive. [Ref: §12.4, Tension 1]
- Ford, Parsons, and Kua, *Building Evolutionary Architectures*: Evolutionary approaches with fitness functions enable controlled architectural change in high-uncertainty environments. [Ref: §12.4, Tension 1]
- Boehm and Turner, *Balancing Agility and Discipline*, 2003: The selection between plan-driven and agile/evolutionary approaches is context-dependent on five home grounds (personnel, culture, size, criticality, dynamism); no single approach dominates universally. [Ref: §12.4, Tension 1; PR-12]

#### 4.1.3 Context-Binding Rules

- **CA-1.1** High cost-of-change, regulated, or safety-critical contexts favor the architecture-first approach. [Ref: §12.4, Tension 1]
- **CA-1.2** High-uncertainty, reversible, or rapidly-changing contexts favor the evolutionary approach. [Ref: §12.4, Tension 1]
- **CA-1.3** A project MAY combine both approaches: architecture-first for stable, high-cost-of-change elements; evolutionary for uncertain, rapidly-changing elements. [Ref: Boehm & Turner, 2003; PR-12]
- **CA-1.4** The choice MUST be recorded as a Decision (§35) with context justification. [Ref: §35; DEC-1]

#### 4.1.4 References

| Source | Citation | Relevance |
|---|---|---|
| Bass, Clements, Kazman | *Software Architecture in Practice* | Architecture-first evidence |
| Ford, Parsons, Kua | *Building Evolutionary Architectures* | Evolutionary architecture evidence |
| Boehm & Turner | *Balancing Agility and Discipline*, 2003 | Reconciliation framework |

[Ref: §12.4, Tension 1]

---

### 4.2 Rewrite vs Incremental Modernization

#### 4.2.1 Description

This tension addresses whether a legacy system is replaced through a complete rewrite (greenfield replacement) or through gradual, incremental modernization of components while the system remains operational (Strangler Fig). [Ref: §12.4, Tension 2]

- **Rewrite approach:** The existing system is discarded and replaced with a newly built system. All functionality is reimplemented simultaneously. [Ref: §12.4, Tension 2]
- **Incremental modernization (Strangler Fig) approach:** New functionality is built around the existing system; existing components are gradually replaced one at a time. The old system is "strangled" as its responsibilities migrate. [Ref: §12.4, Tension 2]

#### 4.2.2 Supporting Evidence

- Fowler, "StranglerFigApplication": Incremental modernization is the documented default at scale. The pattern describes gradually creating a new system around the edges of the old, letting it grow over years until the old system is strangled. [Ref: §12.4, Tension 2]
- Brodie and Stonebraker, *Migrating Legacy Systems*, 1995: Incremental migration reduces risk compared to complete replacement by preserving operational continuity and enabling gradual validation of each migrated component. [Ref: §12.4, Tension 2]

#### 4.2.3 Context-Binding Rules

- **CA-2.1** Incremental modernization is the documented default for large-scale legacy systems. [Ref: §12.4, Tension 2]
- **CA-2.2** A complete rewrite MAY be justified when: the existing system is small; the cost of incremental migration exceeds rewrite cost; the system has no operational consumers; or the technology base is obsolete beyond incremental migration viability. [Ref: Converged practice — Brodie & Stonebraker, 1995]
- **CA-2.3** The choice between rewrite and incremental modernization MUST be recorded as a Decision (§35) with risk analysis (§36). [Ref: §35 DEC-1; §36 IMP-1]

#### 4.2.4 References

| Source | Citation | Relevance |
|---|---|---|
| Fowler | "StranglerFigApplication" | Incremental modernization pattern |
| Brodie & Stonebraker | *Migrating Legacy Systems*, 1995 | Migration methodology evidence |

[Ref: §12.4, Tension 2]

---

### 4.3 Monolith-First vs Microservices

#### 4.3.1 Description

This tension addresses whether a new system should begin as a monolithic application (single deployable unit) or as a set of distributed microservices (independently deployable services around business capabilities). [Ref: §12.4, Tension 3]

- **Monolith-first approach:** The system is built as a single deployable unit. Modules are organized internally but share a single process and deployment boundary. [Ref: §12.4, Tension 3]
- **Microservices approach:** The system is decomposed into independently deployable services, each owning a business capability, communicating via lightweight mechanisms. [Ref: §12.4, Tension 3]

#### 4.3.2 Supporting Evidence

- Fowler, "MonolithFirst": Most successful microservice systems began as monoliths that were later decomposed. Starting with microservices risks premature decomposition before domain boundaries are understood. [Ref: §12.4, Tension 3]
- Newman, *Building Microservices*, 2nd ed.: Microservices impose significant operational complexity (deployment, monitoring, distributed tracing, eventual consistency). This overhead is justified when the organizational and scale benefits exceed the costs. [Ref: §12.4, Tension 3]

#### 4.3.3 Context-Binding Rules

- **CA-3.1** Monolith-first is the documented default for new systems where domain boundaries are not yet well understood. [Ref: §12.4, Tension 3; Fowler, "MonolithFirst"]
- **CA-3.2** Microservices MAY be adopted from the outset when: the domain is well-understood; multiple teams require independent deployability; scaling requirements differ radically across components; or organizational structure aligns with service boundaries (Conway's Law). [Ref: Newman, *Building Microservices*; §2 P-3]
- **CA-3.3** Decomposition from monolith to microservices MUST be preceded by Discovery (§25), Analysis (§12), and Impact Analysis (§36). [Ref: §25 DSC-1; §36 IMP-1]
- **CA-3.4** The choice MUST be recorded as a Decision (§35) with context justification and alternative analysis. [Ref: §35 DEC-1]

#### 4.3.4 References

| Source | Citation | Relevance |
|---|---|---|
| Fowler | "MonolithFirst" | Monolith-first evidence |
| Newman | *Building Microservices*, 2nd ed. | Microservices operational analysis |

[Ref: §12.4, Tension 3]

---

### 4.4 Source-Available vs Binary Reverse Engineering

#### 4.4.1 Description

This tension addresses whether reverse engineering is performed with access to source code (static + dynamic analysis on source) or without source access (binary or protocol reverse engineering). [Ref: §30.4]

- **Source-available reverse engineering:** Analysis is performed on available source code, combining static analysis, dynamic analysis, and cross-validation (triangulation). [Ref: §30.4]
- **Binary/protocol reverse engineering:** Analysis is performed on compiled artifacts, network protocols, or interfaces without access to source code. [Ref: §30.4]

#### 4.4.2 Supporting Evidence

- Chikofsky and Cross, 1990: The general reverse engineering activity model (examination, design recovery, restructuring, reengineering) applies regardless of source availability. [Ref: §30.4; §30.1]
- Eilam, *Reversing*, 2005: Binary reverse engineering requires distinct techniques (disassembly, decompilation, runtime instrumentation) and operates under different legal/authorization constraints. [Ref: §30.4]

#### 4.4.3 Context-Binding Rules

- **CA-4.1** The activity model for reverse engineering (Discovery → Recovery → Understanding → Documentation → Planning → Modification → Validation → Knowledge Preservation) is common to both source-available and binary reverse engineering. [Ref: §30.4; §30.2]
- **CA-4.2** Technique selection is context-bound and extension-defined, not mandated by the core standard. [Ref: §30.4; §30.3 REV-6]
- **CA-4.3** Legal and authorization constraints on reverse engineering MUST be confirmed per engagement before any reverse engineering activity begins. [Ref: §30.4]
- **CA-4.4** Binary/protocol reverse engineering contexts SHALL define the specific technique extensions under the Extension Policy (§19). [Ref: §19 EX-2; §30.3 REV-6]
- **CA-4.5** Confidence levels (§26) apply equally to both contexts; facts derived from binary analysis MUST carry the same evidence and provenance requirements as facts from source analysis. [Ref: §26 EVC-1; §28 ECH-1]

#### 4.4.4 References

| Source | Citation | Relevance |
|---|---|---|
| Chikofsky & Cross | "Reverse Engineering and Design Recovery," IEEE Software, 1990 | General activity model |
| Eilam | *Reversing*, 2005 | Binary reverse engineering techniques |

[Ref: §30.4]

## 5. Context-Binding Framework

The following general rules govern how projects select among competing approaches documented in this standard:

- **CB-1** Where the evidence base shows multiple valid approaches, the project MUST document the selected approach, the rejected alternatives, and the context factors that justify the selection. [Ref: PR-12; §35 DEC-1]
- **CB-2** Context-binding factors MUST include: cost-of-change profile, regulatory requirements, team size and distribution, system scale, uncertainty level, reversibility of decisions, and operational continuity requirements. [Ref: Boehm & Turner, 2003; §12.4]
- **CB-3** The selection among competing approaches MUST be recorded as a Decision (§35) with the Decision Structure (§35.2: Decision, Context, Alternatives, Evidence, Impact, Dependencies, Approval, Status, Superseded By). [Ref: §35 DEC-1]
- **CB-4** A selection MAY be revisited when its governing context changes materially; the revised selection MUST supersede the prior Decision (§35 DEC-3). [Ref: §35 DEC-3]
- **CB-5** No project MAY claim a context exemption from competing approach analysis without an explicit Decision (§35) justifying why the tension is not applicable. [Ref: PR-12; §35]

## 6. Completion Criteria

This document is complete when:

- [ ] All four approach tensions (§4.1–§4.4) are documented with Description, Supporting Evidence, Context-Binding Rules, and References. [Ref: §12.4; §30.4]
- [ ] Each tension cites its SDD authority and approved evidence base sources. [Ref: FR-11]
- [ ] The Context-Binding Framework (§5) defines general rules for approach selection. [Ref: PR-12]
- [ ] Every normative rule (CA-1 through CA-4.5, CB-1 through CB-5) is stated and cites its SDD authority. [Ref: PR-7]
