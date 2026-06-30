# Engineering Lifecycle Specification

> **Authority Class:** Authoritative
> **SDD Authority:** §12, §25
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 3

## 1. Purpose

This document is the **full normative specification of each lifecycle phase** mandated by §12.1. It defines, for each of the eleven phases of the Engineering Lifecycle: Objectives, Inputs, Activities, Outputs, Evidence Produced, Verification, Tools, Mistakes, and References. [Ref: §12.1]

The SES adopts a lifecycle that is **process-based and outcome-defined**, not method-prescriptive, consistent with ISO/IEC/IEEE 12207:2017. The lifecycle describes *what outcomes and evidence each phase produces*, leaving *how* to the project (PR-12). [Ref: §12.1]

This document is the deliverable of **Phase 3 (Define engineering lifecycle)** per the Development Order. [Ref: §12.1; §24]

## 2. Scope

This document specifies the lifecycle phases from receipt of an unknown system through Understanding, Reverse Engineering / Reconstruction, Analysis, Planning, Implementation, Validation, Documentation, Maintenance, Evolution, and Retirement, plus the Discovery phase that feeds into Understanding. [Ref: §12.2; §25]

The ordering is a **dependency ordering of artifacts**, not a claim that work is performed once, linearly. Iteration is expected and is supported by the evidence base. [Ref: §12.2]

This document SHALL present and context-bind competing approaches per FR-12 and PR-12, not dogmatically choose between them. [Ref: §12.4; FR-12; PR-12]

## 3. Normative Rules

### LC-1 — Phase Definition Completeness
Each phase SHALL define explicit inputs, outputs, evidence produced, and verification criteria. [Ref: §12.3; ISO/IEC/IEEE 12207 process structure]

### LC-2 — Evidence-Backed Conclusions
No phase MAY assert a conclusion that is not backed by evidence from the subject system (PR-5). [Ref: §12.3; Chikofsky & Cross; Feathers (characterization tests)]

### LC-3 — Iterative Understanding
The lifecycle SHALL treat understanding/analysis as iterative, not single-pass. The linear diagram is an artifact-dependency DAG, not a waterfall. Asserting a fixed single-pass sequence is UNSUPPORTED as universal practice. [Ref: §12.3; Demeyer et al., 2002; ISO 12207 non-prescription of sequence]

### LC-4 — Maintenance Categories
Maintenance SHALL recognize the four maintenance categories: corrective, adaptive, perfective, preventive. [Ref: §12.3; ISO/IEC/IEEE 14764:2022; Lientz & Swanson, 1980]

### LC-5 — Retirement as Explicit Phase
Retirement SHALL be an explicit, planned phase, not an implicit event (data archival, consumer notification, deprecation policy). [Ref: §12.3; ISO/IEC/IEEE 12207 Disposal process; RFC 8594 (Sunset header) for API deprecation]

## 4. Lifecycle Frame

The lifecycle SHALL comprise the following phases. The ordering is a dependency ordering of artifacts, not a claim that work is performed once, linearly. [Ref: §12.2]

```
Unknown System
   |
Understanding  ------------------------------> (recover the system as it actually is)
   |
Reverse Engineering / Reconstruction
   |
Analysis (dependencies, execution flow, contracts, gaps)
   |
Planning (design docs, ADRs, risk, sequencing)
   |
Implementation (small, isolated, reviewed, reversible changes)
   |
Validation (static -> unit -> integration -> contract -> regression -> system -> runtime -> review)
   |
Documentation (authoritative + generated; docs-as-code)
   |
Maintenance (corrective / adaptive / perfective / preventive)
   |
Evolution (controlled change under fitness/governance)
   |
Retirement (deliberate disposal, archival, deprecation)
   ^
   |
Discovery (feeds into Understanding) [per §25]
```

Discovery is the phase by which an unknown system becomes an understood system. It is organized into evidence layers; layers are dependency-ordered, not strictly sequential (LC-3). [Ref: §25.2]

## 5. Phase Specifications

---

### 5.1 Understanding

#### 5.1.1 Objectives
Recover the system as it actually is. [Ref: §12.2] Produce a verified, evidence-based comprehension of the subject system's structure, behavior, dependencies, contracts, and operational characteristics sufficient to support downstream Analysis and Planning. [Ref: §12.2; §25.1]

#### 5.1.2 Inputs
The SDD does not specify explicit inputs for this phase. [Ref: §12.2]

#### 5.1.3 Activities
- Examine the subject system through the Discovery operations defined in §25.
- Produce observed facts, verified facts, and synthesized engineering knowledge per the Knowledge Model (§14) and Repository Knowledge Architecture (§31).
- Record all findings with provenance (PR-5) and confidence levels (§26).
- Apply triangulation (KN-6): corroborate facts by more than one source class (static, dynamic, human) before recording as authoritative. [Ref: §14.3 KN-6]
- Mark hypotheses as hypotheses (KN-3); they MUST NOT be recorded as facts until verified. [Ref: §14.3 KN-3]

#### 5.1.4 Outputs
- Observed Facts: raw facts captured during discovery, pre-verification. [Ref: §31.2]
- Verified Facts: facts that passed the Evidence Chain (§28). [Ref: §31.2]
- Engineering Knowledge: synthesized understanding from verified facts. [Ref: §31.2]
- Discovery documentation per the Documentation Model (§38), classified as Observed or Verified. [Ref: §38.2]

#### 5.1.5 Evidence Produced
Every recorded fact MUST carry provenance — a reference to the source evidence (file, trace, schema, commit) from which it was derived (KN-1). [Ref: §14.3 KN-1] A fact without provenance is non-authoritative.

Every engineering fact MUST carry a confidence level (A–E) per the Evidence Confidence Model (§26). [Ref: §26.2; EVC-1]

#### 5.1.6 Verification
Verification that Understanding is complete SHALL be against the "Discovery Complete" and "Knowledge Complete" completion states defined in §27. [Ref: §27.2; DSC-5] Discovery is complete only when the §27 criteria are objectively met. [Ref: §25.4 DSC-5]

#### 5.1.7 Tools
The SDD does not specify tools for this phase. Tool selection is out of core scope (CN-1) and MAY be an extension (§19). [Ref: §30.3 REV-6; CN-1; §19]

#### 5.1.8 Mistakes
- Recording assumptions as facts (KN-1 + KN-3 + KN-6 is the structural defense against this). [Ref: §14.4]
- Treating a hypothesis (confidence Level E) as authoritative (EVC-3). [Ref: §26.4 EVC-3]
- Skipping the Evidence Chain (§28) when promoting observations to facts (ECH-1). [Ref: §28.3 ECH-1]
- Failing to record disagreements between static and dynamic analysis (DSC-3). [Ref: §25.4 DSC-3]

#### 5.1.9 References
- §14 Knowledge Model
- §25 Engineering Discovery Model
- §26 Evidence Confidence Model
- §27 Engineering Completion Criteria
- §28 Engineering Evidence Chain
- §31 Repository Knowledge Architecture
- §38 Engineering Documentation Model
- Chikofsky & Cross, 1990; Demeyer et al., 2002; Feathers, 2004

---

### 5.2 Reverse Engineering / Reconstruction

#### 5.2.1 Objectives
Produce higher-level abstractions from lower-level artifacts, transforming raw system examination into structured, documented understanding. [Ref: §30.2] Recovery produces higher-level abstractions from lower-level artifacts, each evidenced (§26) and provenanced (§28). [Ref: §30.3 REV-2]

#### 5.2.2 Inputs
- Observed Facts from the Understanding phase (§5.1). [Ref: §31.2]
- Raw artifacts from the subject system (source code, configuration, database schemas, build files). [Ref: §30.2]

#### 5.2.3 Activities
- Reverse engineering (examination only) — examination of the subject system without alteration (REV-1). [Ref: §30.3 REV-1]
- Design recovery — producing higher-level abstractions from lower-level artifacts (REV-2). [Ref: §30.3 REV-2]
- Restructuring — transforming the system from one representation to another at the same abstraction level. [Ref: §30.1]
- Architecture recovery — synthesizing architectural views from recovered facts. [Ref: §25.2 Synthesis]
- Knowledge extraction — transforming verified facts into Engineering Knowledge. [Ref: §25.2 Synthesis; §31.2]
- Evidence collection — preserving all supporting evidence with provenance and confidence. [Ref: §25.2 Synthesis]

#### 5.2.4 Outputs
- Recovered design abstractions (architectural views, module hierarchies, execution flow models). [Ref: §30.2]
- Engineering Knowledge (synthesized understanding from verified facts). [Ref: §31.2]
- Architecture Decision inputs (discovered constraints and rationales that inform later decisions). [Ref: §35.2]

#### 5.2.5 Evidence Produced
Each recovered abstraction MUST be evidenced (§26) and provenanced (§28). [Ref: §30.3 REV-2] Recovery outputs are Verified Facts or Engineering Knowledge per the Knowledge Model (§14, §31). [Ref: §31.2]

#### 5.2.6 Verification
Recovery outputs MUST pass through the Evidence Chain (§28): Unknown Observation -> Evidence -> Verification -> Engineering Fact. [Ref: §28.2; ECH-1] Verification methods: Inspection, Analysis, Demonstration, or Test per §16.2. [Ref: §16.2]

#### 5.2.7 Tools
The SDD does not specify tools for this phase. Tool selection is out of core scope (CN-1) and MAY be an extension (§19). [Ref: §30.3 REV-6; CN-1; §19]

#### 5.2.8 Mistakes
- Altering the subject system during reverse engineering (REV-1: reverse engineering up to and including Recovery is examination only; it MUST NOT alter the subject system). [Ref: §30.3 REV-1]
- Recording recovered abstractions without evidence or provenance (REV-2). [Ref: §30.3 REV-2]
- Promoting hypotheses (confidence Level E) to facts without verification (ECH-1, EVC-3, KN-3). [Ref: §28.3 ECH-1; §26.4 EVC-3; §14.3 KN-3]

#### 5.2.9 References
- §25 Engineering Discovery Model
- §26 Evidence Confidence Model
- §28 Engineering Evidence Chain
- §30 Reverse Engineering Architecture
- §31 Repository Knowledge Architecture
- §35 Engineering Decision Model
- Chikofsky & Cross, 1990; Demeyer et al., 2002; Feathers, 2004

---

### 5.3 Analysis

#### 5.3.1 Objectives
Examine the system to produce engineering conclusions covering: dependencies, execution flow, contracts, and gaps. [Ref: §12.2] Analysis feeds the Engineering Impact Analysis Model (§36). [Ref: §34.2]

#### 5.3.2 Inputs
- Verified Facts and Engineering Knowledge from Understanding (§5.1) and Reverse Engineering (§5.2). [Ref: §31.2]
- Recovered architectural abstractions from Reverse Engineering / Reconstruction (§5.2). [Ref: §30.2]

#### 5.3.3 Activities
- Dependency analysis — discovering and mapping dependencies between components, modules, and external systems. [Ref: §12.2; §25.2 Structure Layer]
- Execution flow recovery — tracing the flow of control and data through the system. [Ref: §12.2; §25.2 Behavior Layer]
- Contract analysis — identifying and documenting agreed interfaces and semantics across boundaries. [Ref: §12.2; §11.3]
- Gap analysis — identifying discrepancies between the system-as-documented (if any) and the system-as-recovered. [Ref: §37.2 (System vs Documentation comparison)]
- Cross-validation (triangulation) of analysis findings between static and dynamic sources. [Ref: §25.4 DSC-3]
- Security, authentication, and authorization discovery. [Ref: §25.2 Security Layer]

#### 5.3.4 Outputs
- Dependency map (discovered and recorded dependencies). [Ref: §12.2; §36.2]
- Execution flow model. [Ref: §12.2; §25.2 Behavior Layer]
- Contract inventory (APIs, database schemas, configuration contracts). [Ref: §11.3]
- Gap findings (divergences between system and documentation, or between expected and actual behavior). [Ref: §37.2]
- Impact analysis inputs for downstream Planning (§36.2). [Ref: §36.2]

#### 5.3.5 Evidence Produced
All analysis outputs MUST carry provenance (PR-5) and confidence levels (§26). [Ref: §26.2] Every dependency MUST be discovered and recorded (INT-3). [Ref: §40.1 INT-3] Every API MUST have a contract (INT-4). [Ref: §40.1 INT-4] Every database object MUST be documented (INT-5). [Ref: §40.1 INT-5] Every configuration MUST be documented (INT-6). [Ref: §40.1 INT-6]

#### 5.3.6 Verification
Analysis outputs MUST be verified against the Evidence Chain (§28). Comparison results MUST be assigned a confidence level (§26); Runtime-vs-Source disagreements follow EVC-6. [Ref: §37.3 CPM-2] Divergences MUST be recorded as findings and MAY raise Decisions (§35) or Risks (§21); they MUST NOT be silently reconciled. [Ref: §37.3 CPM-3]

#### 5.3.7 Tools
The SDD does not specify tools for this phase. Tool selection is out of core scope (CN-1) and MAY be an extension (§19). [Ref: §30.3 REV-6; CN-1; §19]

#### 5.3.8 Mistakes
- Asserting analysis conclusions without evidence from the subject system (LC-2). [Ref: §12.3 LC-2]
- Silently reconciling divergences between static and dynamic analysis instead of recording them as findings (CPM-3, DSC-3). [Ref: §37.3 CPM-3; §25.4 DSC-3]
- Recording gaps as facts rather than findings (KN-3). [Ref: §14.3 KN-3]
- Proceeding to Planning without verified analysis outputs (REV-3: Understanding MUST precede Planning). [Ref: §30.3 REV-3]

#### 5.3.9 References
- §12.2 (Analysis phase in lifecycle frame)
- §25 Engineering Discovery Model
- §26 Evidence Confidence Model
- §28 Engineering Evidence Chain
- §35 Engineering Decision Model
- §36 Engineering Impact Analysis Model
- §37 Engineering Comparison Model
- §40 Engineering Integrity Rules

---

### 5.4 Planning

#### 5.4.1 Objectives
Produce design documents, Architecture Decision Records (ADRs), risk assessments, and sequencing plans before any modification. [Ref: §12.2] Planning produces decisions/plans before change. [Ref: §46.2 Planning]

#### 5.4.2 Inputs
- Verified analysis outputs from Analysis (§5.3): dependency maps, execution flow models, contract inventory, gap findings. [Ref: §5.3]
- Engineering Knowledge from Understanding and Reverse Engineering phases. [Ref: §31.2]
- Active Mission authorizing the planning work (§32). [Ref: §32.1 MIS-1]

#### 5.4.3 Activities
- Produce design documents specifying the intended changes and their rationale.
- Author Architecture Decision Records (ADRs) per §11.3 and §35: record Decision, Decision Context, Alternatives, Evidence, Impact, Dependencies, Approval, Status, and Superseded By. [Ref: §35.2; §11.3]
- Perform risk assessment per §21: identify likelihood, impact, and mitigation for each risk. [Ref: §21]
- Define sequencing: the order in which changes will be implemented. [Ref: §12.2]
- Perform impact analysis spanning: Affected Components, Dependencies, Execution Flow, Database, API, Security, Tests, Documentation, Deployment, Validation (§36.2). [Ref: §36.2 IMP-1]
- Obtain Approval for Decisions per the Governance Model (§17). [Ref: §35.2; §17.2 GV-3]

#### 5.4.4 Outputs
- Design documents (classified per §38.2 Documentation Categories). [Ref: §38.2]
- Architecture Decision Records (ADRs) — authoritative, immutable once accepted (§11.3). [Ref: §11.3; §35.2]
- Risk register (per §21). [Ref: §21]
- Sequencing plan.
- Impact analysis record (per §36.3 IMP-3). [Ref: §36.3 IMP-3]

#### 5.4.5 Evidence Produced
Each Decision MUST cite the Evidence (§26/§28) and the Impact Analysis (§36) that justify it (DEC-2). [Ref: §35.3 DEC-2] Impact analysis findings MUST be recorded as evidence and MUST feed the authorizing Decision (IMP-3). [Ref: §36.3 IMP-3]

#### 5.4.6 Verification
- Design documents and ADRs MUST pass Review (§15) before becoming effective (RV-1). [Ref: §15.2 RV-1]
- ADRs MUST undergo Inspection (RV-2) because they are authoritative artifacts governing architecture. [Ref: §15.2 RV-2]
- Impact analysis MUST be verified against the dependency view (§5.3) and traceability (§29). [Ref: §36.3 IMP-2]
- Every Decision MUST be recorded with all nine fields (§35.2) per DEC-1. [Ref: §35.3 DEC-1]

#### 5.4.7 Tools
The SDD does not specify tools for this phase. [Ref: §12]

#### 5.4.8 Mistakes
- Proceeding to Implementation without approved Decisions (REV-3: Planning MUST precede Modification; DEC-4: every Implementation MUST trace back to exactly one engineering Decision). [Ref: §30.3 REV-3; §35.3 DEC-4]
- Authoring ADRs without completing impact analysis (DEC-2; IMP-3). [Ref: §35.3 DEC-2; §36.3 IMP-3]
- Silently editing an accepted ADR instead of superseding it (KN-2: Decisions MUST be recorded in an immutable, append/supersede format). [Ref: §14.3 KN-2]
- Planning without an active Mission (MIS-1). [Ref: §32.3 MIS-1]

#### 5.4.9 References
- §11.3 ADR as Special Artifact Type
- §12.2 (Planning phase in lifecycle frame)
- §15 Review Model
- §17 Governance Model
- §21 Risks
- §29 Engineering Traceability Expansion
- §32 Engineering Mission Model
- §35 Engineering Decision Model
- §36 Engineering Impact Analysis Model
- §38 Engineering Documentation Model

---

### 5.5 Implementation

#### 5.5.1 Objectives
Realize approved decisions through small, isolated, reviewed, reversible changes. [Ref: §12.2; §46.2 Implementation]

#### 5.5.2 Inputs
- Approved Decisions (ADRs) from Planning (§5.4). [Ref: §35.3 DEC-4]
- Active Mission authorizing implementation (§32). [Ref: §32.1 MIS-1; MIS-3]
- Impact analysis record (§36). [Ref: §36.3 IMP-3]
- Design documents from Planning (§5.4). [Ref: §5.4]

#### 5.5.3 Activities
- Execute changes that are small, isolated, reviewed, and reversible. [Ref: §12.2]
- Every Implementation MUST trace back to exactly one engineering Decision (DEC-4). [Ref: §35.3 DEC-4]
- Every Implementation MUST begin with an impact analysis spanning the §36.2 dimensions (IMP-1). [Ref: §36.3 IMP-1]
- Changes MUST follow the implementation discipline of the lifecycle and the Validation Model (§16). [Ref: §30.3 REV-4]
- Engineering activity MUST NOT exceed the Mission Scope or violate its Constraints; deviations REQUIRE a new or amended Mission (MIS-4). [Ref: §32.3 MIS-4]

#### 5.5.4 Outputs
- Modified subject system (code, configuration, schema, or other artifacts).
- Implementation records traceable to authorizing Decisions (DEC-4). [Ref: §35.3 DEC-4]
- Validation inputs (the changes to be validated). [Ref: §16]

#### 5.5.5 Evidence Produced
Implementation outputs MUST carry provenance (§28) linking each change to its authorizing Decision. [Ref: §28.2; §35.3 DEC-4] Every produced artifact MUST trace to the Mission that authorized it (MIS-6). [Ref: §32.3 MIS-6]

#### 5.5.6 Verification
- Implementation MUST be reviewed per §15 (RV-1: every authoritative artifact MUST pass at least one review). [Ref: §15.2 RV-1]
- Implementation MUST pass through Validation (§16) before being considered complete. [Ref: §30.3 REV-4]
- Code review SHOULD be performed by someone other than the sole author where independence adds value (RV-4). [Ref: §15.2 RV-4]

#### 5.5.7 Tools
The SDD does not specify tools for this phase. [Ref: §12]

#### 5.5.8 Mistakes
- Implementing without an approved Decision (DEC-4). [Ref: §35.3 DEC-4]
- Implementing without completing impact analysis (IMP-1). [Ref: §36.3 IMP-1]
- Exceeding Mission Scope or violating Mission Constraints (MIS-4). [Ref: §32.3 MIS-4]
- Large, un-isolated, or irreversible changes (contrary to §12.2). [Ref: §12.2]
- Merging implementation and validation responsibilities (PR-8: distinct engineering responsibilities MUST NOT be merged). [Ref: §7 PR-8]

#### 5.5.9 References
- §12.2 (Implementation phase in lifecycle frame)
- §15 Review Model
- §16 Validation Model
- §30 Reverse Engineering Architecture
- §32 Engineering Mission Model
- §35 Engineering Decision Model
- §36 Engineering Impact Analysis Model

---

### 5.6 Validation

#### 5.6.1 Objectives
Verify that implemented changes conform to specification and are fit for intended use, through a fast-feedback-first ordering of verification activities. [Ref: §12.2; §16.3]

#### 5.6.2 Inputs
- Implemented changes from Implementation (§5.5). [Ref: §5.5]
- Authorizing Decisions (ADRs) defining the intended behavior. [Ref: §35.3 DEC-4]
- Contracts and invariants that MUST remain true (§11.3). [Ref: §11.3]

#### 5.6.3 Activities
Execute verification activities in the following order (fast-feedback-first): static analysis -> unit -> integration -> contract -> regression -> system/E2E -> non-functional (performance/security/resilience) -> runtime verification (canary + observability) -> review (in parallel). [Ref: §16.3]

Validation is a responsibility distinct from implementation/execution (PR-8). [Ref: §16.4 VL-5]

#### 5.6.4 Outputs
- Validation verdicts (pass/fail) for each verification layer. [Ref: §16.4 VL-1]
- Recorded validation evidence that is reproducible (VL-3). [Ref: §16.4 VL-3]
- Conformance assertion: a recorded, evidenced statement that the change satisfies applicable requirements at a stated standard version (§16.5). [Ref: §16.5]

#### 5.6.5 Evidence Produced
A conformance verdict MUST cite the evidence on which it rests (PR-5). [Ref: §16.4 VL-4] Validation evidence MUST be recorded and reproducible (VL-3). [Ref: §16.4 VL-3] Review outcomes (findings, disposition) MUST be recorded as evidence (RV-5). [Ref: §15.2 RV-5]

#### 5.6.6 Verification
- Conformance MUST be expressed as objective pass/fail against stated criteria, never as subjective judgment (VL-1). [Ref: §16.4 VL-1]
- Each requirement class MUST have a defined verification method (VL-2). [Ref: §16.4 VL-2]
- A completion state is reached only when its exit criteria are verified by a method in §16.2 (CMP-2). [Ref: §27.3 CMP-2]
- Validation MUST be a responsibility distinct from implementation/execution (VL-5). [Ref: §16.4 VL-5]

#### 5.6.7 Tools
The SDD does not specify tools for this phase. [Ref: §12; §16]

#### 5.6.8 Mistakes
- Skipping validation layers (contrary to §16.3 ordering). [Ref: §16.3]
- Merging validation and implementation responsibilities (VL-5; PR-8). [Ref: §16.4 VL-5]
- Asserting conformance without cited evidence (VL-4). [Ref: §16.4 VL-4]
- Subjective conformance judgment instead of objective pass/fail (VL-1). [Ref: §16.4 VL-1]
- Treating the validation ordering as mandatory rather than converged practice (§16.3 honesty marker). [Ref: §16.3]

#### 5.6.9 References
- §12.2 (Validation phase in lifecycle frame)
- §15 Review Model
- §16 Validation Model
- §27 Engineering Completion Criteria

---

### 5.7 Documentation

#### 5.7.1 Objectives
Produce authoritative and generated documentation per the docs-as-code principle. [Ref: §12.2] Documentation is categorized, non-mixed content aligned to the Artifact Authority Model (§11) and Repository Knowledge classes (§31). [Ref: §38.1]

#### 5.7.2 Inputs
- Engineering Knowledge from prior phases (§14, §31). [Ref: §31.2]
- Validated implementation outputs from Validation (§5.6). [Ref: §5.6]
- Authoritative artifacts: ADRs, contract specifications, invariant registers (§11.3). [Ref: §11.3]

#### 5.7.3 Activities
- Author or generate documentation units, each classified as exactly one of: Observed, Verified, Planned, Implemented, Validated, Historical, Deprecated, Generated, or Authoritative (§38.2). [Ref: §38.2]
- Ensure each documentation unit declares its category (§38.2) and its authority class (§11.2) (DOC-2). [Ref: §38.3 DOC-2]
- Generated documentation MUST NOT be hand-edited and MUST be reproducible (DOC-3). [Ref: §38.3 DOC-3]
- Observed/Planned documentation MUST NOT be presented as Verified/Validated without passing the Evidence Chain (§28) / Validation (§16) (DOC-4). [Ref: §38.3 DOC-4]
- Deprecated/Historical documentation MUST be retained and marked, not deleted (DOC-5). [Ref: §38.3 DOC-5]

#### 5.7.4 Outputs
- Documentation units per §38.2 categories.
- Authoritative documentation (hand-authored, single source of truth). [Ref: §11.1]
- Generated/derived documentation (reproducible from authoritative sources). [Ref: §11.1; RA-4]

#### 5.7.5 Evidence Produced
Documentation MUST NOT mix the §38.2 categories within one authoritative unit (DOC-1). [Ref: §38.3 DOC-1] Each unit's category and authority class are recorded as metadata. [Ref: §38.3 DOC-2]

#### 5.7.6 Verification
- Documentation MUST be reviewed per §15 (RV-1). [Ref: §15.2 RV-1]
- Generated documentation MUST be verified as reproducible from its authoritative source (RA-4). [Ref: §10.2 RA-4]
- "Documentation Complete" completion state (§27.2) MUST be met. [Ref: §27.2]

#### 5.7.7 Tools
The SDD does not specify tools for this phase. [Ref: §12; §38]

#### 5.7.8 Mistakes
- Mixing documentation categories within one authoritative unit (DOC-1). [Ref: §38.3 DOC-1]
- Presenting unverified documentation as verified (DOC-4). [Ref: §38.3 DOC-4]
- Deleting deprecated or historical documentation instead of retaining and marking it (DOC-5). [Ref: §38.3 DOC-5]
- Hand-editing generated documentation (DOC-3; PR-6). [Ref: §38.3 DOC-3; §7 PR-6]
- Drift between documentation and implementation (P-4). [Ref: §2.2 P-4]

#### 5.7.9 References
- §11 Artifact Architecture
- §12.2 (Documentation phase in lifecycle frame)
- §14 Knowledge Model
- §25 Engineering Discovery Model
- §27 Engineering Completion Criteria
- §31 Repository Knowledge Architecture
- §38 Engineering Documentation Model

---

### 5.8 Maintenance

#### 5.8.1 Objectives
Perform corrective, adaptive, perfective, and preventive maintenance on the system. [Ref: §12.2; LC-4]

#### 5.8.2 Inputs
- The maintained system (code, configuration, documentation, contracts).
- Maintenance request categorization (corrective / adaptive / perfective / preventive).
- Engineering Knowledge from prior phases (§31). [Ref: §31.2]

#### 5.8.3 Activities
Maintenance SHALL recognize the four maintenance categories per LC-4 and ISO/IEC/IEEE 14764:2022: [Ref: §12.3 LC-4]
- **Corrective maintenance**: correcting defects.
- **Adaptive maintenance**: adapting to changes in the environment.
- **Perfective maintenance**: improving performance or maintainability.
- **Preventive maintenance**: preventing future problems.

All maintenance activities MUST follow the same lifecycle discipline as initial implementation: Understanding -> Planning -> Implementation -> Validation -> Documentation. [Ref: §12.2; LC-3]

#### 5.8.4 Outputs
- Modified system artifacts.
- Updated documentation per §38. [Ref: §38]
- Updated Knowledge records per §31. [Ref: §31]
- Maintenance records with provenance and confidence. [Ref: §26; §28]

#### 5.8.5 Evidence Produced
All maintenance outputs MUST carry provenance (§28) and confidence (§26). Changes to contracts and invariants MUST pass through governance + versioning (§17-§18) (KN-4). [Ref: §14.3 KN-4] Every produced artifact MUST trace to the Mission that authorized it (MIS-6). [Ref: §32.3 MIS-6]

#### 5.8.6 Verification
- Maintenance changes MUST be validated per §16. [Ref: §16]
- Maintenance outputs MUST be reviewed per §15 (RV-1). [Ref: §15.2 RV-1]
- Impact analysis MUST be performed for maintenance changes per §36 (IMP-1). [Ref: §36.3 IMP-1]

#### 5.8.7 Tools
The SDD does not specify tools for this phase. [Ref: §12]

#### 5.8.8 Mistakes
- Performing maintenance without categorizing it (corrective/adaptive/perfective/preventive) per LC-4. [Ref: §12.3 LC-4]
- Skipping Planning or Validation for maintenance changes (REV-3, REV-4). [Ref: §30.3 REV-3; REV-4]
- Failing to update documentation after maintenance changes (DOC-1 through DOC-5; P-4). [Ref: §38.3]
- Modifying contracts or invariants without governance (KN-4). [Ref: §14.3 KN-4]

#### 5.8.9 References
- §12.2 (Maintenance phase in lifecycle frame)
- §12.3 LC-4
- §14 Knowledge Model
- §15 Review Model
- §16 Validation Model
- §17 Governance Model
- §35 Engineering Decision Model
- §36 Engineering Impact Analysis Model
- §38 Engineering Documentation Model
- ISO/IEC/IEEE 14764:2022; Lientz & Swanson, 1980

---

### 5.9 Evolution

#### 5.9.1 Objectives
Perform controlled change under fitness/governance. Evolution is the disciplined process of changing the system while maintaining conformance to the standard and preserving engineering continuity. [Ref: §12.2]

#### 5.9.2 Inputs
- Current system state and its authoritative documentation. [Ref: §31]
- Change proposals containing: the problem, the evidence, the proposed change, the impact on existing requirements, and the affected versions (GV-2). [Ref: §17.2 GV-2]
- Governance decisions authorizing the evolution (§17). [Ref: §17]

#### 5.9.3 Activities
- Submit change proposals per GV-2. [Ref: §17.2 GV-2]
- Obtain approval from the designated Standard Authority after Inspection (GV-3). [Ref: §17.2 GV-3]
- Ensure changes are supported by evidence from the approved evidence base or explicitly marked UNSUPPORTED (GV-4). [Ref: §17.2 GV-4]
- Produce version increment, changelog entry, and ADR for every accepted change (GV-5). [Ref: §17.2 GV-5]
- Maintain a single identifiable current authoritative version (GV-6). [Ref: §17.2 GV-6]
- The standard MUST change only through governance and only on verified evidence; projects MUST NOT mutate the standard (PR-10). [Ref: §7 PR-10]

#### 5.9.4 Outputs
- Modified system (evolved state).
- Version increment (§18). [Ref: §18]
- Changelog entry (VS-2). [Ref: §18.2 VS-2]
- ADR recording the evolution decision and its rationale (GV-5). [Ref: §17.2 GV-5]
- Updated traceability links (§29). [Ref: §29]

#### 5.9.5 Evidence Produced
Every accepted change MUST produce a version increment, a changelog entry, and an ADR recording the decision and its rationale (GV-5). [Ref: §17.2 GV-5] Changes MUST be supported by evidence or marked UNSUPPORTED (GV-4). [Ref: §17.2 GV-4]

#### 5.9.6 Verification
- Changes MUST be approved by the Standard Authority after Inspection (GV-3). [Ref: §17.2 GV-3]
- Version increments MUST follow Semantic Versioning (§18). [Ref: §18]
- A change's impact on existing requirements MUST be assessed. [Ref: §17.2 GV-2]
- Traceability MUST be updated per §29. [Ref: §29]

#### 5.9.7 Tools
The SDD does not specify tools for this phase. [Ref: §12]

#### 5.9.8 Mistakes
- Mutating the standard without governance (GV-1: Projects MUST NOT modify the core standard). [Ref: §17.2 GV-1]
- Accepting changes without evidence or UNSUPPORTED marking (GV-4). [Ref: §17.2 GV-4]
- Releasing backward-incompatible changes as MINOR or PATCH (VS-5). [Ref: §18.2 VS-5]
- Failing to produce version increment, changelog, or ADR (GV-5). [Ref: §17.2 GV-5]
- Deleting deprecated knowledge instead of marking it Historical (RKA-3). [Ref: §31.3 RKA-3]

#### 5.9.9 References
- §12.2 (Evolution phase in lifecycle frame)
- §17 Governance Model
- §18 Versioning Strategy
- §29 Engineering Traceability Expansion
- §31 Repository Knowledge Architecture
- §35 Engineering Decision Model

---

### 5.10 Retirement

#### 5.10.1 Objectives
Perform deliberate disposal, archival, and deprecation of the system. Retirement SHALL be an explicit, planned phase, not an implicit event. [Ref: §12.2; LC-5]

#### 5.10.2 Inputs
- The system to be retired.
- Deprecation policy (per LC-5, referencing RFC 8594 for API deprecation). [Ref: §12.3 LC-5]
- Consumer notification list.
- Data archival requirements.

#### 5.10.3 Activities
- Data archival: preserve required data per organizational and regulatory requirements.
- Consumer notification: notify all consumers of the system's retirement. [Ref: §12.3 LC-5]
- Deprecation: apply deprecation policy (RFC 8594 Sunset header for APIs). [Ref: §12.3 LC-5]
- Dispose of the system in a planned manner per ISO/IEC/IEEE 12207 Disposal process. [Ref: §12.3 LC-5]
- Mark relevant knowledge as Deprecated (not deleted) per RKA-3. [Ref: §31.3 RKA-3]
- Record retirement decision with rationale per §35. [Ref: §35]

#### 5.10.4 Outputs
- Archived data.
- Retirement record (authoritative artifact per §11.3). [Ref: §11.3]
- Deprecated system artifacts (marked, not deleted). [Ref: §31.2 Deprecated Knowledge; RKA-3]
- Updated knowledge classification: Operational Knowledge becomes Historical Knowledge or Deprecated Knowledge per §31.2. [Ref: §31.2]

#### 5.10.5 Evidence Produced
Retirement activities MUST be evidenced and recorded with provenance (§28). The retirement decision MUST be recorded as an engineering Decision per §35. Deprecated knowledge MUST be retained and marked, not deleted (RKA-3; DOC-5). [Ref: §31.3 RKA-3; §38.3 DOC-5]

#### 5.10.6 Verification
- Retirement MUST be verified against the "Retirement" or "ARCHIVED" completion state per §27.2 and §33.2. [Ref: §27.2; §33.2]
- Deprecation signaling MUST conform to RFC 8594 where applicable. [Ref: §12.3 LC-5]
- Disposal MUST conform to ISO/IEC/IEEE 12207 Disposal process. [Ref: §12.3 LC-5]

#### 5.10.7 Tools
The SDD does not specify tools for this phase. [Ref: §12]

#### 5.10.8 Mistakes
- Treating retirement as an implicit event rather than an explicit, planned phase (LC-5). [Ref: §12.3 LC-5]
- Deleting deprecated knowledge instead of retaining and marking it (RKA-3; DOC-5). [Ref: §31.3 RKA-3; §38.3 DOC-5]
- Failing to notify consumers (LC-5). [Ref: §12.3 LC-5]
- Failing to archive required data (LC-5). [Ref: §12.3 LC-5]

#### 5.10.9 References
- §12.2 (Retirement phase in lifecycle frame)
- §12.3 LC-5
- §27 Engineering Completion Criteria
- §31 Repository Knowledge Architecture
- §33 Engineering State Model
- §35 Engineering Decision Model
- §38 Engineering Documentation Model
- ISO/IEC/IEEE 12207 Disposal process
- RFC 8594

---

### 5.11 Discovery

#### 5.11.1 Objectives
Transform an unknown system into an understood system through a goal-directed, iterative, evidence-producing process. Discovery feeds into Understanding (§5.1). [Ref: §25.1; §25.2] Full comprehension is not the objective; sufficiency for the mission is. [Ref: §25.4 DSC-4]

#### 5.11.2 Inputs
- Unknown system (source code, binaries, configuration, documentation, runtime environment). [Ref: §25.2]
- Active Mission defining the discovery scope and sufficiency criteria (§32). [Ref: §32.1 MIS-1]

#### 5.11.3 Activities
Discovery is organized into evidence layers; layers are dependency-ordered, not strictly sequential (LC-3): [Ref: §25.2]

- **Inventory Layer**: Asset, Repository, Technology, Build-System, Runtime-Environment detection.
- **Structure Layer**: Dependency, Module, API, Database, Configuration discovery.
- **Security Layer**: Security, Authentication, Authorization discovery.
- **Behavior Layer**: Event, Workflow, Execution-Flow Recovery, Runtime Observation.
- **Analysis Methods**: Static Analysis, Dynamic Analysis, Cross-Validation (triangulation).
- **Synthesis**: Architecture Recovery, Knowledge Extraction, Evidence Collection.

Discovery SHALL account for all 25 mandated activities listed in §25.3 (specified in detail in §4 of the Discovery Specification document). [Ref: §25.3]

#### 5.11.4 Outputs
- Documentation of discovered facts (classified per §38.2). [Ref: §25.2 Output; §38.2]
- Verification evidence. [Ref: §25.2 Output]
- Discovery Complete status (per §27). [Ref: §25.2 Output; §25.4 DSC-5]

#### 5.11.5 Evidence Produced
Every discovery output MUST carry provenance (KN-1) and a confidence level (§26). [Ref: §25.4 DSC-2] Discovery MUST combine static and dynamic analysis and cross-validate (triangulate); disagreements MUST be recorded, not silently resolved (DSC-3). [Ref: §25.4 DSC-3] No discovery conclusion MAY assert confidence exceeding its evidence (DSC-6). [Ref: §25.4 DSC-6]

#### 5.11.6 Verification
Discovery is complete only when the "Discovery Complete" criteria (§27) are objectively met (DSC-5). [Ref: §25.4 DSC-5; §27] Every discovery output MUST carry provenance and confidence for verification (DSC-2). [Ref: §25.4 DSC-2]

#### 5.11.7 Tools
The SDD does not specify tools for this phase. Tool selection is out of core scope (CN-1) and MAY be an extension (§19). [Ref: §30.3 REV-6; CN-1; §19]

#### 5.11.8 Mistakes
- Modifying the unknown system before completing Discovery (DSC-1: an unknown system SHALL pass through Discovery before any modification). [Ref: §25.4 DSC-1]
- Silently resolving disagreements between static and dynamic analysis (DSC-3). [Ref: §25.4 DSC-3]
- Asserting confidence exceeding evidence (DSC-6). [Ref: §25.4 DSC-6]
- Treating discovery as a single-pass, linear sequence rather than iterative and goal-directed (DSC-4; LC-3). [Ref: §25.4 DSC-4; §12.3 LC-3]
- Failing to record provenance for discovery outputs (DSC-2). [Ref: §25.4 DSC-2]

#### 5.11.9 References
- §12.2 (Discovery feeds into Understanding)
- §14 Knowledge Model
- §25 Engineering Discovery Model (full specification)
- §26 Evidence Confidence Model
- §27 Engineering Completion Criteria
- §28 Engineering Evidence Chain
- §31 Repository Knowledge Architecture
- §32 Engineering Mission Model
- §38 Engineering Documentation Model
- Demeyer et al., 2002; Chikofsky & Cross, 1990; Feathers, 2004

---

## 6. Competing Approaches

The following documented tensions SHALL be presented and context-bound per FR-12 and PR-12, not dogmatically resolved. [Ref: §12.4]

### 6.1 Plan-Driven / Architecture-First vs Evolutionary / Emergent Design

Context decides: high cost-of-change / regulated / safety-critical favors architecture-first; high-uncertainty / reversible favors evolutionary. [Ref: §12.4; Bass/Clements/Kazman, *Software Architecture in Practice*; Ford/Parsons/Kua, *Building Evolutionary Architectures*; reconciliation: Boehm & Turner, 2003]

The SES does not mandate either approach. The project SHALL select the approach that satisfies the stated process outcomes for its context. [Ref: §12.4; PR-12]

### 6.2 Rewrite vs Incremental Modernization (Strangler Fig)

Incremental modernization is the documented default at scale. [Ref: §12.4; Fowler, "StranglerFigApplication"; Brodie & Stonebraker, *Migrating Legacy Systems*, 1995]

The SES does not prohibit rewrites but notes that incremental modernization is the converged practice for large-scale system transformation. The project SHALL context-bind the choice per PR-12. [Ref: §12.4; PR-12]

### 6.3 Monolith-First vs Microservices

The SES presents both approaches without mandating either. [Ref: §12.4; Fowler, "MonolithFirst"; Newman, *Building Microservices*, 2nd ed.]

The project SHALL evaluate its context (team size, deployment topology, communication overhead, data consistency requirements) and select the approach that satisfies the stated process outcomes per PR-12. [Ref: §12.4; PR-12]

---

## 7. Completion Criteria

This document is complete when all of the following are satisfied: [Ref: §12.1; §12.3]

1. **LC-1 satisfaction**: Each of the 11 phases (§5.1–§5.11) defines explicit inputs, outputs, evidence produced, and verification criteria. [Ref: §12.3 LC-1]
2. **LC-2 satisfaction**: No phase asserts a conclusion not backed by evidence from the subject system. [Ref: §12.3 LC-2]
3. **LC-3 satisfaction**: Understanding and Analysis are treated as iterative, not single-pass; the lifecycle frame (§4) is presented as a DAG, not a waterfall. [Ref: §12.3 LC-3]
4. **LC-4 satisfaction**: Maintenance (§5.8) recognizes all four maintenance categories (corrective, adaptive, perfective, preventive). [Ref: §12.3 LC-4]
5. **LC-5 satisfaction**: Retirement (§5.10) is an explicit, planned phase with defined activities for data archival, consumer notification, and deprecation. [Ref: §12.3 LC-5]
6. **Per-phase field coverage**: Each phase (§5.1–§5.11) defines all 9 mandated fields (Objectives, Inputs, Activities, Outputs, Evidence Produced, Verification, Tools, Mistakes, References), with explicit marking where the SDD does not specify content for a field. [Ref: §12.1]
7. **Competing approaches**: §6 presents and context-binds all three documented tensions without dogmatic resolution. [Ref: §12.4]
8. **SDD citation coverage**: Every normative statement carries a [Ref: §X.Y] citation to the SDD. [Ref: FR-11; PR-1]
