# Object Schema Reference

> **Authority Class:** Authoritative
> **SDD Authority:** §43.2, §43.3, §42.2, §11.1, §11.2, §33, §18, §44, §26, §28, §35, §10, §48
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 4

## 1. Purpose

This document specifies the mandatory schema for every engineering object recognized by the Software Engineering Standard (SES). It generalizes the Artifact metadata model (§11.2) into a unified object model (§43) that applies to all instances of the canonical entities defined in the Engineering Meta-Model (§42). [Ref: §43.1]

Every engineering object MUST carry the fifteen fields defined herein. No engineering object MAY exist outside this model. [Ref: §43.3 OM-1, OM-2]

## 2. Scope

This document applies to all artifact instances, decision records, evidence items, knowledge objects, and every other engineering concept instantiated as a repository object under the SES. It defines the field schema only; storage layout is the deliverable of Phase 2, and templates are the deliverable of Phase 8. [Ref: §43, §11.4, §24 Phase 2/Phase 8]

This document does NOT define: per-field data types (SDD does not specify data types for object fields [Ref: §43.2]); storage serialization formats (Phase 2); templates for object instantiation (Phase 8); validation checklists (Phase 6).

## 3. Mandatory Fields (15)

The following fifteen fields SHALL be present on every engineering object. These fields are a superset of, and consistent with, §11.2 artifact metadata (artifacts are objects). [Ref: §43.3 OM-5]

| # | Field | Source Section |
|---|---|---|
| 1 | Object ID | §11.2 |
| 2 | Object Type | §42 |
| 3 | Authority Class | §11.1 |
| 4 | Owner | §11.2 |
| 5 | Lifecycle State | §33 |
| 6 | Status | §11.2 |
| 7 | Version | §18 |
| 8 | Parent Objects | §44 (contains/owns) |
| 9 | Child Objects | §44 |
| 10 | Incoming Relationships | §44 |
| 11 | Outgoing Relationships | §44 |
| 12 | Evidence References | §26, §28 |
| 13 | Decision References | §35 |
| 14 | Repository Location | §10 |
| 15 | Traceability Links | §48 |

## 4. Field Specifications

### 4.1 Object ID

**Definition:** A unique identifier that distinguishes the object from all other objects within the repository.

**Normative Properties:**
- The Object ID SHALL be unique within the scope of the repository. [Ref: §11.2]
- The Object ID SHALL be immutable for the lifetime of the object.
- SDD does not specify the format or syntax of the Object ID. [Ref: §43.2]

### 4.2 Object Type

**Definition:** The entity classification of the object, drawn from the canonical entity set.

**Normative Properties:**
- Object Type SHALL be one of the entities defined in §42.2. [Ref: §43.3 OM-3]
- Object Type MAY be: Mission, State, Stage, Operation, Artifact, Evidence, Observation, Fact, Knowledge, Decision, Requirement, Constraint, Review, Validation, Documentation, or Repository. [Ref: §42.2]
- The SES MAY introduce additional entity types only through governance (§17). [Ref: §42.3 MM-3]

### 4.3 Authority Class

**Definition:** The authority classification of the object, indicating its position in the single-source-of-truth hierarchy.

**Normative Properties:**
- Authority Class SHALL be exactly one of: Authoritative, Derived, or Generated. [Ref: §11.1; §43.3 OM-3]
- **Authoritative:** The single source of truth for some fact or decision; hand-authored; MAY be edited by humans through review and governance. [Ref: §11.1]
- **Derived:** Produced by transforming one or more authoritative artifacts; carries no independent truth; MUST NOT be hand-edited; MUST be regenerated from source. [Ref: §11.1]
- **Generated:** Mechanically produced from authoritative sources or from the subject under engineering; MUST NOT be hand-edited; MUST be reproducible. [Ref: §11.1]

### 4.4 Owner

**Definition:** The single accountable owner responsible for the object's lifecycle, accuracy, and governance.

**Normative Properties:**
- Each object has exactly one Owner. [Ref: §11.2; §43]
- The Owner SHALL be an identifiable role, person, or organizational unit.
- Ownership transfer SHALL be recorded as a traceable event. SDD does not specify the ownership transfer procedure. [Ref: §43.2]

### 4.5 Lifecycle State

**Definition:** The current state of the object within the engineering state machine.

**Normative Properties:**
- Lifecycle State SHALL be a valid state from §33. [Ref: §33; §43.2]
- Valid states are: UNKNOWN, DISCOVERING, UNDERSTOOD, DOCUMENTED, PLANNED, IMPLEMENTING, VALIDATING, COMPLETED, MAINTAINING, ARCHIVED. [Ref: §33.2]
- An object MUST be in exactly one Lifecycle State at a time. [Ref: §33 STA-1; §49 CON-7]

### 4.6 Status

**Definition:** The editorial status of the object within its governance lifecycle.

**Normative Properties:**
- Status SHALL be one of: Draft, Accepted, Superseded, or Deprecated. [Ref: §11.2; §43.2]
- **Draft:** Under development, not yet effective.
- **Accepted:** Reviewed, approved, and effective.
- **Superseded:** Replaced by a newer version; retained as Historical (RKA-3). [Ref: §35 DEC-3; §31 RKA-3]
- **Deprecated:** Marked obsolete, retained for traceability; non-governing. [Ref: §31 RKA-3]

### 4.7 Version

**Definition:** The semantic version of the object.

**Normative Properties:**
- Version SHALL conform to Semantic Versioning 2.0.0 semantics (MAJOR.MINOR.PATCH). [Ref: §18; §43.2]
- MAJOR: A normative change that can break existing conformance.
- MINOR: A backward-compatible addition.
- PATCH: Editorial/clarification/typo/evidence-citation fixes with no normative effect. [Ref: §18.1]
- Every version change SHALL be recorded in a changelog. [Ref: §18 VS-2]

### 4.8 Parent Objects

**Definition:** The set of objects that contain or own this object.

**Normative Properties:**
- Parent Objects SHALL reference objects via the contains or owns relationship types defined in §44. [Ref: §44.2 contains, owns]
- An object MAY have zero or more Parent Objects.
- The contains relationship is directed 1:n from container to member. [Ref: §44.2 contains]
- The owns relationship is directed 1:n from Owner to object; exactly one owner per object (CON-3). [Ref: §44.2 owns; §49 CON-3]

### 4.9 Child Objects

**Definition:** The set of objects that this object contains.

**Normative Properties:**
- Child Objects SHALL reference objects via the contains relationship type defined in §44. [Ref: §44.2 contains]
- An object MAY have zero or more Child Objects.
- The contains relationship is directed 1:n from container to member. [Ref: §44.2 contains]

### 4.10 Incoming Relationships

**Definition:** The set of directed edges pointing into this object from other objects.

**Normative Properties:**
- Incoming relationships SHALL be types from the Relationship Model (§44). [Ref: §43.3 OM-4]
- Valid incoming relationship types include: depends_on, produces, consumes, owns, implements, validates, documents, references, supersedes, derives_from, generated_from, verified_by, reviewed_by, approved_by, blocks, requires, contains, extends. [Ref: §44.2]
- Every relationship SHALL connect existing objects (no dangling endpoint) -- referential integrity. [Ref: §44 REL-2; §49 CON-4]

### 4.11 Outgoing Relationships

**Definition:** The set of directed edges pointing out of this object to other objects.

**Normative Properties:**
- Outgoing relationships SHALL be types from the Relationship Model (§44). [Ref: §43.3 OM-4]
- Valid outgoing relationship types are the same as for Incoming Relationships. [Ref: §44.2]
- Every relationship SHALL connect existing objects (no dangling endpoint). [Ref: §44 REL-2]

### 4.12 Evidence References

**Definition:** Provenance links to the evidence that justifies or supports this object.

**Normative Properties:**
- Evidence References SHALL link to provenance-bearing items as defined in §26 and §28. [Ref: §43.2; §26; §28]
- Every recorded fact MUST carry provenance (KN-1). [Ref: §14.3 KN-1]
- Evidence SHALL carry a confidence level (A--E) per §26. [Ref: §26 EVC-1]
- The Evidence Chain (§28) SHALL be preserved: each link justifies the downstream node by the upstream node. [Ref: §28 ECH-2]

### 4.13 Decision References

**Definition:** Links to the engineering decision(s) that authorize this object.

**Normative Properties:**
- Decision References SHALL link to Decision records as defined in §35. [Ref: §43.2; §35]
- Every implementation MUST trace back to exactly one engineering Decision (DEC-4). [Ref: §35 DEC-4; §40 INT-1]
- A Decision SHALL record: Decision; Decision Context; Alternatives; Evidence; Impact; Dependencies; Approval; Status; Superseded By. [Ref: §35.2]
- A Decision is immutable once Approved; change occurs only by a new Decision setting Superseded By. [Ref: §35 DEC-3]

### 4.14 Repository Location

**Definition:** The canonical location of the object within the repository structure.

**Normative Properties:**
- Repository Location SHALL identify the canonical path or address where the object resides. [Ref: §10; §43.2]
- The repository architecture separates: Normative Standard, Derived Operational Documents, Reference Material, Templates, and Examples. [Ref: §10.3]
- One fact SHALL have exactly one authoritative location (RA-3). [Ref: §10.3 RA-3]
- Derived/generated content MUST be reproducible from its authoritative source (RA-4). [Ref: §10.3 RA-4]

### 4.15 Traceability Links

**Definition:** Links connecting this object as a node in the Engineering Traceability Graph.

**Normative Properties:**
- Traceability Links SHALL conform to the Traceability Graph (§48). [Ref: §43.2; §48]
- Every engineering object MUST be a node in the traceability graph; no object MAY be orphaned (TGR-1). [Ref: §48 TGR-1; §49 CON-1]
- The graph SHALL support: Forward Trace, Backward Trace, Impact Trace, Dependency Trace, Evidence Trace, and Decision Trace. [Ref: §48.2]
- The traceability graph is built from Object nodes (§43) and Relationship edges (§44); it introduces no new node/edge types. [Ref: §48 TGR-3]

## 5. Normative Rules (OM-1..OM-6)

The following rules govern all engineering objects. Violation of any rule renders the affected object non-conformant. [Ref: §43.3]

| ID | Rule | Evidence |
|---|---|---|
| **OM-1** | Every engineering object **MUST** carry all fifteen fields (§43.2). No object MAY be instantiated with fewer than fifteen fields. | [Ref: §11.2 (superset); PR-5] |
| **OM-2** | No engineering object **MAY** exist outside this model. Every object in the repository SHALL be an instance of the §43 schema. | [Ref: Engineering Review Order; §42.3 MM-1] |
| **OM-3** | Object Type **MUST** be a §42.2 entity; Authority Class **MUST** be from §11.1. Invalid values for either field are non-conformant. | [Ref: §42; §11.1] |
| **OM-4** | Incoming/outgoing relationships **MUST** be Relationship Model (§44) types. Relationships outside §44.2 are non-conformant. | [Ref: §44] |
| **OM-5** | These fields are a **superset of, and consistent with,** §11.2 artifact metadata (artifacts are objects). The artifact metadata model is subsumed by this object model without contradiction. | [Ref: §11.2; NFR-11] |
| **OM-6** | Generated/Derived objects **MUST** remain reproducible (RA-4); their fields **MUST NOT** be hand-forged. The fields of a Generated or Derived object SHALL be produced by a documented, tool-agnostic procedure from an authoritative source. | [Ref: RA-4; PR-6] |

## 6. Entity Type Reference (§42.2)

The following entities from the Engineering Meta-Model (§42) are valid values for the Object Type field. [Ref: §42.2]

| Entity | Purpose | Authority Class | Defined in |
|---|---|---|---|
| **Mission** | Authorize and bound a task | Authoritative | §32 |
| **State** | Position in the engineering state machine | Authoritative | §33 |
| **Stage** | Gated unit of work | Authoritative | §13 |
| **Operation** | Defined engineering action | Authoritative | §34 |
| **Artifact** | Work product | Auth/Derived/Generated | §11 |
| **Evidence** | Justifying observation/result | Carries confidence | §26, §28 |
| **Observation** | Raw captured datum | Non-authoritative | §28 |
| **Fact** | Verified statement | Candidate-authoritative | §14, §26 |
| **Knowledge** | Synthesized understanding | Authoritative | §14, §31 |
| **Decision** | Recorded engineering choice | Authoritative (immutable) | §35 |
| **Requirement** | Stated obligation | Authoritative | §8, §9 |
| **Constraint** | Non-negotiable boundary | Authoritative | §23 |
| **Review** | Criteria-based examination | Authoritative record | §15 |
| **Validation** | Objective conformance check | Authoritative record | §16 |
| **Documentation** | Categorized recorded knowledge | Auth/Derived/Generated | §38 |
| **Repository** | Permanent engineering memory | Authoritative root store | §10, §31 |

Every engineering concept in the standard MUST be an instance of a §42.2 entity (MM-1). [Ref: §42.3 MM-1] The meta-model is authoritative; later specifications MUST derive from it and MUST NOT introduce entities outside §42.2 without governance (§17). [Ref: §42.3 MM-3]

## 7. Completion Criteria

This document is complete when:

1. All fifteen mandatory fields are specified with normative properties (§3, §4). [Ref: §43.2]
2. All six normative rules OM-1 through OM-6 are stated (§5). [Ref: §43.3]
3. The entity type reference from §42.2 is reproduced (§6). [Ref: §42.2]
4. Every field specification cites its SDD authority.
5. All fields use RFC 2119 keywords (MUST, SHALL, MAY, SHOULD) per §46. [Ref: §46]
