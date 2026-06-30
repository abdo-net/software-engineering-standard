# State Machine Specification

> **Authority Class:** Authoritative
> **SDD Authority:** §33, §27, §40
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 3

## 1. Purpose

This document specifies the canonical engineering state machine through which a subject system progresses under a Mission. [Ref: §33.1] The state machine defines nine mandatory states, their entry and exit conditions, required evidence, produced artifacts, and the normative rules governing transitions. [Ref: §33.2] This document implements the Phase-3 operational specification of the Engineering State Model defined architecturally in §33. [Ref: §33, Phase boundary note]

The state machine aligns with the Engineering Lifecycle phases (§12.2) and with life-cycle stage standards. [Ref: §33.1] A state's Exit Conditions equal the corresponding Completion-State criteria (§27); the state machine and the completion model are two views of one gate set. [Ref: §33.3]

---

## 2. State Machine Definition

The engineering state machine comprises nine mandatory states arranged in the following directed progression: [Ref: §33.2]

```
UNKNOWN → DISCOVERING → UNDERSTOOD → DOCUMENTED → PLANNED → IMPLEMENTING
→ VALIDATING → COMPLETED → MAINTAINING → ARCHIVED
```

### 2.1 State Ordering

The ordering is a dependency ordering of lifecycle phases, not a claim that work is performed once, linearly. [Ref: §12.3, LC-3] Iteration is expected and is supported by the evidence base. [Ref: §12.3] Re-entry to a previously occupied state is permitted under stage-gate iteration rules. [Ref: §13.3, SG-3]

### 2.2 Terminal States

- **ARCHIVED** is a terminal state. SDD does not specify exit conditions for ARCHIVED. [Ref: §33.2]
- **COMPLETED** may transition forward to MAINTAINING or, under retirement conditions, toward ARCHIVED. SDD does not specify the detailed COMPLETED → ARCHIVED path. [Ref: §33.2; §12.2 Retirement phase]

---

## 3. State-to-Lifecycle Mapping

The following table maps each state to its governing lifecycle phase(s): [Ref: §33.2]

| State | Lifecycle Phase | Governing Section |
|---|---|---|
| **DISCOVERING** | Discovery / Understanding | §25 (Engineering Discovery Model) |
| **UNDERSTOOD** | Reverse Engineering / Reconstruction | §30 (Reverse Engineering Architecture); §25 |
| **DOCUMENTED** | Documentation | §38 (Engineering Documentation Model) |
| **PLANNED** | Planning | §7 (Engineering Principles); §35 (Engineering Decision Model); §12 Planning |
| **IMPLEMENTING** | Implementation | §12 (Engineering Lifecycle — Implementation) |
| **VALIDATING** | Validation | §16 (Validation Model) |
| **COMPLETED** | "Engineering Complete" | §27 (Engineering Completion Criteria) |
| **MAINTAINING** | Maintenance | §12.3, LC-4 (maintenance categories) |
| **ARCHIVED** | Retirement | §12.3, LC-5 (retirement as explicit phase) |

---

## 4. Normative Rules

### 4.1 STA-1 — Single State Occupancy

A subject system **MUST** occupy exactly one state at a time under a given Mission. [Ref: §33.4, STA-1; OMG UML state-machine semantics] Concurrent state occupancy under a single Mission is prohibited. [Ref: STA-1]

### 4.2 STA-2 — Transition Gating

A transition **MUST NOT** occur unless the source state's Exit Conditions are verified. [Ref: §33.4, STA-2; §16; §27, CMP-2] Verification **MUST** be performed by a method defined in the Validation Model (§16.2). [Ref: §16.2]

### 4.3 STA-3 — Four-Element Completeness

Each state **MUST** define its four elements: Entry Conditions; Exit Conditions; Required Evidence; Produced Artifacts. [Ref: §33.4, STA-3; §33.3; ISO 12207; PR-7] A state whose four elements are not defined is incomplete and **MUST NOT** be occupied. [Ref: STA-3]

### 4.4 STA-4 — Transition Recording

Transitions **MUST** be recorded as evidence and are traceable. [Ref: §33.4, STA-4; PR-5; §29] Every transition **MUST** carry provenance linking it to the verification that enabled it. [Ref: §28, Evidence Chain]

### 4.5 STA-5 — INT Violation Blocking

An INT (§40) violation **MUST** block the transition out of its originating state. [Ref: §33.4, STA-5; §40] No transition **MAY** proceed while an integrity rule violation remains unresolved. [Ref: STA-5; §40.2] INT rules **MAY** be waived only through governance (§17). [Ref: §40.2]

---

## 5. State Specifications

### 5.1 UNKNOWN

UNKNOWN is the initial state of every subject system upon first encounter under a new Mission. [Ref: §33.2; §25.2]

#### 5.1.1 Entry Conditions

The subject system enters UNKNOWN when a new Mission is activated (§32) and no prior engineering state has been established for that system under that Mission. [Ref: §32, MIS-1; §33.2]

#### 5.1.2 Exit Conditions

SDD does not specify Exit Conditions for the UNKNOWN state. [Ref: §33.2] The transition from UNKNOWN to DISCOVERING is triggered by the commencement of Discovery activities (§25). [Ref: §25.2; §25.3]

#### 5.1.3 Required Evidence

SDD does not specify Required Evidence for the UNKNOWN state. [Ref: §33.3]

#### 5.1.4 Produced Artifacts

SDD does not specify Produced Artifacts for the UNKNOWN state. [Ref: §33.3]

#### 5.1.5 Lifecycle Mapping

UNKNOWN corresponds to the "Unknown System" entry point of the Engineering Lifecycle (§12.2). [Ref: §12.2; §25.2]

---

### 5.2 DISCOVERING

DISCOVERING is the state in which the subject system is being discovered, inventoried, and understood through goal-directed, iterative, evidence-producing activities. [Ref: §33.2; §25.2]

#### 5.2.1 Entry Conditions

The subject system enters DISCOVERING when the UNKNOWN state yields to active Discovery. SDD does not specify formal Entry Conditions for DISCOVERING beyond the initiation of Discovery activities. [Ref: §33.3; §25]

#### 5.2.2 Exit Conditions

Exit from DISCOVERING **MUST** equal the "Discovery Complete" Completion-State criteria defined in §27. [Ref: §33.3] Discovery is complete only when the "Discovery Complete" criteria are objectively met. [Ref: §25.4, DSC-5] These criteria **MUST** be verified by a method in §16.2. [Ref: §27, CMP-2] Detailed per-state criteria are deferred to Phase 5/6. [Ref: §27, CMP-5]

#### 5.2.3 Required Evidence

Every discovery output **MUST** carry provenance (KN-1) and a confidence level (§26). [Ref: §25.4, DSC-2] Discovery **MUST** combine static and dynamic analysis and cross-validate (triangulate); disagreements **MUST** be recorded, not silently resolved. [Ref: §25.4, DSC-3] No discovery conclusion **MAY** assert confidence exceeding its evidence (§26). [Ref: §25.4, DSC-6]

#### 5.2.4 Produced Artifacts

SDD does not specify the complete set of Produced Artifacts for the DISCOVERING state. [Ref: §33.3] The Discovery Model (§25.2) defines evidence layers (Inventory, Structure, Security, Behavior) and analysis outputs as architectural categories; detailed artifact specifications are deferred to Phase 3 (lifecycle) and Phase 5 (stages). [Ref: §25, Phase boundary note]

#### 5.2.5 Lifecycle Mapping

DISCOVERING corresponds to the Discovery/Understanding phases of the Engineering Lifecycle (§12.2). [Ref: §33.2]

---

### 5.3 UNDERSTOOD

UNDERSTOOD is the state in which the subject system has been sufficiently discovered and analyzed for the Mission at hand. [Ref: §33.2; §25.4, DSC-4]

#### 5.3.1 Entry Conditions

Entry to UNDERSTOOD **MUST** equal the "Discovery Complete" Completion-State criteria (§27), which are the Exit Conditions of DISCOVERING. [Ref: §33.3] Sufficiency for the Mission is the criterion, not complete comprehension. [Ref: §25.4, DSC-4]

#### 5.3.2 Exit Conditions

SDD does not specify Exit Conditions for the UNDERSTOOD state. [Ref: §33.3] The transition from UNDERSTOOD to DOCUMENTED is governed by the Documentation Model (§38). [Ref: §38]

#### 5.3.3 Required Evidence

SDD does not specify Required Evidence for the UNDERSTOOD state beyond the evidence already required by the DISCOVERING Exit Conditions. [Ref: §33.3]

#### 5.3.4 Produced Artifacts

SDD does not specify Produced Artifacts for the UNDERSTOOD state. [Ref: §33.3]

#### 5.3.5 Lifecycle Mapping

UNDERSTOOD corresponds to the Reverse Engineering / Reconstruction phases of the Engineering Lifecycle (§12.2). [Ref: §33.2; §30.2]

---

### 5.4 DOCUMENTED

DOCUMENTED is the state in which the subject system's engineering knowledge has been recorded in categorized documentation per the Documentation Model (§38). [Ref: §33.2; §38]

#### 5.4.1 Entry Conditions

Entry to DOCUMENTED **MUST** satisfy the requirements of the Documentation Model (§38). Documentation **MUST NOT** mix categories within one authoritative unit (DOC-1). [Ref: §38.3, DOC-1] Each documentation unit **MUST** declare its category (§38.2) and its authority class (§11.2). [Ref: §38.3, DOC-2]

#### 5.4.2 Exit Conditions

Exit from DOCUMENTED **MUST** equal the "Documentation Complete" Completion-State criteria defined in §27. [Ref: §33.3] Detailed criteria are deferred to Phase 5/6. [Ref: §27, CMP-5]

#### 5.4.3 Required Evidence

Observed/Planned documentation **MUST NOT** be presented as Verified/Validated without passing the Evidence Chain (§28) / Validation (§16). [Ref: §38.3, DOC-4]

#### 5.4.4 Produced Artifacts

SDD does not specify the complete set of Produced Artifacts for the DOCUMENTED state. [Ref: §33.3] Documentation units **SHALL** be classified per §38.2 categories (Observed; Verified; Planned; Implemented; Validated; Historical; Deprecated; Generated; Authoritative). [Ref: §38.2]

#### 5.4.5 Lifecycle Mapping

DOCUMENTED corresponds to the Documentation phase of the Engineering Lifecycle (§12.2). [Ref: §33.2]

---

### 5.5 PLANNED

PLANNED is the state in which engineering decisions have been recorded and plans have been produced before modification. [Ref: §33.2; §35; §12.2 Planning]

#### 5.5.1 Entry Conditions

Entry to PLANNED **MUST** be preceded by adequate documentation (DOCUMENTED state) and **MUST** satisfy the Decision Model (§35) requirements. Every Decision **MUST** be recorded with all nine fields (§35.2). [Ref: §35.3, DEC-1] A Decision **MUST** cite the Evidence (§26/§28) and the Impact Analysis (§36) that justify it. [Ref: §35.3, DEC-2]

#### 5.5.2 Exit Conditions

SDD does not specify Exit Conditions for the PLANNED state. [Ref: §33.3] Planning exits when the Implementation phase is authorized. SDD does not define formal Planning completion criteria. [Ref: §33.3; §27]

#### 5.5.3 Required Evidence

Every Decision **MUST** cite the Evidence (§26/§28) and the Impact Analysis (§36) that justify it. [Ref: §35.3, DEC-2]

#### 5.5.4 Produced Artifacts

SDD does not specify the complete set of Produced Artifacts for the PLANNED state. [Ref: §33.3] Decisions are immutable once Approved; change occurs only by a new Decision setting "Superseded By." [Ref: §35.3, DEC-3]

#### 5.5.5 Lifecycle Mapping

PLANNED corresponds to the Planning phase of the Engineering Lifecycle (§12.2). [Ref: §33.2]

---

### 5.6 IMPLEMENTING

IMPLEMENTING is the state in which approved decisions are being realized as changes to the subject system. [Ref: §33.2; §12.2 Implementation]

#### 5.6.1 Entry Conditions

Entry to IMPLEMENTING **MUST** be preceded by the PLANNED state and **MUST** satisfy the Impact Analysis Model (§36). Every Implementation **MUST** begin with an impact analysis spanning the §36.2 dimensions. [Ref: §36.3, IMP-1] Impact analysis **MUST** use the dependency view (§12 Analysis) and traceability (§29). [Ref: §36.3, IMP-2] Identified impacts **MUST** be recorded as evidence and **MUST** feed the authorizing Decision (§35). [Ref: §36.3, IMP-3]

#### 5.6.2 Exit Conditions

SDD does not specify Exit Conditions for the IMPLEMENTING state. [Ref: §33.3] The Exit Conditions of IMPLEMENTING **SHALL** be defined in Phase 5 as implementation-stage exit criteria.

#### 5.6.3 Required Evidence

Impact analysis **MUST** precede the IMPLEMENTING state. [Ref: §36.3, IMP-5] A change whose impact cannot be determined **MUST** be treated as high-risk and **MUST NOT** proceed without explicit Mission authorization (§32). [Ref: §36.3, IMP-4]

#### 5.6.4 Produced Artifacts

Every Implementation **MUST** trace back to exactly one engineering Decision. [Ref: §35.3, DEC-4]

#### 5.6.5 Lifecycle Mapping

IMPLEMENTING corresponds to the Implementation phase of the Engineering Lifecycle (§12.2). [Ref: §33.2]

---

### 5.7 VALIDATING

VALIDATING is the state in which the implementation is being objectively verified against stated criteria. [Ref: §33.2; §16]

#### 5.7.1 Entry Conditions

Entry to VALIDATING **MUST** be preceded by the IMPLEMENTING state. The implementation **MUST** be complete to the extent required by the Mission before Validation commences. SDD does not specify additional formal Entry Conditions for VALIDATING. [Ref: §33.3; §16]

#### 5.7.2 Exit Conditions

Exit from VALIDATING **MUST** equal the "Validation Complete" Completion-State criteria defined in §27. [Ref: §33.3] A conformance verdict **MUST** cite the evidence on which it rests (PR-5). [Ref: §16.4, VL-4] Validation **MUST** be a responsibility distinct from implementation/execution (PR-8). [Ref: §16.4, VL-5] Detailed criteria are deferred to Phase 5/6. [Ref: §27, CMP-5]

#### 5.7.3 Required Evidence

Validation evidence **MUST** be recorded and reproducible. [Ref: §16.4, VL-3] Each requirement class **MUST** have a defined verification method (§16.2). [Ref: §16.4, VL-2]

#### 5.7.4 Produced Artifacts

SDD does not specify the complete set of Produced Artifacts for the VALIDATING state. [Ref: §33.3] Validation produces conformance verdicts and recorded evidence. [Ref: §16.4, VL-4]

#### 5.7.5 Lifecycle Mapping

VALIDATING corresponds to the Validation phase of the Engineering Lifecycle (§12.2). [Ref: §33.2]

---

### 5.8 COMPLETED

COMPLETED is the state in which all subordinate completion states are complete and evidenced, marking "Engineering Complete." [Ref: §33.2; §27]

#### 5.8.1 Entry Conditions

Entry to COMPLETED **MUST** equal the "Engineering Complete" Completion-State criteria defined in §27. [Ref: §33.3] "Engineering Complete" **MUST NOT** be asserted unless all subordinate completion states are complete and evidenced. [Ref: §27.3, CMP-3] Completion **MUST** be evidenced and recorded (provenance). [Ref: §27.3, CMP-4]

#### 5.8.2 Exit Conditions

SDD does not specify Exit Conditions for the COMPLETED state. [Ref: §33.3] The COMPLETED state transitions forward to MAINTAINING for systems entering maintenance, or toward ARCHIVED for systems being retired. SDD does not define formal criteria for these transitions. [Ref: §33.2]

#### 5.8.3 Required Evidence

Each completion state **MUST** define objective, verifiable exit criteria; subjective "done" is prohibited. [Ref: §27.3, CMP-1] A completion state is reached only when its exit criteria are verified by a method in §16.2. [Ref: §27.3, CMP-2]

#### 5.8.4 Produced Artifacts

SDD does not specify Produced Artifacts for the COMPLETED state. [Ref: §33.3]

#### 5.8.5 Lifecycle Mapping

COMPLETED corresponds to "Engineering Complete" (§27). [Ref: §33.2]

---

### 5.9 MAINTAINING

MAINTAINING is the state in which the subject system is under active maintenance. [Ref: §33.2; §12.3, LC-4]

#### 5.9.1 Entry Conditions

Entry to MAINTAINING **MUST** be preceded by the COMPLETED state. SDD does not specify additional formal Entry Conditions for MAINTAINING. [Ref: §33.3]

#### 5.9.2 Exit Conditions

SDD does not specify Exit Conditions for the MAINTAINING state. [Ref: §33.3] The MAINTAINING state exits toward ARCHIVED when the system enters retirement (LC-5). SDD does not define formal criteria for this transition. [Ref: §33.2; §12.3, LC-5]

#### 5.9.3 Required Evidence

SDD does not specify Required Evidence for the MAINTAINING state. [Ref: §33.3] Maintenance **SHALL** recognize the four maintenance categories: corrective, adaptive, perfective, preventive. [Ref: §12.3, LC-4]

#### 5.9.4 Produced Artifacts

SDD does not specify Produced Artifacts for the MAINTAINING state. [Ref: §33.3]

#### 5.9.5 Lifecycle Mapping

MAINTAINING corresponds to the Maintenance phase of the Engineering Lifecycle (§12.2), governed by LC-4. [Ref: §33.2]

---

## 6. Transition Rules

### 6.1 Transition Preconditions

A transition **MUST NOT** occur unless all of the following hold: [Ref: §33.4, STA-1 through STA-5]

1. The source state's Exit Conditions are verified. [Ref: STA-2; §16; §27]
2. No INT (§40) violation blocks the transition. [Ref: STA-5; §40.2]
3. The transition is recorded as evidence with provenance. [Ref: STA-4; §28]

### 6.2 Transition Sequence

The canonical forward sequence is: [Ref: §33.2]

```
UNKNOWN → DISCOVERING → UNDERSTOOD → DOCUMENTED → PLANNED → IMPLEMENTING
→ VALIDATING → COMPLETED → MAINTAINING → ARCHIVED
```

Iteration (re-entry to a previously occupied state) is permitted per LC-3 and SG-3. [Ref: §12.3, LC-3; §13.3, SG-3] Re-entry **MUST** be recorded. [Ref: SG-3]

### 6.3 Transition Recording

Every transition **MUST** be recorded with: [Ref: STA-4]

- Source state and target state
- Verification evidence referencing the Exit Conditions of the source state
- Timestamp
- Traceability link to the Mission (§32) under which the transition occurred

SDD does not specify a transition recording template or schema. [Ref: §33.4, STA-4]

---

## 7. INT Violation Blocking

### 7.1 Blocking Scope

Any violation of an Engineering Integrity Rule (§40, INT-1 through INT-10) **MUST** block the transition out of the state in which the violation originated. [Ref: §33.4, STA-5; §40.2]

### 7.2 INT Rules Summary

The following integrity rules, when violated, block state transitions: [Ref: §40.1]

| ID | Rule | Blocks Transition From |
|---|---|---|
| **INT-1** | No undocumented implementation | IMPLEMENTING |
| **INT-2** | No undocumented decision | PLANNED |
| **INT-3** | No undocumented dependency | DISCOVERING, IMPLEMENTING |
| **INT-4** | No undocumented API | DISCOVERING, DOCUMENTED |
| **INT-5** | No undocumented database object | DISCOVERING, DOCUMENTED |
| **INT-6** | No undocumented configuration | DISCOVERING |
| **INT-7** | No undocumented workflow | DISCOVERING |
| **INT-8** | No undocumented security rule | DISCOVERING |
| **INT-9** | No undocumented assumption | All states |
| **INT-10** | No undocumented evidence | All states |

### 7.3 Resolution

INT rule violations **MAY** be waived only through governance (§17). [Ref: §40.2] An unresolved INT violation renders the affected work non-conformant (§16) and **MUST** block Repository Readiness (§41). [Ref: §40.2]

### 7.4 INT-to-Transition Binding

The binding between specific INT rules and the states they block is derived from: the INT rule's subject matter determines which state's produced artifacts it governs. SDD does not specify an explicit INT-to-state binding table. [Ref: §33.4, STA-5; §40] The table in §7.2 is a derived operational interpretation.

---

## 8. Completion Criteria

This document is complete when: [Ref: §27; §33.3]

1. All nine states are specified with their four mandatory elements (Entry Conditions, Exit Conditions, Required Evidence, Produced Artifacts). [Ref: §33.3, STA-3]
2. All Exit Conditions are mapped to the corresponding Completion-State criteria (§27). [Ref: §33.3]
3. All five normative rules (STA-1 through STA-5) are specified with citations. [Ref: §33.4]
4. State-to-lifecycle mapping is documented. [Ref: §33.2]
5. Transition rules, including INT violation blocking, are specified. [Ref: §33.4, STA-2, STA-4, STA-5]

**Note:** Detailed per-state criteria are deferred to Phase 5/6 per §27, CMP-5. Elements marked "SDD does not specify" in this document are architectural gaps that Phase 5/6 **SHALL** close. [Ref: §27, CMP-5; §33, Phase boundary note]
