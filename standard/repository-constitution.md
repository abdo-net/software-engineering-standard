# Repository Constitution

> **Authority Class:** Authoritative
> **SDD Authority:** §10, §11, §17, §18, §40
> **Status:** Accepted
> **Version:** 0.4.0
> **Phase:** Phase 2

---

## 1. Repository Purpose

This repository exists to be the permanent, version-controlled residence of the Software Engineering Standard (SES), which SHALL be the authoritative, vendor-independent, technology-independent engineering reference that governs how software engineering work is performed across all future projects of this organization. [Ref: §1.1 Vision Statement] The repository is the only permanent engineering artifact; therefore the standard that governs engineering resides in the repository and depends on nothing transient. [Ref: §1.3 Durability Requirement; PR-4]

The SES exists to counter the documented failure modes of engineering continuity loss: continuing change and decay (P-1), loss of decision rationale (P-2), organizational coupling and divergence (P-3), drift between artifacts (P-4), and tool/vendor volatility (P-5). [Ref: §2 Problem Statement] These failure modes manifest as implementations drifting from contracts, documentation drifting from implementation, and architectural intent being lost over time. [Ref: §2.1 Core Problem]

The repository realizes the following objectives: providing a single authoritative engineering standard (OBJ-1); basing every normative rule on citable evidence (OBJ-2); reconstructing existing proven practice (OBJ-3); remaining valid under total replacement of any vendor, tool, or AI system (OBJ-4); making the repository the permanent engineering memory (OBJ-5); making every engineering claim traceable to evidence (OBJ-6); making conformance objectively verifiable (OBJ-7); making the standard evolvable under governance (OBJ-8); and being readable and executable by both human engineers and automated agents (OBJ-9). [Ref: §3 Objectives]

---

## 2. Authority Hierarchy

The **Normative Standard** region is supreme; all other regions derive their authority from it. [Ref: §10.4 Authority Rule; RA-5] The normative standard region is authoritative over all other regions; in any conflict, the standard governs. [Ref: RA-5 — Standard precedes derivation] The SES is superordinate to every project; projects are users of the standard. [Ref: §1.1 Vision Statement; §1.2 What the Standard Aspires To Be] The standard defines what process properties must hold; the project decides how to realize them in its context. [Ref: §1.2]

Operational documents, templates, and examples MUST derive their authority by citing the standard and MUST NOT introduce new normative rules. [Ref: §10.4 Authority Rule] This architectural decision (RA-5) is driven by PR-10 (controlled evolution) and §1.2 (superordination). [Ref: §10.2 RA-5 rationale]

---

## 3. Repository Regions

The repository SHALL be organized into five architectural regions, each containing a distinct kind of content. [Ref: §10.3 Architectural View (logical); FR-17] These regions are:

### 3.1 NORMATIVE STANDARD (authoritative; governs everything)

This region contains the SDD and its successors — the single source of truth for all engineering rules. [Ref: §10.3] It is the only region that may contain MUST/SHALL rules. [Ref: §10.4 Authority Rule] All other regions derive their content from this region. [Ref: RA-5]

### 3.2 DERIVED OPERATIONAL DOCS (generated/derived from the standard)

This region contains SOPs, Stage Specifications, Checklists, Review Rules, and Validation Rules. [Ref: §10.3] These are produced by transforming one or more authoritative artifacts; they carry no independent truth. [Ref: RA-4] They MUST NOT be hand-edited; they MUST be regenerated from source. [Ref: §11.1 Artifact Authority Model]

### 3.3 REFERENCE MATERIAL (the cited evidence base)

This region contains the supporting reference material that constitutes the approved evidence base for normative rules. [Ref: §10.3] It is supporting, not authoritative in itself; authority resides in the standard region. [Ref: RA-5]

### 3.4 TEMPLATES (derived; instantiate artifacts)

This region contains templates used to instantiate artifacts conforming to the standard. [Ref: §10.3] Templates are derived artifacts and SHALL be produced in Phase 8. [Ref: §24 Future Work — Phase 8]

### 3.5 EXAMPLES (illustrative; non-normative)

This region contains worked examples across domains (backend, frontend, infra, reverse engineering, legacy modernization). [Ref: §10.3] Examples are non-normative and illustrative; they SHALL be produced in Phase 9. [Ref: §24 Future Work — Phase 9]

---

## 4. Document Precedence

On conflict between any two artifacts in the repository, the Normative Standard region governs. [Ref: RA-5 — Standard precedes derivation] The Canonical Engineering Vocabulary (§46) is the authoritative source of terminology; no later document may redefine the terms defined therein. [Ref: §46.3 VOC-1] Appendix B (Glossary) is a derived convenience view of §46 and introduces no independent authority; on conflict, §46 governs. [Ref: §46.3 VOC-3; CON-2 — No duplicate authority]

The architectural decision RA-3 (One fact, one authoritative location) reinforces this: no fact SHALL be authoritative in two places. Cross-references MUST point to the single authoritative artifact. [Ref: RA-3] Where a conflict-resolution rule among principles is needed, PR-1 (evidence) and PR-7 (verifiability) take precedence. [Ref: §7 Conflict-resolution rule among principles]

---

## 5. Modification Rules

### 5.1 Project Modification Prohibition

Projects MUST NOT modify the core standard. [Ref: §17.2 GV-1; CN-7] Projects MAY submit change proposals with evidence (the feedback path). [Ref: GV-1] This governance rule is driven by PR-10 (controlled evolution) and the Mission Statement. [Ref: §17.2 GV-1 rationale]

### 5.2 Change Proposal Requirements

A change to the standard MUST originate as a proposal containing: the problem, the evidence, the proposed change, the impact on existing requirements, and the affected versions. [Ref: §17.2 GV-2] This is consistent with converged RFC process practice. [Ref: §17.2 GV-2 rationale]

### 5.3 Change Approval Process

A change MUST be approved by the designated Standard Authority (STK-1) after Inspection (the most rigorous review form per RV-2). [Ref: §17.2 GV-3; §15.2 RV-2] The change MUST be supported by evidence from the approved evidence base (Appendix A) or be explicitly marked UNSUPPORTED; unevidenced changes MUST NOT be accepted as normative. [Ref: §17.2 GV-4]

### 5.4 Change Documentation

Every accepted change MUST produce: a version increment (§18), a changelog entry, and an ADR recording the decision and its rationale. [Ref: §17.2 GV-5] The standard MUST maintain a single, identifiable current authoritative version; superseded versions are retained for history but are non-governing. [Ref: §17.2 GV-6]

### 5.5 Roles

Roles MUST be defined at minimum as: Standard Authority, Maintainer, Reviewer, Contributor/Project. [Ref: §17.2 GV-7] The detailed RACI is a Phase-7 deliverable. [Ref: §17.2 GV-7; §24 Future Work — Phase 7]

---

## 6. Artifact Ownership

Every artifact SHALL carry, at minimum: a unique identifier, an authority class (§11.1), an owner, a version, a status, and — for derived/generated artifacts — a pointer to the authoritative source(s) from which it is produced. [Ref: §11.2 Mandatory Artifact Metadata] This metadata requirement is driven by PR-5 (provenance) and PR-6 (single source of truth). [Ref: §11.2 rationale]

Every engineering object MUST carry an Owner field, which represents the single accountable owner of that object. [Ref: §43.2 Mandatory Object Fields — Owner; OM-1] The consistency rule CON-3 (No duplicate ownership) reinforces this: each object has exactly one Owner. [Ref: §49.1 CON-3]

The Object Model (§43) generalizes the Artifact metadata (§11.2) into a unified schema where every engineering object is an instance with mandatory fields including Object ID, Object Type, Authority Class, Owner, Lifecycle State, Status, Version, Parent Objects, Child Objects, Incoming Relationships, Outgoing Relationships, Evidence References, Decision References, Repository Location, and Traceability Links. [Ref: §43.2] Every engineering object MUST carry all fifteen fields. [Ref: §43.3 OM-1]

No engineering object MAY exist outside this model. [Ref: §43.3 OM-2] Object Type MUST be a §42.2 entity; Authority Class MUST be from §11.1. [Ref: §43.3 OM-3] Incoming/outgoing relationships MUST be Relationship Model (§44) types. [Ref: §43.3 OM-4] These fields are a superset of, and consistent with, §11.2 artifact metadata. [Ref: §43.3 OM-5]

Generated/Derived objects MUST remain reproducible (RA-4); their fields MUST NOT be hand-forged. [Ref: §43.3 OM-6]

---

## 7. Frozen Areas

SDD v0.4.0 is frozen as the authoritative Phase 1 deliverable. Changes to the standard follow the governance model (§17) and versioning strategy (§18). [Ref: §17 Governance Model; §18 Versioning Strategy] Every release of the standard MUST carry a unique semantic version. [Ref: §18.2 VS-1] Every change MUST be recorded in a changelog that states what changed and why. [Ref: §18.2 VS-2]

The SDD v0.4.0 defines the architecture of the standard; the full normative specification of lifecycle, stages, knowledge, review, validation, and governance are explicitly deferred to later phases. [Ref: §4.4 Phase-1 Document Scope; §12–§17 phase-boundary notes] The concrete repository directory/file structure is deferred to Phase 2. [Ref: §24 Future Work] The SOP, Stage Specifications, Templates, Checklists, Workflows, Examples, and all other repository files are out of scope for Phase 1 and MUST NOT be produced in this phase. [Ref: §4.4]

Violation of the Integrity Rules (§40) renders affected work non-conformant (§16), MUST block state transition (STA-2), and MUST block Repository Readiness (§41). [Ref: §40.2 Enforcement] Integrity Rules MAY be waived only through governance (§17). [Ref: §40.2]

---

## 8. Generated Artifacts Policy

Every artifact the SES recognizes SHALL be classified into exactly one of three authority classes: Authoritative, Derived, or Generated. [Ref: §11.1 Artifact Authority Model] This tri-class model is the structural core that prevents documentation drift. [Ref: §11.1 rationale]

**Authoritative** artifacts are the single source of truth for some fact or decision, hand-authored, and MAY be edited by humans through review and governance. [Ref: §11.1 Authoritative class] **Derived** artifacts are produced by transforming one or more authoritative artifacts and MUST NOT be hand-edited; they MUST be regenerated from source. [Ref: §11.1 Derived class] **Generated** artifacts are mechanically produced from authoritative sources or from the system under engineering and MUST NOT be hand-edited; they MUST be reproducible. [Ref: §11.1 Generated class]

Any derived or generated artifact MUST be reproducible from its authoritative source by a documented, tool-agnostic procedure. [Ref: RA-4 — Derived/generated content is regenerable] A derived artifact that cannot be regenerated has silently become a second source of truth, which is prohibited by PR-6. [Ref: RA-4 rationale]

Traceability links SHOULD be generated artifacts (§11), not hand-maintained, to prevent drift. [Ref: §29.3 TRC-3] This policy extends to the Traceability Graph (§48), which SHOULD be a generated artifact. [Ref: §48.3 TGR-4] Appendix C (Requirements Traceability Index) is a generated artifact and MUST be generated, not hand-maintained. [Ref: §11.3 Traceability Index; PR-6]

The Documentation Model (§38) reinforces this: generated documentation MUST NOT be hand-edited and MUST be reproducible. [Ref: §38.3 DOC-3] The Repository Knowledge Architecture (§31) requires that generated and derived knowledge MUST NOT be hand-edited; they MUST be reproducible from authoritative sources. [Ref: §31.3 RKA-4]

---

*End of Repository Constitution*
