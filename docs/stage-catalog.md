# Stage Catalog

> **Authority Class:** Authoritative
> **SDD Authority:** §13.2, §13.3, §12.2, §25.3, §15, §16
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 5

## 1. Purpose

This document specifies the catalog of engineering stages derived from the Engineering Lifecycle (§12.2) and the Engineering Discovery Model (§25.3). Every stage listed herein SHALL define the eight mandatory fields prescribed by §13.2. [Ref: §13.2]

The SES defines the meta-model of a stage in §13.1; this catalog populates that meta-model with the stages implied by the canonical lifecycle phases and the mandated discovery activities. [Ref: §13.1; §12.2; §25.3]

## 2. Scope

This document lists all stages derived from:
- The canonical lifecycle phases defined in §12.2.
- The mandated discovery activities defined in §25.3.

Each stage is specified using the eight-field schema mandated by §13.2. Where the SDD does not specify the content of a field, this document states so explicitly.

This document does NOT define: operational procedures within each stage (deferred to Phase 3/Phase 5 per §13); stage checklists (Phase 6/Phase 8); tools for executing stages (out of core scope, CN-1); templates for stage outputs (Phase 8). [Ref: §13; §24; CN-1]

## 3. Normative Rules (SG-1..SG-4)

The following rules govern all stages. Violation of any rule renders stage completion non-conformant. [Ref: §13.3]

| ID | Rule | Evidence |
|---|---|---|
| **SG-1** | A stage **MUST NOT** be declared complete unless its **exit criteria are verified** by the verification method named in its schema. [Ref: PR-7; IEEE 1028] |
| **SG-2** | Stage outputs **MUST** be classified per the Artifact Authority Model (§11). Every output SHALL carry an authority classification of Authoritative, Derived, or Generated. [Ref: PR-6] |
| **SG-3** | A stage **MAY** be re-entered (iteration); re-entry **MUST** be recorded. Iteration is expected per LC-3. [Ref: LC-3] |
| **SG-4** | Separation of duties: where a stage produces a change and another verifies it, the SES **SHOULD** keep these as distinct responsibilities. [Ref: PR-8; ISO/IEC/IEEE 1012] |

## 4. Stage Schema (8 fields)

Every stage in §5 SHALL define, at minimum, the following fields. [Ref: §13.2]

| Field | Meaning | Evidence Basis |
|---|---|---|
| **Entry Criteria** | Preconditions that MUST hold before the stage may begin | Stage-gate practice |
| **Inputs** | Authoritative artifacts consumed | ISO 12207 |
| **Activities** | Work performed | ISO 12207 |
| **Outputs** | Artifacts produced, with authority class | §11 |
| **Evidence Produced** | Verifiable evidence of the work | PR-5 |
| **Exit Criteria** | Postconditions that MUST hold to leave the stage | Stage-gate practice |
| **Verification Criteria** | How exit is objectively checked | PR-7, §16 |
| **Review Type** | Which review (§15) gates the stage | IEEE 1028 |

## 5. Stage Catalog

### 5.1 Discovery -- Inventory

Derived from the Inventory Layer (§25.2) and mandated discovery activities: Asset Inventory, Repository Inventory, Technology Detection, Build System Detection, Runtime Environment Detection. [Ref: §25.2; §25.3]

#### Entry Criteria
- The subject system is in the UNKNOWN state (§33.2).
- A Mission authorizing DISCOVER operations is active (§32 MIS-1, MIS-2).
- Read access to the subject system's repository and runtime environment is available.
- SDD does not specify additional entry criteria for this stage. [Ref: §25]

#### Inputs
- Subject system repository.
- Active Mission specifying discovery scope and constraints.
- SDD does not specify additional inputs for this stage. [Ref: §25]

#### Activities
- Asset Inventory: identify all version-controlled assets in the repository.
- Repository Inventory: identify repository structure, branches, tags, commit history.
- Technology Detection: identify programming languages, frameworks, platforms in use.
- Build System Detection: identify build tools, dependency managers, CI/CD configurations.
- Runtime Environment Detection: identify deployment targets, containers, servers, platforms.
- SDD does not specify detailed procedures for these activities. [Ref: §25.3]

#### Outputs
- Inventory report (Authority Class: Authoritative) documenting detected assets, technologies, build systems, and runtime environments.
- Observed Facts (Authority Class: Non-authoritative; Confidence Level A/B/E per §26) for each detected item.
- SDD does not specify output formats. [Ref: §25]

#### Evidence Produced
- Inventory listings with repository references.
- Technology detection results with provenance (file paths, tool outputs).
- Confidence classifications (§26 EVC-1) for each observed item.
- SDD does not specify additional evidence requirements. [Ref: §25; §26]

#### Exit Criteria
- All five inventory activities (Asset, Repository, Technology, Build System, Runtime Environment) have been performed.
- Results are recorded with provenance (§28 ECH-2).
- SDD does not specify quantitative exit criteria for this stage. [Ref: §25]

#### Verification Criteria
- Inventory results are recorded and traceable (§29 TRC-1).
- Results carry confidence levels (§26 EVC-1).
- SDD does not specify detailed verification procedures for this stage. [Ref: §25; §16]

#### Review Type
- Walkthrough (§15.1) for early-stage discovery feedback. [Ref: §15.1]

---

### 5.2 Discovery -- Structure

Derived from the Structure Layer (§25.2) and mandated discovery activities: Dependency Discovery, Module Discovery, API Discovery, Database Discovery, Configuration Discovery. [Ref: §25.2; §25.3]

#### Entry Criteria
- Discovery -- Inventory stage exit criteria are verified (SG-1).
- Inventory results are available as inputs.
- SDD does not specify additional entry criteria for this stage. [Ref: §25]

#### Inputs
- Inventory report from Discovery -- Inventory.
- Subject system source code and build artifacts.
- SDD does not specify additional inputs for this stage. [Ref: §25]

#### Activities
- Dependency Discovery: identify internal and external dependencies.
- Module Discovery: identify modules, packages, components, and their boundaries.
- API Discovery: identify API endpoints, protocols, contracts, and consumers.
- Database Discovery: identify database systems, schemas, migrations, and data flows.
- Configuration Discovery: identify configuration sources, formats, and environment-specific values.
- SDD does not specify detailed procedures for these activities. [Ref: §25.3]

#### Outputs
- Structure report (Authority Class: Authoritative) documenting dependencies, modules, APIs, databases, and configurations.
- Dependency graph fragments (Authority Class: Generated).
- Observed Facts with confidence levels (§26).
- SDD does not specify output formats. [Ref: §25]

#### Evidence Produced
- Dependency listings with source references.
- Module boundary descriptions with file mappings.
- API inventory with endpoint/contract summaries.
- Database schema documentation with provenance.
- Configuration inventory with source locations.
- SDD does not specify additional evidence requirements. [Ref: §25]

#### Exit Criteria
- All five structure activities (Dependency, Module, API, Database, Configuration) have been performed.
- Results are recorded with provenance (§28 ECH-2).
- SDD does not specify quantitative exit criteria for this stage. [Ref: §25]

#### Verification Criteria
- Structure results are recorded and traceable (§29 TRC-1).
- Results carry confidence levels (§26 EVC-1).
- Cross-validation where feasible (§25 DSC-3).
- SDD does not specify detailed verification procedures for this stage. [Ref: §25; §16]

#### Review Type
- Walkthrough (§15.1). [Ref: §15.1]

---

### 5.3 Discovery -- Security

Derived from the Security Layer (§25.2) and mandated discovery activities: Security Discovery, Authentication Discovery, Authorization Discovery. [Ref: §25.2; §25.3]

#### Entry Criteria
- Discovery -- Inventory stage exit criteria are verified (SG-1).
- Structure discovery results are available (recommended but not mandated by SDD).
- SDD does not specify additional entry criteria for this stage. [Ref: §25]

#### Inputs
- Subject system source code, configuration, and runtime.
- Inventory and structure discovery results.
- SDD does not specify additional inputs for this stage. [Ref: §25]

#### Activities
- Security Discovery: identify security mechanisms, vulnerabilities, and controls.
- Authentication Discovery: identify authentication methods, flows, and enforcement points.
- Authorization Discovery: identify authorization models, roles, permissions, and enforcement points.
- SDD does not specify detailed procedures for these activities. [Ref: §25.3]

#### Outputs
- Security report (Authority Class: Authoritative) documenting security, authentication, and authorization findings.
- Observed Facts with confidence levels (§26).
- Risk findings per §21 (where applicable).
- SDD does not specify output formats. [Ref: §25; §21]

#### Evidence Produced
- Security control inventory with source references.
- Authentication flow descriptions.
- Authorization model descriptions.
- Vulnerability findings with confidence levels.
- SDD does not specify additional evidence requirements. [Ref: §25]

#### Exit Criteria
- All three security activities (Security, Authentication, Authorization) have been performed.
- Results are recorded with provenance (§28 ECH-2).
- SDD does not specify quantitative exit criteria for this stage. [Ref: §25]

#### Verification Criteria
- Security results are recorded and traceable (§29 TRC-1).
- Results carry confidence levels (§26 EVC-1).
- SDD does not specify detailed verification procedures for this stage. [Ref: §25; §16]

#### Review Type
- Technical Review (§15.1) due to security sensitivity. [Ref: §15.1]

---

### 5.4 Discovery -- Behavior

Derived from the Behavior Layer (§25.2) and mandated discovery activities: Event Discovery, Workflow Discovery, Execution Flow Recovery, Runtime Observation. [Ref: §25.2; §25.3]

#### Entry Criteria
- Discovery -- Structure stage exit criteria are verified (SG-1).
- Security discovery results are available (recommended but not mandated by SDD).
- SDD does not specify additional entry criteria for this stage. [Ref: §25]

#### Inputs
- Subject system source code, runtime environment, and configuration.
- Structure discovery results (dependency/module/API context).
- SDD does not specify additional inputs for this stage. [Ref: §25]

#### Activities
- Event Discovery: identify events, event sources, handlers, and flows.
- Workflow Discovery: identify business/workflows, states, and transitions.
- Execution Flow Recovery: recover execution paths, entry points, call chains, and control flow.
- Runtime Observation: observe actual system behavior under execution (Level-A evidence per §26).
- SDD does not specify detailed procedures for these activities. [Ref: §25.3]

#### Outputs
- Behavior report (Authority Class: Authoritative) documenting events, workflows, execution flows, and runtime observations.
- Execution flow models (Authority Class: Derived/Generated).
- Observed Facts with confidence levels (§26), including Level-A (runtime) evidence.
- SDD does not specify output formats. [Ref: §25]

#### Evidence Produced
- Event inventory with source references.
- Workflow descriptions with state/transition mappings.
- Execution flow diagrams/recoveries with provenance.
- Runtime observation logs/results with Level-A confidence marking (§26).
- SDD does not specify additional evidence requirements. [Ref: §25]

#### Exit Criteria
- All four behavior activities (Event, Workflow, Execution Flow, Runtime Observation) have been performed.
- Results are recorded with provenance (§28 ECH-2).
- Runtime observations are classified as Level-A evidence (§26).
- SDD does not specify quantitative exit criteria for this stage. [Ref: §25]

#### Verification Criteria
- Behavior results are recorded and traceable (§29 TRC-1).
- Results carry confidence levels (§26 EVC-1).
- Runtime-vs-static disagreements follow EVC-6 (higher-fidelity governs). [Ref: §25; §26 EVC-6]
- SDD does not specify detailed verification procedures for this stage. [Ref: §25; §16]

#### Review Type
- Technical Review (§15.1). [Ref: §15.1]

---

### 5.5 Discovery -- Analysis Methods

Derived from the Analysis Methods component (§25.2) and mandated discovery activities: Static Analysis, Dynamic Analysis, Cross Validation. [Ref: §25.2; §25.3]

#### Entry Criteria
- Discovery -- Behavior stage exit criteria are verified (SG-1).
- Discovery outputs from prior stages are available as inputs.
- SDD does not specify additional entry criteria for this stage. [Ref: §25]

#### Inputs
- All discovery outputs from prior stages (Inventory, Structure, Security, Behavior).
- Subject system source code, build artifacts, and runtime environment.
- SDD does not specify additional inputs for this stage. [Ref: §25]

#### Activities
- Static Analysis: analyze source code without execution (code metrics, dependency analysis, pattern detection).
- Dynamic Analysis: analyze system behavior during execution (profiling, tracing, coverage).
- Cross Validation: triangulate findings across static and dynamic sources; record disagreements (§25 DSC-3).
- SDD does not specify detailed procedures for these activities. [Ref: §25.3]

#### Outputs
- Analysis report (Authority Class: Authoritative) documenting static analysis, dynamic analysis, and cross-validation results.
- Verified Facts (Authority Class: Candidate-authoritative) for findings that passed verification.
- Disagreement findings where static and dynamic analysis conflict (recorded, not silently resolved per §25 DSC-3).
- SDD does not specify output formats. [Ref: §25]

#### Evidence Produced
- Static analysis results with tool/method provenance.
- Dynamic analysis results with runtime provenance.
- Cross-validation matrix showing corroboration/conflict.
- Confidence levels for all findings (§26 EVC-1).
- SDD does not specify additional evidence requirements. [Ref: §25]

#### Exit Criteria
- All three analysis activities (Static, Dynamic, Cross Validation) have been performed.
- Cross-validation is performed; disagreements are recorded, not silently resolved (§25 DSC-3).
- Results are recorded with provenance (§28 ECH-2).
- SDD does not specify quantitative exit criteria for this stage. [Ref: §25]

#### Verification Criteria
- Analysis results are recorded and traceable (§29 TRC-1).
- Results carry confidence levels (§26 EVC-1).
- Static-dynamic disagreements are documented per DSC-3.
- SDD does not specify detailed verification procedures for this stage. [Ref: §25; §16]

#### Review Type
- Technical Review (§15.1). [Ref: §15.1]

---

### 5.6 Discovery -- Synthesis

Derived from the Synthesis component (§25.2) and mandated discovery activities: Architecture Recovery, Knowledge Extraction, Evidence Collection. [Ref: §25.2; §25.3]

#### Entry Criteria
- Discovery -- Analysis Methods stage exit criteria are verified (SG-1).
- Verified facts from analysis are available as inputs.
- SDD does not specify additional entry criteria for this stage. [Ref: §25]

#### Inputs
- All discovery outputs and verified facts from prior stages.
- Cross-validation results.
- SDD does not specify additional inputs for this stage. [Ref: §25]

#### Activities
- Architecture Recovery: produce higher-level architectural abstractions from lower-level artifacts.
- Knowledge Extraction: synthesize engineering knowledge from verified facts (§31 RKA-2).
- Evidence Collection: assemble and organize evidence for downstream stages.
- SDD does not specify detailed procedures for these activities. [Ref: §25.3; §30]

#### Outputs
- Recovered architecture documentation (Authority Class: Authoritative).
- Engineering Knowledge records (Authority Class: Authoritative) per §31.
- Evidence collection (Authority Class: Carries confidence) per §26, §28.
- SDD does not specify output formats. [Ref: §25; §31]

#### Evidence Produced
- Architecture recovery documentation with provenance.
- Knowledge records showing progression from Observed -> Verified -> Engineering Knowledge (§31 RKA-2).
- Evidence chain links preserved (§28 ECH-2).
- SDD does not specify additional evidence requirements. [Ref: §25; §28]

#### Exit Criteria
- All three synthesis activities (Architecture Recovery, Knowledge Extraction, Evidence Collection) have been performed.
- Knowledge has progressed through the Evidence Chain (§28).
- Architecture recovery is documented with provenance (§30 REV-2).
- SDD does not specify quantitative exit criteria for this stage. [Ref: §25; §28]

#### Verification Criteria
- Synthesis outputs are recorded and traceable (§29 TRC-1).
- Knowledge progression follows §31 RKA-2 (Observed -> Verified -> Engineering Knowledge via Evidence Chain).
- Architecture recovery is evidenced per §30 REV-2.
- SDD does not specify detailed verification procedures for this stage. [Ref: §25; §16]

#### Review Type
- Technical Review (§15.1). [Ref: §15.1]

---

### 5.7 Discovery -- Completion

Derived from the Output component (§25.2) and mandated discovery activities: Documentation (discovery), Verification (discovery), Discovery Complete. [Ref: §25.2; §25.3]

#### Entry Criteria
- Discovery -- Synthesis stage exit criteria are verified (SG-1).
- Synthesis outputs are available as inputs.
- SDD does not specify additional entry criteria for this stage. [Ref: §25]

#### Inputs
- All discovery outputs from prior stages.
- Recovered architecture and engineering knowledge.
- SDD does not specify additional inputs for this stage. [Ref: §25]

#### Activities
- Documentation: produce discovery documentation from collected knowledge.
- Verification: verify that Discovery Complete criteria (§27) are met.
- Discovery Complete: assert and record completion of the discovery phase.
- SDD does not specify detailed procedures for these activities. [Ref: §25.3; §27]

#### Outputs
- Discovery documentation (Authority Class: Derived/Authoritative per §38).
- Discovery Complete assertion with evidence (Authority Class: Authoritative).
- Validation records (Authority Class: Authoritative record) per §16.
- SDD does not specify output formats. [Ref: §25; §27]

#### Evidence Produced
- Discovery documentation with category declaration (§38 DOC-2).
- Discovery Complete evidence per §27 CMP-4 (completion evidenced and recorded).
- Verification records per §16 VL-3 (validation evidence recorded and reproducible).
- SDD does not specify additional evidence requirements. [Ref: §25; §27; §16]

#### Exit Criteria
- Discovery Complete completion state (§27.2) is objectively met.
- CMP-1: exit criteria are objective and verifiable.
- CMP-2: exit criteria are verified by a method in §16.2.
- CMP-4: completion is evidenced and recorded.
- SDD does not specify detailed per-state criteria; these are the Phase 5/6 deliverable per CMP-5. [Ref: §27; §27.3 CMP-5]

#### Verification Criteria
- Discovery Complete assertion cites the evidence on which it rests (§16 VL-4).
- Verification method is one of Inspection, Analysis, Demonstration, or Test (§16.2).
- SDD does not specify detailed verification procedures. [Ref: §27; §16]

#### Review Type
- Audit (§15.1) for Discovery Complete assertion. [Ref: §15.1]

---

### 5.8 Understanding

Derived from the Understanding phase of the Engineering Lifecycle (§12.2). [Ref: §12.2]

#### Entry Criteria
- Discovery activities have produced sufficient knowledge for the mission (§25 DSC-4).
- SDD does not specify detailed entry criteria for this stage. [Ref: §12.2]

#### Inputs
- Discovery outputs (Inventory, Structure, Security, Behavior, Analysis, Synthesis).
- Engineering Knowledge records (§31).
- SDD does not specify additional inputs for this stage. [Ref: §12.2]

#### Activities
- Synthesize discovery outputs into a coherent understanding of the subject system.
- Verify that understanding is sufficient for the Mission scope (§32 MIS-4).
- Record understanding as Engineering Knowledge (§31).
- SDD does not specify detailed procedures for this stage. [Ref: §12.2]

#### Outputs
- System understanding documentation (Authority Class: Authoritative).
- Engineering Knowledge records (§31).
- SDD does not specify output formats. [Ref: §12.2]

#### Evidence Produced
- Knowledge records with provenance (§28).
- Evidence of sufficiency for Mission scope.
- SDD does not specify additional evidence requirements. [Ref: §12.2]

#### Exit Criteria
- System understanding is sufficient for the Mission scope (§25 DSC-4).
- Knowledge is recorded with provenance (§28 ECH-2).
- SDD does not specify quantitative exit criteria for this stage. [Ref: §12.2]

#### Verification Criteria
- Understanding outputs are recorded and traceable (§29 TRC-1).
- Verification method per §16.2.
- SDD does not specify detailed verification procedures. [Ref: §12.2; §16]

#### Review Type
- Technical Review (§15.1). [Ref: §15.1]

---

### 5.9 Reverse Engineering / Reconstruction

Derived from the Reverse Engineering / Reconstruction phase of the Engineering Lifecycle (§12.2). [Ref: §12.2; §30]

#### Entry Criteria
- Understanding stage exit criteria are verified (SG-1).
- System understanding is sufficient for recovery.
- SDD does not specify additional entry criteria. [Ref: §12.2; §30]

#### Inputs
- System understanding documentation.
- Subject system artifacts (source, configuration, documentation).
- SDD does not specify additional inputs. [Ref: §12.2; §30]

#### Activities
- Recovery: produce higher-level abstractions from lower-level artifacts (§30 REV-2).
- Produce design documentation, architecture diagrams, and recovered contracts.
- Recovery MUST produce higher-level abstractions from lower-level artifacts, each evidenced (§26) and provenanced (§28). [Ref: §30 REV-2]
- SDD does not specify detailed procedures. [Ref: §12.2; §30]

#### Outputs
- Recovered design documentation (Authority Class: Authoritative).
- Recovered architecture abstractions (Authority Class: Authoritative).
- Recovered contracts (Authority Class: Authoritative per §11.3).
- SDD does not specify output formats. [Ref: §12.2; §30]

#### Evidence Produced
- Recovery documentation with provenance (§28).
- Confidence levels for recovered abstractions (§26).
- Evidence that recovery is examination-only (no modification per §30 REV-1).
- SDD does not specify additional evidence requirements. [Ref: §30]

#### Exit Criteria
- Higher-level abstractions are produced from lower-level artifacts (§30 REV-2).
- Recovery is examination-only; the subject system is not altered (§30 REV-1).
- All outputs are evidenced and provenanced.
- SDD does not specify quantitative exit criteria. [Ref: §12.2; §30]

#### Verification Criteria
- Recovery outputs are recorded and traceable (§29 TRC-1).
- Recovery results carry confidence levels (§26 EVC-1).
- Verification method per §16.2.
- SDD does not specify detailed verification procedures. [Ref: §12.2; §16]

#### Review Type
- Inspection (§15.1) for recovered contracts and architecture. [Ref: §15.1]

---

### 5.10 Analysis

Derived from the Analysis phase of the Engineering Lifecycle (§12.2). [Ref: §12.2]

#### Entry Criteria
- Reverse Engineering / Reconstruction stage exit criteria are verified (SG-1).
- Recovered design and architecture are available.
- SDD does not specify additional entry criteria. [Ref: §12.2]

#### Inputs
- Recovered design documentation.
- Recovered architecture abstractions.
- Subject system artifacts.
- SDD does not specify additional inputs. [Ref: §12.2]

#### Activities
- Analyze dependencies, execution flow, contracts, and gaps.
- Produce engineering conclusions from examination.
- Analysis is examination producing engineering conclusions (§46.2 Analysis definition).
- SDD does not specify detailed procedures. [Ref: §12.2]

#### Outputs
- Analysis report (Authority Class: Authoritative).
- Gap analysis documentation.
- Engineering conclusions with evidence.
- SDD does not specify output formats. [Ref: §12.2]

#### Evidence Produced
- Analysis conclusions with provenance (§28).
- Confidence levels for conclusions (§26).
- Gap findings documented as findings/risks per §21.
- SDD does not specify additional evidence requirements. [Ref: §12.2; §21]

#### Exit Criteria
- Dependencies are analyzed and documented.
- Execution flow is analyzed and documented.
- Contracts are analyzed and documented.
- Gaps are identified and recorded.
- SDD does not specify quantitative exit criteria. [Ref: §12.2]

#### Verification Criteria
- Analysis outputs are recorded and traceable (§29 TRC-1).
- Verification method per §16.2.
- SDD does not specify detailed verification procedures. [Ref: §12.2; §16]

#### Review Type
- Technical Review (§15.1). [Ref: §15.1]

---

### 5.11 Planning

Derived from the Planning phase of the Engineering Lifecycle (§12.2). [Ref: §12.2; §35]

#### Entry Criteria
- Analysis stage exit criteria are verified (SG-1).
- Analysis results (dependencies, execution flow, contracts, gaps) are available.
- SDD does not specify additional entry criteria. [Ref: §12.2]

#### Inputs
- Analysis report.
- Gap analysis.
- Engineering conclusions.
- Active Mission scope and constraints.
- SDD does not specify additional inputs. [Ref: §12.2]

#### Activities
- Produce design documents and ADRs.
- Perform risk assessment and sequencing.
- Record decisions (§35 DEC-1).
- Planning produces decisions/plans before change (§46.2 Planning definition).
- SDD does not specify detailed procedures. [Ref: §12.2; §35]

#### Outputs
- Design documents (Authority Class: Authoritative).
- Architecture Decision Records (Authority Class: Authoritative; immutable once accepted) (§11.3).
- Risk assessment (Authority Class: Authoritative).
- Sequencing plan (Authority Class: Authoritative).
- SDD does not specify output formats. [Ref: §12.2; §35]

#### Evidence Produced
- Decision records with all nine fields (§35.2).
- Impact analysis results (§36 IMP-1).
- Risk records per §21.
- SDD does not specify additional evidence requirements. [Ref: §12.2; §35; §36]

#### Exit Criteria
- All required decisions are recorded and approved (§35 DEC-1, DEC-3).
- Impact analysis is performed (§36 IMP-1).
- Risk assessment is documented.
- Sequencing plan is documented.
- SDD does not specify quantitative exit criteria. [Ref: §12.2]

#### Verification Criteria
- All decisions carry nine fields (§35 DEC-1).
- All implementations trace to a decision (§35 DEC-4).
- Verification method per §16.2.
- SDD does not specify detailed verification procedures. [Ref: §12.2; §16]

#### Review Type
- Inspection (§15.1) for ADRs and design documents. [Ref: §15.1]

---

### 5.12 Implementation

Derived from the Implementation phase of the Engineering Lifecycle (§12.2). [Ref: §12.2]

#### Entry Criteria
- Planning stage exit criteria are verified (SG-1).
- All required decisions are recorded and approved.
- Mission Allowed Operations include IMPLEMENT (§32, §34).
- Impact analysis is performed (§36 IMP-1).
- SDD does not specify additional entry criteria. [Ref: §12.2; §36]

#### Inputs
- Approved design documents and ADRs.
- Sequencing plan.
- Active Mission with IMPLEMENT in Allowed Operations.
- SDD does not specify additional inputs. [Ref: §12.2]

#### Activities
- Realize approved decisions through small, isolated, reviewed, reversible changes.
- Every change traces back to exactly one engineering Decision (§35 DEC-4).
- Implementation realizes an approved decision (§46.2 Implementation definition).
- SDD does not specify detailed procedures. [Ref: §12.2]

#### Outputs
- Implemented changes (Authority Class: Authoritative).
- Change records with decision traceability.
- Updated artifacts.
- SDD does not specify output formats. [Ref: §12.2]

#### Evidence Produced
- Change records with decision references (§35 DEC-4).
- Review records (§15 RV-5).
- Implementation evidence per §28 (Decision -> Implementation link).
- SDD does not specify additional evidence requirements. [Ref: §12.2; §28]

#### Exit Criteria
- Approved decisions are realized.
- Changes are reviewed and recorded.
- All implementations trace to a decision (§35 DEC-4).
- INT rules (§40) are satisfied (no undocumented implementation).
- SDD does not specify quantitative exit criteria. [Ref: §12.2; §40]

#### Verification Criteria
- Implementation outputs are recorded and traceable (§29 TRC-1).
- Verification method per §16.2.
- SDD does not specify detailed verification procedures. [Ref: §12.2; §16]

#### Review Type
- Inspection (§15.1) for high-risk changes; Technical Review (§15.1) for standard changes. [Ref: §15.1]

---

### 5.13 Validation

Derived from the Validation phase of the Engineering Lifecycle (§12.2). [Ref: §12.2; §16]

#### Entry Criteria
- Implementation stage exit criteria are verified (SG-1).
- Implemented changes are available for validation.
- §16 preconditions are met.
- SDD does not specify additional entry criteria. [Ref: §12.2; §16]

#### Inputs
- Implemented changes.
- Validation criteria from Mission.
- Subject system in testable state.
- SDD does not specify additional inputs. [Ref: §12.2; §16]

#### Activities
- Execute validation ordering: static analysis -> unit -> integration -> contract -> regression -> system/E2E -> non-functional -> runtime verification -> review (§16.3).
- Record validation evidence.
- Validation is an objective conformance check (§46.2 Validation definition).
- SDD does not specify detailed procedures. [Ref: §12.2; §16.3]

#### Outputs
- Validation verdict (Authority Class: Authoritative record) per §16.
- Validation records (Authority Class: Authoritative record).
- Defect/finding records (where applicable).
- SDD does not specify output formats. [Ref: §12.2; §16]

#### Evidence Produced
- Validation evidence recorded and reproducible (§16 VL-3).
- Conformance verdict cites evidence (§16 VL-4).
- Test/check results with provenance.
- SDD does not specify additional evidence requirements. [Ref: §16]

#### Exit Criteria
- All applicable validation layers are executed.
- Conformance verdict is objective pass/fail (§16 VL-1).
- Validation evidence is recorded and reproducible (§16 VL-3).
- Validation Complete completion state (§27.2) is objectively met.
- SDD does not specify quantitative exit criteria. [Ref: §12.2; §16; §27]

#### Verification Criteria
- Validation outputs are recorded and traceable (§29 TRC-1).
- Verification method per §16.2.
- Validation is distinct from implementation (§16 VL-5; PR-8).
- SDD does not specify detailed verification procedures. [Ref: §16]

#### Review Type
- Audit (§15.1) for conformance verification. [Ref: §15.1]

---

### 5.14 Documentation

Derived from the Documentation phase of the Engineering Lifecycle (§12.2). [Ref: §12.2; §38]

#### Entry Criteria
- Validation stage exit criteria are verified (SG-1).
- Validation verdict is pass.
- SDD does not specify additional entry criteria. [Ref: §12.2; §38]

#### Inputs
- All prior stage outputs.
- Validation verdict.
- Engineering knowledge records.
- SDD does not specify additional inputs. [Ref: §12.2; §38]

#### Activities
- Produce authoritative documentation from engineering knowledge.
- Produce generated documentation from authoritative sources.
- Classify each documentation unit per §38.2 categories.
- Documentation is categorized recorded knowledge (§46.2 Documentation definition).
- SDD does not specify detailed procedures. [Ref: §12.2; §38]

#### Outputs
- Documentation units (Authority Class: per §38.2 -- Auth/Derived/Generated).
- Documentation category declarations (§38 DOC-2).
- Updated traceability index.
- SDD does not specify output formats. [Ref: §12.2; §38]

#### Evidence Produced
- Documentation with category and authority class declarations (§38 DOC-2).
- Evidence that generated documentation is reproducible (§38 DOC-3).
- SDD does not specify additional evidence requirements. [Ref: §38]

#### Exit Criteria
- All documentation units declare category and authority class (§38 DOC-2).
- Generated documentation is reproducible (§38 DOC-3).
- Documentation Complete completion state (§27.2) is objectively met.
- §38 categories are satisfied.
- SDD does not specify quantitative exit criteria. [Ref: §12.2; §27; §38]

#### Verification Criteria
- Documentation outputs are recorded and traceable (§29 TRC-1).
- No mixed categories within one authoritative unit (§38 DOC-1).
- Verification method per §16.2.
- SDD does not specify detailed verification procedures. [Ref: §38; §16]

#### Review Type
- Technical Review (§15.1). [Ref: §15.1]

---

### 5.15 Maintenance

Derived from the Maintenance phase of the Engineering Lifecycle (§12.2). [Ref: §12.2; §33]

#### Entry Criteria
- Documentation stage exit criteria are verified (SG-1).
- The subject system is in COMPLETED state (§33.2).
- A maintenance Mission is active.
- SDD does not specify additional entry criteria. [Ref: §12.2; §33]

#### Inputs
- System documentation.
- Active maintenance Mission.
- SDD does not specify additional inputs. [Ref: §12.2]

#### Activities
- Corrective maintenance: diagnose and fix defects.
- Adaptive maintenance: adapt to environmental changes.
- Perfective maintenance: improve performance, maintainability, or other attributes.
- Preventive maintenance: detect and correct latent faults before they become effective.
- Maintenance SHALL recognize the four maintenance categories (LC-4). [Ref: §12.3 LC-4]
- SDD does not specify detailed procedures. [Ref: §12.2]

#### Outputs
- Maintenance change records (Authority Class: Authoritative).
- Updated documentation.
- Updated knowledge records.
- SDD does not specify output formats. [Ref: §12.2]

#### Evidence Produced
- Change records with decision traceability (§35 DEC-4).
- Review records (§15 RV-5).
- Updated evidence chain links (§28).
- SDD does not specify additional evidence requirements. [Ref: §12.2]

#### Exit Criteria
- Maintenance work is reviewed and validated.
- Changes are documented and traceable.
- INT rules (§40) remain satisfied.
- SDD does not specify quantitative exit criteria. [Ref: §12.2; §40]

#### Verification Criteria
- Maintenance outputs are recorded and traceable (§29 TRC-1).
- Verification method per §16.2.
- SDD does not specify detailed verification procedures. [Ref: §12.2; §16]

#### Review Type
- Technical Review (§15.1). [Ref: §15.1]

---

### 5.16 Evolution

Derived from the Evolution phase of the Engineering Lifecycle (§12.2). [Ref: §12.2; §39]

#### Entry Criteria
- The subject system is under governance.
- A change proposal is approved (§17 GV-3).
- SDD does not specify additional entry criteria. [Ref: §12.2; §39]

#### Inputs
- Approved change proposal.
- Current system state and documentation.
- Active Mission authorizing evolution.
- SDD does not specify additional inputs. [Ref: §12.2; §39]

#### Activities
- Execute controlled change under governance.
- Produce per-cycle outputs: New Knowledge, Updated Knowledge, Deprecated Knowledge, Generated Knowledge, Review Records, Validation Records, Decision Records, Traceability Updates (§39.2).
- Every cycle emits applicable §39.2 outputs (EVO-1). [Ref: §39.2; §39.3 EVO-1]
- SDD does not specify detailed procedures. [Ref: §12.2; §39]

#### Outputs
- Per-cycle outputs per §39.2, each as a classified Repository Knowledge artifact (§31).
- Updated system artifacts.
- Governance records.
- SDD does not specify output formats. [Ref: §12.2; §39]

#### Evidence Produced
- Cycle output records (§39.2).
- Decision records for changes (§35).
- Review and validation records (§15, §16).
- Traceability updates (§29).
- SDD does not specify additional evidence requirements. [Ref: §39]

#### Exit Criteria
- All per-cycle outputs (§39.2) are produced and classified per §31.
- Updates preserve history; superseded knowledge becomes Historical (§39.3 EVO-3).
- Changes are governed and versioned (§39.3 EVO-4).
- SDD does not specify quantitative exit criteria. [Ref: §12.2; §39]

#### Verification Criteria
- Evolution outputs are recorded and traceable (§29 TRC-1).
- History preservation verified (§39.3 EVO-3).
- Verification method per §16.2.
- SDD does not specify detailed verification procedures. [Ref: §39; §16]

#### Review Type
- Management Review (§15.1) for governance gates. [Ref: §15.1]

---

### 5.17 Retirement

Derived from the Retirement phase of the Engineering Lifecycle (§12.2). [Ref: §12.2; §33]

#### Entry Criteria
- The subject system is in MAINTAINING state (§33.2).
- A retirement decision is approved (§35).
- SDD does not specify additional entry criteria. [Ref: §12.2; §33]

#### Inputs
- System documentation and knowledge records.
- Approved retirement decision.
- SDD does not specify additional inputs. [Ref: §12.2]

#### Activities
- Data archival.
- Consumer notification.
- Deprecation policy enforcement.
- Retirement SHALL be an explicit, planned phase, not an implicit event (LC-5). [Ref: §12.3 LC-5]
- SDD does not specify detailed procedures. [Ref: §12.2]

#### Outputs
- Retirement plan (Authority Class: Authoritative).
- Archival records (Authority Class: Authoritative).
- Deprecation notices (Authority Class: Authoritative).
- System state transition to ARCHIVED (§33.2).
- SDD does not specify output formats. [Ref: §12.2; §33]

#### Evidence Produced
- Retirement decision record (§35).
- Archival evidence with provenance.
- Consumer notification records.
- SDD does not specify additional evidence requirements. [Ref: §12.2]

#### Exit Criteria
- Data archival is completed.
- Consumers are notified.
- Deprecation policy is enacted.
- System state is ARCHIVED (§33.2).
- SDD does not specify quantitative exit criteria. [Ref: §12.2; §33]

#### Verification Criteria
- Retirement outputs are recorded and traceable (§29 TRC-1).
- State transition to ARCHIVED is verified (§33 STA-2).
- Verification method per §16.2.
- SDD does not specify detailed verification procedures. [Ref: §12.2; §16]

#### Review Type
- Management Review (§15.1) for retirement authorization. [Ref: §15.1]

## 6. Completion Criteria

This document is complete when:

1. All four normative rules SG-1 through SG-4 are stated (§3). [Ref: §13.3]
2. The eight-field stage schema is stated (§4). [Ref: §13.2]
3. Every stage derived from §12.2 and §25.3 is listed with all eight fields populated (§5). [Ref: §12.2; §25.3]
4. Every field explicitly cites its SDD authority or states "SDD does not specify."
5. Stages are ordered consistent with the dependency ordering of §12.2 and §25.2.
6. All fields use RFC 2119 keywords per §46. [Ref: §46]
