# Repository Rules

> **Authority Class:** Authoritative
> **SDD Authority:** §10, §11, §17, §18, §19, §43, §49
> **Status:** Accepted
> **Version:** 0.4.0
> **Phase:** Phase 2

---

## 1. Naming Conventions

All artifacts in the repository SHALL be expressed in plain-text, structured, version-controllable form, with no dependency on a proprietary format or tool to be read or checked. [Ref: FR-13] This functional requirement traces to OBJ-9 (readable and executable by both human engineers and automated agents) and PR-3 (vendor/tool/language/AI independence). [Ref: FR-13 traces to OBJ-9, PR-3]

File and directory names within the repository MUST use only plain-text characters compatible with common version-control systems and file systems. [Ref: FR-13; NFR-1] The standard MUST be fully usable with only a text editor and version control. [Ref: NFR-1] File names SHOULD be descriptive, use lowercase with hyphens as word separators, and use the `.md` extension for Markdown documents, consistent with the plain-text structured requirement. [Ref: FR-13; Converged practice — docs-as-code]

All artifacts MUST be plain-text and version-controllable. [Ref: CN-8] The repository MUST store the standard as plain-text, structured files (Markdown) in a version-control system. [Ref: RA-1 — The standard is plain text under version control] This is driven by NFR-1 (tool/vendor independence), NFR-7 (durability), and PR-4 (repository as memory). [Ref: RA-1 rationale]

---

## 2. Directory Ownership

Each directory in the repository is an engineering object and therefore MUST have an owner. [Ref: §43.2 Mandatory Object Fields — Owner; OM-1] The Owner field represents the single accountable owner of that object. [Ref: §43.2 Owner field definition] The consistency invariant CON-3 (No duplicate ownership) requires that each object has exactly one Owner. [Ref: §49.1 CON-3]

The Owner relationship type (§44.2) is directed 1:n from Owner to object, with the constraint that exactly one owner must exist per CON-3. [Ref: §44.2 owns relationship; §49.1 CON-3] This applies to all container objects including directories, which are part of the Repository Location field of every engineering object. [Ref: §43.2 Repository Location field]

The repository architecture (§10.3) defines five top-level regions (NORMATIVE STANDARD, DERIVED OPERATIONAL DOCS, REFERENCE MATERIAL, TEMPLATES, EXAMPLES), each of which MUST have a designated owner accountable for its contents. [Ref: §10.3; §43.2]

---

## 3. Immutability Rules

Authoritative artifacts are immutable once accepted. This applies specifically to Architecture Decision Records (ADRs) and other authoritative decision artifacts. [Ref: §11.3 ADR — Authoritative; immutable once accepted (superseded, never edited)] The ADR SHALL be superseded, never edited, once accepted. [Ref: §11.3 ADR classification]

The Knowledge Model reinforces this immutability: decisions MUST be recorded in an immutable, append/supersede format (ADR). An accepted decision MUST NOT be silently edited; it is superseded by a new record. [Ref: §14.3 KN-2] The Decision Model (§35) states: a Decision is immutable once Approved; change occurs only by a new Decision setting Superseded By. [Ref: §35.3 DEC-3]

The Engineering Consistency Rules (§49) provide structural enforcement: the relationship type supersedes (§44.2) is directed 1:1 from new to old, and MUST preserve the superseded object as Historical (RKA-3); it MUST NOT delete it. [Ref: §44.3 REL-4; §31.3 RKA-3]

Repository Knowledge Architecture requires that superseded knowledge MUST be retained as Historical; deprecated knowledge MUST be marked, not deleted. [Ref: §31.3 RKA-3] Updates MUST preserve history; superseded knowledge becomes Historical and MUST NOT be overwritten silently. [Ref: §39.3 EVO-3]

---

## 4. Generated File Protection

Derived and generated artifacts MUST NOT be hand-edited. [Ref: §11.1 Artifact Authority Model — Derived class: MUST NOT be hand-edited; Generated class: MUST NOT be hand-edited] Any derived or generated artifact MUST be reproducible from its authoritative source by a documented, tool-agnostic procedure. [Ref: RA-4] A derived artifact that cannot be regenerated has silently become a second source of truth, which violates PR-6. [Ref: RA-4 rationale]

The Documentation Model (§38) reinforces this: generated documentation MUST NOT be hand-edited and MUST be reproducible. [Ref: §38.3 DOC-3] The Repository Knowledge Architecture (§31) requires that generated and derived knowledge MUST NOT be hand-edited; they MUST be reproducible from authoritative sources. [Ref: §31.3 RKA-4]

Generated/Derived objects MUST remain reproducible (RA-4); their fields MUST NOT be hand-forged. [Ref: §43.3 OM-6] The relationship model requires that derives_from and generated_from relationships MUST point to authoritative sources, and the dependent object MUST NOT be hand-edited. [Ref: §44.3 REL-3]

Traceability links SHOULD be generated artifacts, not hand-maintained, to prevent drift. [Ref: §29.3 TRC-3] The Traceability Graph SHOULD be a generated artifact. [Ref: §48.3 TGR-4] Appendix C (Requirements Traceability Index) is a generated artifact and MUST be generated, not hand-maintained. [Ref: §11.3 Traceability Index; PR-6]

---

## 5. Authority Boundaries

The Normative Standard region is the only region that may contain MUST/SHALL rules. [Ref: §10.4 Authority Rule] Operational documents, templates, and examples MUST derive their authority by citing the standard and MUST NOT introduce new normative rules. [Ref: §10.4] This is driven by PR-6 (single source of truth) and RA-5 (standard precedes derivation). [Ref: §10.4 rationale]

The architectural decision RA-5 establishes that the normative standard region is authoritative over all other regions; in any conflict, the standard governs. [Ref: RA-5] The architectural decision RA-2 (Authority layering) requires the repository to separate kinds of content into distinct regions precisely to prevent mixing authoritative and derived content so that readers cannot tell which governs. [Ref: RA-2 rationale]

Extensions MUST NOT contradict the core; in any conflict, the core governs. [Ref: §19.2 EX-3] An extension MUST NOT weaken a core MUST/SHALL rule; it MAY only add or strengthen. [Ref: §19.2 EX-4] This preserves the authority boundary: only the standard region may weaken or modify core rules, and only through governance (§17). [Ref: §19.2 EX-3; §17]

---

## 6. Version Control Rules

The repository MUST store the standard as plain-text, structured files in a version-control system. [Ref: RA-1] Version control provides history, review, and provenance "for free." [Ref: RA-1 rationale] This satisfies NFR-1 (tool/vendor independence), NFR-7 (durability), and PR-4 (repository as permanent memory). [Ref: RA-1 rationale]

Authoritative engineering knowledge MUST reside in version-controlled repository artifacts, never solely in conversation or tooling. [Ref: PR-4] Engineering work products are kept under version control (AS-2). If this assumption is false, repository-as-memory fails. [Ref: §22 AS-2]

Knowledge MUST reside in the repository (PR-4), never solely in conversation, model memory, or tooling state. [Ref: §14.3 KN-5] The repository is the permanent engineering memory; nothing essential lives only in conversation or tooling. [Ref: OBJ-5; §1.3 Durability Requirement]

Every authoritative artifact class is defined as a version-controlled repository file. [Ref: SC-5] Changes to the standard MUST follow governance and semantic versioning; no silent change is permitted. [Ref: NFR-9] Every release of the standard MUST carry a unique semantic version. [Ref: §18.2 VS-1] Every change MUST be recorded in a changelog that states what changed and why. [Ref: §18.2 VS-2]

---

## 7. Extension Rules

### 7.1 Core vs Extension Distinction

The SES SHALL distinguish a stable core (technology-independent, governs all projects) from extensions (context-specific: language conventions, framework rules, domain specifics). [Ref: §19.2 EX-1] Projects MAY define extensions for their context. [Ref: §19.2 EX-2]

### 7.2 Extension Constraints

An extension MUST NOT contradict the core. In any conflict, the core governs. [Ref: §19.2 EX-3; RA-5; PR-10] An extension MUST NOT weaken a core MUST/SHALL rule; it MAY only add or strengthen. [Ref: §19.2 EX-4] This constraint reflects converged practice: standards profiles may constrain but not relax the base. [Ref: §19.2 EX-4 rationale]

Extensions MUST declare which standard version and which core rules they extend (traceability). [Ref: §19.2 EX-5] Where a context genuinely requires deviating from a core rule, this MUST be raised as a governance change proposal (§17), not implemented as a silent local override. [Ref: §19.2 EX-6; GV-1]

### 7.3 Extension Mechanism

Extensions are separate artifacts that reference the core; they are the sanctioned path by which projects adapt without forking the standard. [Ref: §19.3 Mechanism] This preserves "projects do not modify the standard" (Mission Statement; GV-1) while making the standard usable across every declared domain. [Ref: §19.3; §17; PR-10]

### 7.4 Extension Governance

The SES core MUST NOT contain any rule that names a specific commercial product, programming language, framework, or AI model as a requirement. [Ref: FR-16] Language-specific conventions are an extension point (§19), not part of the core. [Ref: NG-4] The extension policy resolves the tension between the standard being stable and singular (PR-10) yet applicable to diverse contexts (S-2). [Ref: §19.1]

---

*End of Repository Rules*
