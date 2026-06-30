# Governance Procedure

> **Authority Class:** Authoritative
> **SDD Authority:** §17.2, §17.1, §17.3
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 7

---

## 1. Purpose

This document defines the operational governance procedure for the Software Engineering Standard (SES). It instantiates the Governance Model architecture (§17) by specifying the governing premise, the seven normative governance rules (GV-1..GV-7), the change proposal procedure, the approval procedure, version management requirements, and role definitions. [Ref: §17]

Governance is the mechanism by which the standard itself is changed. Per PR-10 (controlled evolution), the standard **must** change only through governance and only on verified evidence; projects **must not** mutate the standard. [Ref: PR-10; §17]

---

## 2. Governing Premise (§17.1)

The standard is **superordinate** to projects. Projects conform to and provide feedback to the standard; **only verified engineering evidence may change the standard**. [Ref: §17.1; Mission Statement; §1.2]

This premise establishes a unidirectional authority flow: the standard governs projects; projects do not govern the standard. The feedback path (proposals with evidence) is the only sanctioned mechanism by which project experience influences the standard. [Ref: §17.1; GV-1; GV-2]

---

## 3. Normative Rules (GV-1..GV-7)

| ID | Rule | Evidence |
|---|---|---|
| **GV-1** | Projects **MUST NOT** modify the core standard. They **MAY** submit change proposals with evidence (feedback path). | [Ref: §17.2 GV-1; PR-10; Mission Statement] |
| **GV-2** | A change to the standard **MUST** originate as a proposal containing: the problem, the evidence, the proposed change, the impact on existing requirements, and the affected versions. | [Ref: §17.2 GV-2; converged practice — RFC process, IETF; ADR for the change itself] |
| **GV-3** | A change **MUST** be approved by the designated **Standard Authority** (STK-1) after **Inspection** (RV-2). | [Ref: §17.2 GV-3; IEEE 1028; §15] |
| **GV-4** | A change **MUST** be supported by evidence from the approved evidence base (Appendix A) or be explicitly marked UNSUPPORTED; unevidenced changes **MUST NOT** be accepted as normative. | [Ref: §17.2 GV-4; PR-1] |
| **GV-5** | Every accepted change **MUST** produce: a version increment (§18), a changelog entry, and an ADR recording the decision and its rationale. | [Ref: §17.2 GV-5; PR-5; Nygard; Keep a Changelog convention] |
| **GV-6** | The standard **MUST** maintain a single, identifiable **current authoritative version**; superseded versions are retained for history but are non-governing. | [Ref: §17.2 GV-6; PR-6; semantic versioning] |
| **GV-7** | Roles **MUST** be defined (at minimum: Standard Authority, Maintainer, Reviewer, Contributor/Project). Detailed RACI is a Phase-7 deliverable. | [Ref: §17.2 GV-7; converged practice — open-source governance models] |

---

## 4. Change Proposal Procedure

A change to the standard **MUST** originate as a proposal conforming to GV-2. The proposal procedure is:

**Step 1 — Problem statement.** The proposer **MUST** state the problem the change addresses, with evidence that the problem is real. [Ref: GV-2]

**Step 2 — Evidence base.** The proposer **MUST** cite evidence from the approved evidence base (Appendix A) or mark the proposal UNSUPPORTED per GV-4. [Ref: GV-4; PR-1]

**Step 3 — Proposed change.** The proposer **MUST** state the exact change to the standard, including: the text to be added, modified, or removed; the affected sections; and the authority class of any new artifacts. [Ref: GV-2]

**Step 4 — Impact analysis.** The proposer **MUST** analyze the impact on existing requirements: which requirements are affected, whether any are contradicted, and what compatibility consequences follow. [Ref: GV-2; §36]

**Step 5 — Affected versions.** The proposer **MUST** state which standard versions are affected and what version increment (MAJOR/MINOR/PATCH per §18) the change would require. [Ref: GV-2; §18]

**Step 6 — Submission.** The completed proposal **MUST** be submitted to the Standard Authority (STK-1) for review. [Ref: GV-3; STK-1]

Projects **MUST NOT** implement a change to the standard without proceeding through all six steps. [Ref: GV-1; GV-2]

---

## 5. Approval Procedure

A change proposal **MUST** undergo the following approval procedure:

**Step 1 — Reception.** The Standard Authority **MUST** acknowledge receipt of the proposal and assign it a tracking identifier. [Ref: GV-3]

**Step 2 — Inspection.** The proposal **MUST** undergo Inspection per RV-2 (the most rigorous review form). Inspection **MUST** be performed by qualified reviewers against explicit, written criteria. [Ref: GV-3; RV-2; RV-3]

**Step 3 — Evidence verification.** The Standard Authority **MUST** verify that the proposal's evidence is drawn from the approved evidence base (Appendix A) or is appropriately marked UNSUPPORTED per GV-4. [Ref: GV-4]

**Step 4 — Impact confirmation.** The Standard Authority **MUST** confirm the accuracy of the impact analysis (Step 4 of §4) and assess whether the proposed version increment is correct. [Ref: GV-2; §18]

**Step 5 — Decision.** The Standard Authority **MUST** render one of three verdicts: **Accepted**, **Rejected**, or **Deferred**. A Deferred proposal **MAY** be resubmitted when additional evidence becomes available. [Ref: GV-3; §35]

**Step 6 — Recording.** If Accepted, the Standard Authority **MUST** ensure GV-5 is satisfied: a version increment, a changelog entry, and an ADR **MUST** be produced before the change becomes effective. [Ref: GV-5]

A change **MUST NOT** be considered approved until all six steps are complete. [Ref: GV-3]

---

## 6. Version Management (§18)

Every accepted change **MUST** produce a version increment per the following rules. [Ref: GV-5; §18]

| Increment | Trigger | Conformance Impact |
|---|---|---|
| **MAJOR** | A normative change that can break existing project conformance (rule made stricter, requirement removed/redefined). | Projects **MAY** need rework to remain conformant. [Ref: §18.1] |
| **MINOR** | A backward-compatible addition (new optional rule, new guidance, new artifact type) that does not invalidate existing conformance. | Existing conformant projects remain conformant. [Ref: §18.1] |
| **PATCH** | Editorial/clarification/typo/evidence-citation fixes with no normative effect. | No conformance impact. [Ref: §18.1] |

Additional version management rules:

- **VS-1:** Every release **MUST** carry a unique semantic version. [Ref: §18.2 VS-1]
- **VS-2:** Every change **MUST** be recorded in a changelog. [Ref: §18.2 VS-2]
- **VS-3:** A conformance assertion **MUST** name the standard version it conforms to. [Ref: §18.2 VS-3]
- **VS-4:** A MAJOR change **MUST** include a migration note. [Ref: §18.2 VS-4]
- **VS-5:** Backward-incompatible changes **MUST NOT** be released as MINOR or PATCH. [Ref: §18.2 VS-5]

The standard **MUST** maintain a single identifiable current authoritative version per GV-6. Superseded versions are retained as Historical Knowledge (RKA-3) but are non-governing. [Ref: GV-6; §18; RKA-3]

---

## 7. Role Definitions

The four mandatory roles defined by GV-7 are specified operationally below. A detailed RACI matrix is provided in the companion document `roles-and-raci.md`. [Ref: GV-7]

### 7.1 Standard Authority

The **Standard Authority** is the stakeholder (STK-1) empowered to approve changes to the standard. [Ref: GV-3; STK-1; §17.2]

- **MUST** approve or reject all change proposals per GV-3.
- **MUST** ensure Inspection (RV-2) is performed before approval.
- **MAY** delegate review execution but **MUST NOT** delegate the approval decision.
- **MUST** ensure GV-5 is satisfied for every accepted change.

### 7.2 Maintainer

The **Maintainer** is responsible for the operational integrity of the standard repository and the execution of accepted changes. [Ref: §17.3; GV-7]

- **MUST** implement accepted changes in the repository.
- **MUST** ensure version increments (§18) and changelog entries are produced per GV-5.
- **MUST** maintain the repository structure per §10.
- **MAY** triage incoming proposals and route them to the Standard Authority.
- **MUST NOT** approve changes (reserved to Standard Authority per GV-3).

### 7.3 Reviewer

The **Reviewer** performs criteria-based examination of proposals and artifacts per the Review Model (§15). [Ref: GV-7; RV-4; §15]

- **MUST** perform Inspection per RV-2 for standard changes.
- **SHOULD** be independent of the proposal author per RV-4.
- **MUST** record review findings as evidence per RV-5.
- **MUST** review against explicit, written criteria per RV-3.

### 7.4 Contributor/Project

The **Contributor/Project** is any project or individual that uses the standard and may submit change proposals. [Ref: GV-7; GV-1]

- **MUST NOT** modify the core standard per GV-1.
- **MAY** submit change proposals with evidence per GV-1, GV-2.
- **MUST** conform to the current authoritative version per GV-6.
- **MAY** define extensions for their context per §19, provided extensions do not contradict the core.

---

## 8. Completion Criteria

This document is complete when:

1. The governing premise (§17.1) is stated (§2). [Ref: §17.1]
2. All seven governance rules (GV-1..GV-7) are stated and traceable to their SDD sources (§3). [Ref: §17.2]
3. The change proposal procedure is defined with explicit steps derived from GV-2 (§4). [Ref: GV-2]
4. The approval procedure is defined with explicit steps derived from GV-3 and RV-2 (§5). [Ref: GV-3; RV-2]
5. Version management rules are stated and linked to §18 (§6). [Ref: GV-5; §18]
6. All four mandatory roles are defined with responsibilities (§7). [Ref: GV-7]

---

*END OF DOCUMENT*
