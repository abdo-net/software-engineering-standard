# Roles and RACI

> **Authority Class:** Authoritative
> **SDD Authority:** §17.2 GV-7
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 7

---

## 1. Purpose

This document defines the four mandatory governance roles specified by GV-7 and provides a RACI matrix mapping those roles to standard activities. It is the Phase-7 deliverable mandated by GV-7: "Roles MUST be defined (at minimum: Standard Authority, Maintainer, Reviewer, Contributor/Project). Detailed RACI is a Phase-7 deliverable." [Ref: §17.2 GV-7]

A RACI matrix assigns one of four accountability designations to each role-activity intersection: **R** (Responsible — does the work), **A** (Accountable — ultimately answerable), **C** (Consulted — provides input), **I** (Informed — notified of outcome). [Ref: Converged practice — RACI project-management discipline]

---

## 2. Role Definitions

### 2.1 Standard Authority

| Field | Value |
|---|---|
| **SDD Source** | GV-3, STK-1 |
| **Definition** | The stakeholder (STK-1) empowered to approve changes to the standard. |
| **Primary Concerns** | Authority, durability, evidence basis, governance integrity. [Ref: STK-1] |

**Normative responsibilities:**

- **MUST** approve or reject all change proposals per GV-3. [Ref: §17.2 GV-3]
- **MUST** ensure Inspection (RV-2) is performed before approving any change to the standard. [Ref: §17.2 GV-3; §15 RV-2]
- **MAY** delegate review execution but **MUST NOT** delegate the approval decision. [Ref: §17.2 GV-3]
- **MUST** ensure GV-5 is satisfied for every accepted change (version increment, changelog entry, ADR). [Ref: §17.2 GV-5]
- **MUST** maintain a single current authoritative version per GV-6. [Ref: §17.2 GV-6]

### 2.2 Maintainer

| Field | Value |
|---|---|
| **SDD Source** | §17.3, GV-7 |
| **Definition** | The role responsible for operational integrity of the standard repository and execution of accepted changes. |
| **Primary Concerns** | Controlled evolution, backward compatibility, change provenance. [Ref: STK-6] |

**Normative responsibilities:**

- **MUST** implement accepted changes in the repository. [Ref: §17.3]
- **MUST** ensure version increments (§18) and changelog entries are produced per GV-5. [Ref: §17.2 GV-5; §18]
- **MUST** maintain the repository structure per §10. [Ref: §10]
- **MAY** triage incoming proposals and route them to the Standard Authority. [Ref: §17.3]
- **MUST NOT** approve changes (reserved to Standard Authority per GV-3). [Ref: §17.2 GV-3]

### 2.3 Reviewer

| Field | Value |
|---|---|
| **SDD Source** | RV-4, §15 |
| **Definition** | A qualified individual who performs criteria-based examination of proposals and artifacts per the Review Model (§15). |
| **Primary Concerns** | Objective conformance criteria, traceability, review process. [Ref: STK-4] |

**Normative responsibilities:**

- **MUST** perform Inspection per RV-2 for changes to the standard itself. [Ref: §15 RV-2; §17.2 GV-3]
- **SHOULD** be independent of the proposal author where independence adds value per RV-4. [Ref: §15 RV-4]
- **MUST** review against explicit, written criteria per RV-3. [Ref: §15 RV-3]
- **MUST** record review findings (findings, disposition) as evidence per RV-5. [Ref: §15 RV-5]
- **MUST NOT** both author and solely review the same artifact where separation of duties adds value. [Ref: §15 RV-4; PR-8]

### 2.4 Contributor/Project

| Field | Value |
|---|---|
| **SDD Source** | GV-1, GV-7 |
| **Definition** | Any project or individual that uses the standard and may submit change proposals through the feedback path. |
| **Primary Concerns** | Extensibility for their context without forking the standard. [Ref: STK-5] |

**Normative responsibilities:**

- **MUST NOT** modify the core standard per GV-1. [Ref: §17.2 GV-1]
- **MAY** submit change proposals with evidence per GV-1. [Ref: §17.2 GV-1]
- **MUST** conform to the current authoritative version per GV-6. [Ref: §17.2 GV-6]
- **MAY** define extensions for their context per §19, provided extensions do not contradict the core. [Ref: §19 EX-1 through EX-6]
- **MUST** submit proposals containing problem, evidence, proposed change, impact analysis, and affected versions per GV-2. [Ref: §17.2 GV-2]

---

## 3. RACI Matrix

### 3.1 Governance Activities

| Activity | Standard Authority | Maintainer | Reviewer | Contributor/Project |
|---|---|---|---|---|
| Submit change proposal | I | I | I | R/A |
| Triage incoming proposal | C | R/A | C | I |
| Perform Inspection (RV-2) on proposal | A | C | R | I |
| Approve/reject change proposal | R/A | C | C | I |
| Implement accepted change | I | R/A | C | I |
| Produce version increment | A | R | I | I |
| Produce changelog entry | A | R | I | I |
| Produce ADR for change | A | R | C | I |
| Maintain repository structure | I | R/A | I | I |
| Enforce single current version | R/A | R | I | I |
| Define extensions (per §19) | I | I | I | R/A |

### 3.2 Review Activities

| Activity | Standard Authority | Maintainer | Reviewer | Contributor/Project |
|---|---|---|---|---|
| Define review criteria (checklists) | A | R | C | I |
| Perform Inspection of standard changes | A | C | R | I |
| Perform Technical Review | C | I | R/A | I |
| Perform Audit | A | C | R | I |
| Record review findings | I | I | R/A | I |

### 3.3 Version Management Activities

| Activity | Standard Authority | Maintainer | Reviewer | Contributor/Project |
|---|---|---|---|---|
| Decide version increment (MAJOR/MINOR/PATCH) | R/A | C | C | I |
| Execute version increment | I | R/A | I | I |
| Author migration note (MAJOR) | C | R | C | I |
| Retain superseded versions | I | R/A | I | I |

### 3.4 Standard Evolution Activities

| Activity | Standard Authority | Maintainer | Reviewer | Contributor/Project |
|---|---|---|---|---|
| Propose new rule / amendment | C | C | C | R/A |
| Propose new entity (§42.2) | C | C | C | R/A |
| Verify evidence base citation | C | I | R | I |
| Verify no contradiction (NFR-11) | C | I | R | I |
| Govern term addition (§46) | R/A | R | C | I |

---

## 4. Completion Criteria

This document is complete when:

1. All four mandatory roles are defined with responsibilities traceable to SDD sources (§2). [Ref: GV-7]
2. Each role's normative responsibilities cite the governing SDD sections. [Ref: GV-7]
3. A RACI matrix maps all four roles to standard activities across governance, review, version management, and standard evolution (§3). [Ref: GV-7 "Detailed RACI is a Phase-7 deliverable"]
4. No role is assigned both accountability (A) and sole responsibility (R) for the same activity where separation of duties (PR-8) applies. [Ref: PR-8]

---

*END OF DOCUMENT*
