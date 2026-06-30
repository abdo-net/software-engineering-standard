# Discovery Specification

> **Authority Class:** Authoritative
> **SDD Authority:** §25
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 3

## 1. Purpose

This document specifies the **Engineering Discovery Model** mandated by §25. It defines the detailed specification of each discovery activity: Purpose, Inputs, Activities, Outputs, Evidence Produced, Verification, Tools, Mistakes, and References. [Ref: §25.1]

Discovery realizes the **Understanding** and **Reverse Engineering / Reconstruction** phases of the Engineering Lifecycle (§12.2) at the architectural level, and feeds the Knowledge Model (§14), the Evidence Confidence Model (§26), the Engineering Evidence Chain (§28), and the Repository Knowledge Architecture (§31). [Ref: §25.1]

Discovery is a **goal-directed, iterative, evidence-producing** transformation from an unknown system to a verified understanding. Full comprehension is not the objective; sufficiency for the mission is. [Ref: §25.2]

The detailed specification of each discovery activity is the deliverable of **Phase 3 (lifecycle)** and **Phase 5 (stages)**. [Ref: §25.1]

## 2. Discovery Model

Discovery is organized into evidence layers. Layers are **dependency-ordered, not strictly sequential** (LC-3). [Ref: §25.2; §12.3 LC-3]

```
UNKNOWN SYSTEM
  |
  |- Inventory Layer   : Asset . Repository . Technology . Build-System . Runtime-Environment detection
  |- Structure Layer   : Dependency . Module . API . Database . Configuration discovery
  |- Security Layer    : Security . Authentication . Authorization discovery
  |- Behavior Layer    : Event . Workflow . Execution-Flow Recovery . Runtime Observation
  |
  |- Analysis Methods  : Static Analysis . Dynamic Analysis . Cross-Validation (triangulation)
  |- Synthesis         : Architecture Recovery . Knowledge Extraction . Evidence Collection
  |- Output            : Documentation . Verification  ->  DISCOVERY COMPLETE (§27)
```

The flow is: Inventory -> Structure -> Security -> Behavior, supported by Analysis Methods, producing Synthesis, leading to Output. [Ref: §25.2]

## 3. Normative Rules

### DSC-1 — Discovery Before Modification
An unknown system SHALL pass through Discovery before any modification. [Ref: §25.4 DSC-1; Chikofsky & Cross 1990; Feathers 2004]

### DSC-2 — Provenance and Confidence
Every discovery output MUST carry provenance (KN-1) and a confidence level (§26). [Ref: §25.4 DSC-2; PR-5; §26]

### DSC-3 — Static, Dynamic, and Cross-Validation
Discovery MUST combine static and dynamic analysis and cross-validate (triangulate); disagreements MUST be recorded, not silently resolved. [Ref: §25.4 DSC-3; Demeyer et al. 2002]

### DSC-4 — Goal-Directed and Iterative
Discovery is goal-directed and iterative; complete comprehension is NOT required — only sufficiency for the mission. [Ref: §25.4 DSC-4; Lehman's Laws; Demeyer 2002]

### DSC-5 — Completion Criteria
Discovery is complete only when the "Discovery Complete" criteria (§27) are objectively met. [Ref: §25.4 DSC-5; §27; IEEE 1028 exit criteria]

### DSC-6 — Confidence Not Exceeding Evidence
No discovery conclusion MAY assert confidence exceeding its evidence (§26). [Ref: §25.4 DSC-6; PR-1; PR-5]

## 4. Discovery Activities

---

### 4.1 Asset Inventory

#### 4.1.1 Purpose
Identify and catalog all assets belonging to the unknown system. [Ref: §25.2 Inventory Layer]

#### 4.1.2 Inputs
The SDD does not specify explicit inputs for this activity. [Ref: §25.2]

#### 4.1.3 Activities
- Detect and catalog assets comprising or related to the unknown system.
- Assign provenance and confidence level (§26) to each inventoried asset. [Ref: §25.4 DSC-2]

#### 4.1.4 Outputs
- Asset inventory list: a catalog of all detected assets, each with provenance and confidence classification. [Ref: §25.2; §25.4 DSC-2]

#### 4.1.5 Evidence Produced
Each asset record MUST carry provenance (KN-1) and a confidence level (§26). [Ref: §25.4 DSC-2]

#### 4.1.6 Verification
Asset inventory outputs MUST be verified against the Evidence Chain (§28): observation -> evidence -> verification -> fact. [Ref: §28.2; ECH-1]

#### 4.1.7 Tools
The SDD does not specify tools for this activity. [Ref: §25]

#### 4.1.8 Mistakes
- Recording assets without provenance or confidence (DSC-2). [Ref: §25.4 DSC-2]
- Asserting asset inventory completeness beyond the evidence (DSC-6). [Ref: §25.4 DSC-6]

#### 4.1.9 References
- §25.2 Inventory Layer
- §26 Evidence Confidence Model
- §28 Engineering Evidence Chain
- §31 Repository Knowledge Architecture

---

### 4.2 Repository Inventory

#### 4.2.1 Purpose
Identify and catalog the repositories (version-controlled stores) that contain the unknown system's artifacts. [Ref: §25.2 Inventory Layer]

#### 4.2.2 Inputs
The SDD does not specify explicit inputs for this activity. [Ref: §25.2]

#### 4.2.3 Activities
- Detect and catalog version-controlled repositories containing system artifacts.
- Record repository locations, types, and ownership.
- Assign provenance and confidence level (§26) to each repository record. [Ref: §25.4 DSC-2]

#### 4.2.4 Outputs
- Repository inventory: a catalog of all detected repositories, each with provenance and confidence classification. [Ref: §25.2; §25.4 DSC-2]

#### 4.2.5 Evidence Produced
Each repository record MUST carry provenance (KN-1) and a confidence level (§26). [Ref: §25.4 DSC-2]

#### 4.2.6 Verification
Repository inventory outputs MUST be verified against the Evidence Chain (§28). [Ref: §28.2; ECH-1]

#### 4.2.7 Tools
The SDD does not specify tools for this activity. [Ref: §25]

#### 4.2.8 Mistakes
- Recording repositories without provenance or confidence (DSC-2). [Ref: §25.4 DSC-2]
- Missing repositories due to insufficient detection scope (DSC-4: sufficiency for mission). [Ref: §25.4 DSC-4]

#### 4.2.9 References
- §25.2 Inventory Layer
- §26 Evidence Confidence Model
- §28 Engineering Evidence Chain

---

### 4.3 Technology Detection

#### 4.3.1 Purpose
Detect the technologies (programming languages, frameworks, libraries, platforms) used by the unknown system. [Ref: §25.2 Inventory Layer]

#### 4.3.2 Inputs
- Asset inventory outputs (§4.1). [Ref: §25.2 Inventory Layer]
- Repository inventory outputs (§4.2). [Ref: §25.2 Inventory Layer]

#### 4.3.3 Activities
- Detect technologies from source artifacts, build files, configuration, and runtime evidence.
- Cross-validate technology detections between static and dynamic sources where possible (DSC-3). [Ref: §25.4 DSC-3]
- Assign provenance and confidence level (§26) to each technology detection. [Ref: §25.4 DSC-2]

#### 4.3.4 Outputs
- Technology inventory: a catalog of detected technologies, each with provenance and confidence classification. [Ref: §25.2; §25.4 DSC-2]

#### 4.3.5 Evidence Produced
Each technology record MUST carry provenance (KN-1) and a confidence level (§26). [Ref: §25.4 DSC-2]

#### 4.3.6 Verification
Technology detection outputs MUST be verified through cross-validation (triangulation) where feasible (KN-6). [Ref: §14.3 KN-6; §25.4 DSC-3]

#### 4.3.7 Tools
The SDD does not specify tools for this activity. Tool selection is out of core scope (CN-1). [Ref: CN-1]

#### 4.3.8 Mistakes
- Detecting technologies without provenance or confidence (DSC-2). [Ref: §25.4 DSC-2]
- Relying on a single detection source without cross-validation (DSC-3). [Ref: §25.4 DSC-3]
- Treating inferred technologies as directly observed (DSC-6: confidence must not exceed evidence). [Ref: §25.4 DSC-6]

#### 4.3.9 References
- §25.2 Inventory Layer
- §14.3 KN-6
- §25.4 DSC-2, DSC-3, DSC-6
- §26 Evidence Confidence Model

---

### 4.4 Build System Detection

#### 4.4.1 Purpose
Detect and document the build systems used to compile, package, and deploy the unknown system. [Ref: §25.2 Inventory Layer]

#### 4.4.2 Inputs
- Asset inventory (§4.1). [Ref: §25.2]
- Repository inventory (§4.2). [Ref: §25.2]
- Technology detection outputs (§4.3). [Ref: §25.2]

#### 4.4.3 Activities
- Detect build configuration files, scripts, pipelines, and tooling.
- Document build steps, dependencies, and artifacts produced.
- Assign provenance and confidence level (§26). [Ref: §25.4 DSC-2]

#### 4.4.4 Outputs
- Build system specification: detected build systems with their configurations, provenance, and confidence classification. [Ref: §25.2; §25.4 DSC-2]

#### 4.4.5 Evidence Produced
Build system records MUST carry provenance (KN-1) and a confidence level (§26). [Ref: §25.4 DSC-2]

#### 4.4.6 Verification
Build system detection MUST be verified against the Evidence Chain (§28). [Ref: §28.2; ECH-1]

#### 4.4.7 Tools
The SDD does not specify tools for this activity. [Ref: §25]

#### 4.4.8 Mistakes
- Recording build systems without provenance (DSC-2). [Ref: §25.4 DSC-2]
- Missing build pipeline stages (DSC-4: sufficiency for mission). [Ref: §25.4 DSC-4]

#### 4.4.9 References
- §25.2 Inventory Layer
- §25.4 DSC-2, DSC-4
- §28 Engineering Evidence Chain

---

### 4.5 Runtime Environment Detection

#### 4.5.1 Purpose
Detect and document the runtime environments in which the unknown system executes. [Ref: §25.2 Inventory Layer]

#### 4.5.2 Inputs
- Asset inventory (§4.1). [Ref: §25.2]
- Technology detection outputs (§4.3). [Ref: §25.2]

#### 4.5.3 Activities
- Detect runtime platforms, containers, orchestrators, operating systems, and infrastructure.
- Document runtime dependencies and constraints.
- Assign provenance and confidence level (§26). [Ref: §25.4 DSC-2]

#### 4.5.4 Outputs
- Runtime environment specification: detected environments with provenance and confidence classification. [Ref: §25.2; §25.4 DSC-2]

#### 4.5.5 Evidence Produced
Runtime environment records MUST carry provenance (KN-1) and a confidence level (§26). [Ref: §25.4 DSC-2]

#### 4.5.6 Verification
Runtime environment detection MUST be verified against the Evidence Chain (§28). [Ref: §28.2; ECH-1]

#### 4.5.7 Tools
The SDD does not specify tools for this activity. [Ref: §25]

#### 4.5.8 Mistakes
- Recording runtime environments without provenance (DSC-2). [Ref: §25.4 DSC-2]
- Confusing development environments with production runtime (DSC-3: disagreements must be recorded). [Ref: §25.4 DSC-3]

#### 4.5.9 References
- §25.2 Inventory Layer
- §25.4 DSC-2, DSC-3
- §28 Engineering Evidence Chain

---

### 4.6 Dependency Discovery

#### 4.6.1 Purpose
Discover and document all dependencies of the unknown system: internal modules, external libraries, services, and data stores. [Ref: §25.2 Structure Layer]

#### 4.6.2 Inputs
- Asset inventory (§4.1). [Ref: §25.2]
- Technology detection (§4.3). [Ref: §25.2]
- Build system detection (§4.4). [Ref: §25.2]

#### 4.6.3 Activities
- Discover dependencies from build files, import statements, package manifests, configuration, and runtime behavior.
- Map dependency direction and coupling strength.
- Cross-validate static dependency declarations against runtime behavior (DSC-3). [Ref: §25.4 DSC-3]
- Assign provenance and confidence level (§26). [Ref: §25.4 DSC-2]

#### 4.6.4 Outputs
- Dependency map: a complete inventory of dependencies, each with direction, coupling, provenance, and confidence. [Ref: §25.2; §25.4 DSC-2]

#### 4.6.5 Evidence Produced
Dependency records MUST carry provenance (KN-1) and confidence (§26). Every dependency MUST be discovered and recorded (INT-3). [Ref: §25.4 DSC-2; §40.1 INT-3]

#### 4.6.6 Verification
Dependency discovery outputs MUST be verified through cross-validation between static declarations and runtime observation (DSC-3). [Ref: §25.4 DSC-3] Dependencies MUST be validated against the Evidence Chain (§28). [Ref: §28.2]

#### 4.6.7 Tools
The SDD does not specify tools for this activity. [Ref: §25]

#### 4.6.8 Mistakes
- Missing undocumented dependencies (DSC-4: sufficiency depends on mission scope). [Ref: §25.4 DSC-4]
- Recording dependencies without provenance (DSC-2). [Ref: §25.4 DSC-2]
- Silently resolving disagreements between declared and actual dependencies (DSC-3). [Ref: §25.4 DSC-3]
- Failing to record dependencies (INT-3 violation). [Ref: §40.1 INT-3]

#### 4.6.9 References
- §25.2 Structure Layer
- §25.4 DSC-2, DSC-3, DSC-4
- §26 Evidence Confidence Model
- §28 Engineering Evidence Chain
- §40.1 INT-3

---

### 4.7 Module Discovery

#### 4.7.1 Purpose
Discover and document the modules (cohesive units of code/data) comprising the unknown system. [Ref: §25.2 Structure Layer]

#### 4.7.2 Inputs
- Dependency discovery outputs (§4.6). [Ref: §25.2]
- Technology detection outputs (§4.3). [Ref: §25.2]
- Repository inventory (§4.2). [Ref: §25.2]

#### 4.7.3 Activities
- Discover module boundaries from source structure, build artifacts, and runtime organization.
- Document module responsibilities, interfaces, and internal structure.
- Assign provenance and confidence level (§26). [Ref: §25.4 DSC-2]

#### 4.7.4 Outputs
- Module catalog: discovered modules with boundaries, responsibilities, interfaces, provenance, and confidence. [Ref: §25.2; §25.4 DSC-2]

#### 4.7.5 Evidence Produced
Module records MUST carry provenance (KN-1) and confidence (§26). [Ref: §25.4 DSC-2]

#### 4.7.6 Verification
Module discovery outputs MUST be verified against the Evidence Chain (§28). [Ref: §28.2; ECH-1]

#### 4.7.7 Tools
The SDD does not specify tools for this activity. [Ref: §25]

#### 4.7.8 Mistakes
- Recording modules without provenance (DSC-2). [Ref: §25.4 DSC-2]
- Inventing module boundaries without evidence from the source system (DSC-6). [Ref: §25.4 DSC-6]

#### 4.7.9 References
- §25.2 Structure Layer
- §25.4 DSC-2, DSC-6
- §28 Engineering Evidence Chain

---

### 4.8 API Discovery

#### 4.8.1 Purpose
Discover and document all APIs (application programming interfaces) exposed or consumed by the unknown system. [Ref: §25.2 Structure Layer]

#### 4.8.2 Inputs
- Module discovery outputs (§4.7). [Ref: §25.2]
- Technology detection outputs (§4.3). [Ref: §25.2]
- Static analysis outputs (§4.18). [Ref: §25.2 Analysis Methods]
- Dynamic analysis outputs (§4.19). [Ref: §25.2 Analysis Methods]

#### 4.8.3 Activities
- Discover API endpoints, protocols, request/response schemas, and authentication requirements.
- Document API contracts (agreed interfaces + semantics across boundaries per §11.3). [Ref: §11.3]
- Cross-validate static API declarations against runtime behavior (DSC-3). [Ref: §25.4 DSC-3]
- Assign provenance and confidence level (§26). [Ref: §25.4 DSC-2]

#### 4.8.4 Outputs
- API inventory: discovered APIs with contracts, provenance, and confidence classification. [Ref: §25.2; §25.4 DSC-2]
- Contract specifications where APIs are confirmed (§11.3). [Ref: §11.3]

#### 4.8.5 Evidence Produced
API records MUST carry provenance (KN-1) and confidence (§26). Every API MUST have a contract (INT-4). [Ref: §25.4 DSC-2; §40.1 INT-4]

#### 4.8.6 Verification
API discovery outputs MUST be verified through cross-validation between static declarations and runtime observation (DSC-3). Comparison results MUST be assigned a confidence level (§26). [Ref: §25.4 DSC-3; §37.3 CPM-2]

#### 4.8.7 Tools
The SDD does not specify tools for this activity. [Ref: §25]

#### 4.8.8 Mistakes
- Recording APIs without provenance (DSC-2). [Ref: §25.4 DSC-2]
- Failing to document discovered APIs (INT-4 violation). [Ref: §40.1 INT-4]
- Presenting inferred API contracts as confirmed without verification (DSC-6). [Ref: §25.4 DSC-6]

#### 4.8.9 References
- §25.2 Structure Layer
- §11.3 Contract Specification
- §25.4 DSC-2, DSC-3, DSC-6
- §26 Evidence Confidence Model
- §37.3 CPM-2
- §40.1 INT-4

---

### 4.9 Database Discovery

#### 4.9.1 Purpose
Discover and document all databases, schemas, tables, and data stores used by the unknown system. [Ref: §25.2 Structure Layer]

#### 4.9.2 Inputs
- Technology detection outputs (§4.3). [Ref: §25.2]
- Dependency discovery outputs (§4.6). [Ref: §25.2]
- Static analysis outputs (§4.18). [Ref: §25.2]
- Dynamic analysis outputs (§4.19). [Ref: §25.2]

#### 4.9.3 Activities
- Discover database connections, schemas, tables, columns, indexes, and relationships.
- Document ORM mappings and data access patterns.
- Cross-validate schema declarations against runtime database state (DSC-3). [Ref: §25.4 DSC-3]
- Assign provenance and confidence level (§26). [Ref: §25.4 DSC-2]

#### 4.9.4 Outputs
- Database inventory: discovered databases and schemas with provenance and confidence classification. [Ref: §25.2; §25.4 DSC-2]

#### 4.9.5 Evidence Produced
Database records MUST carry provenance (KN-1) and confidence (§26). Every database object MUST be documented (INT-5). [Ref: §25.4 DSC-2; §40.1 INT-5]

#### 4.9.6 Verification
Database discovery outputs MUST be verified through cross-validation between ORM definitions and runtime schema (DSC-3). Comparison results MUST be assigned a confidence level (§26). [Ref: §25.4 DSC-3; §37.2 (Database vs ORM comparison)]

#### 4.9.7 Tools
The SDD does not specify tools for this activity. [Ref: §25]

#### 4.9.8 Mistakes
- Recording database objects without provenance (DSC-2). [Ref: §25.4 DSC-2]
- Failing to document database objects (INT-5 violation). [Ref: §40.1 INT-5]
- Relying solely on ORM definitions without verifying against actual database schema (DSC-3). [Ref: §25.4 DSC-3]

#### 4.9.9 References
- §25.2 Structure Layer
- §25.4 DSC-2, DSC-3
- §26 Evidence Confidence Model
- §37.2 (Database vs ORM comparison)
- §40.1 INT-5

---

### 4.10 Configuration Discovery

#### 4.10.1 Purpose
Discover and document all configuration parameters, files, and sources for the unknown system. [Ref: §25.2 Structure Layer]

#### 4.10.2 Inputs
- Asset inventory (§4.1). [Ref: §25.2]
- Technology detection (§4.3). [Ref: §25.2]
- Build system detection (§4.4). [Ref: §25.2]
- Runtime environment detection (§4.5). [Ref: §25.2]

#### 4.10.3 Activities
- Discover configuration files, environment variables, feature flags, and configuration sources.
- Document configuration defaults, overrides, and runtime values.
- Cross-validate configuration files against runtime values (DSC-3). [Ref: §25.4 DSC-3]
- Assign provenance and confidence level (§26). [Ref: §25.4 DSC-2]

#### 4.10.4 Outputs
- Configuration inventory: discovered configuration with sources, values, provenance, and confidence. [Ref: §25.2; §25.4 DSC-2]

#### 4.10.5 Evidence Produced
Configuration records MUST carry provenance (KN-1) and confidence (§26). Every configuration MUST be documented (INT-6). [Ref: §25.4 DSC-2; §40.1 INT-6]

#### 4.10.6 Verification
Configuration discovery outputs MUST be verified through cross-validation between declared and runtime configuration (DSC-3; §37.2 Configuration vs Runtime comparison). [Ref: §25.4 DSC-3; §37.2]

#### 4.10.7 Tools
The SDD does not specify tools for this activity. [Ref: §25]

#### 4.10.8 Mistakes
- Recording configuration without provenance (DSC-2). [Ref: §25.4 DSC-2]
- Failing to document configuration (INT-6 violation). [Ref: §40.1 INT-6]
- Missing runtime configuration overrides (DSC-4: sufficiency for mission). [Ref: §25.4 DSC-4]

#### 4.10.9 References
- §25.2 Structure Layer
- §25.4 DSC-2, DSC-3, DSC-4
- §26 Evidence Confidence Model
- §37.2 (Configuration vs Runtime comparison)
- §40.1 INT-6

---

### 4.11 Security Discovery

#### 4.11.1 Purpose
Discover and document the security posture, controls, and vulnerabilities of the unknown system. [Ref: §25.2 Security Layer]

#### 4.11.2 Inputs
- Asset inventory (§4.1). [Ref: §25.2]
- Technology detection (§4.3). [Ref: §25.2]
- Dependency discovery (§4.6). [Ref: §25.2]
- API discovery (§4.8). [Ref: §25.2]

#### 4.11.3 Activities
- Discover security controls, encryption usage, input validation, output encoding, and vulnerability exposure.
- Document security rules and constraints.
- Cross-validate static security configuration against runtime behavior (DSC-3). [Ref: §25.4 DSC-3]
- Assign provenance and confidence level (§26). [Ref: §25.4 DSC-2]

#### 4.11.4 Outputs
- Security inventory: discovered security controls and findings with provenance and confidence. [Ref: §25.2; §25.4 DSC-2]

#### 4.11.5 Evidence Produced
Security records MUST carry provenance (KN-1) and confidence (§26). Every security rule MUST be documented (INT-8). [Ref: §25.4 DSC-2; §40.1 INT-8]

#### 4.11.6 Verification
Security discovery outputs MUST be verified through cross-validation between static configuration and runtime observation (DSC-3). [Ref: §25.4 DSC-3]

#### 4.11.7 Tools
The SDD does not specify tools for this activity. [Ref: §25]

#### 4.11.8 Mistakes
- Recording security findings without provenance (DSC-2). [Ref: §25.4 DSC-2]
- Failing to document security rules (INT-8 violation). [Ref: §40.1 INT-8]
- Asserting security posture confidence beyond evidence (DSC-6). [Ref: §25.4 DSC-6]

#### 4.11.9 References
- §25.2 Security Layer
- §25.4 DSC-2, DSC-3, DSC-6
- §26 Evidence Confidence Model
- §40.1 INT-8

---

### 4.12 Authentication Discovery

#### 4.12.1 Purpose
Discover and document the authentication mechanisms used by the unknown system. [Ref: §25.2 Security Layer]

#### 4.12.2 Inputs
- Security discovery outputs (§4.11). [Ref: §25.2]
- API discovery outputs (§4.8). [Ref: §25.2]
- Runtime observation outputs (§4.17). [Ref: §25.2]

#### 4.12.3 Activities
- Discover authentication schemes, identity providers, credential stores, and session management.
- Document authentication flows and trust boundaries.
- Cross-validate static authentication configuration against runtime behavior (DSC-3). [Ref: §25.4 DSC-3]
- Assign provenance and confidence level (§26). [Ref: §25.4 DSC-2]

#### 4.12.4 Outputs
- Authentication specification: discovered authentication mechanisms with provenance and confidence. [Ref: §25.2; §25.4 DSC-2]

#### 4.12.5 Evidence Produced
Authentication records MUST carry provenance (KN-1) and confidence (§26). [Ref: §25.4 DSC-2]

#### 4.12.6 Verification
Authentication discovery outputs MUST be verified through cross-validation (DSC-3). [Ref: §25.4 DSC-3]

#### 4.12.7 Tools
The SDD does not specify tools for this activity. [Ref: §25]

#### 4.12.8 Mistakes
- Recording authentication mechanisms without provenance (DSC-2). [Ref: §25.4 DSC-2]
- Inferring authentication flows without runtime verification (DSC-6). [Ref: §25.4 DSC-6]

#### 4.12.9 References
- §25.2 Security Layer
- §25.4 DSC-2, DSC-3, DSC-6
- §26 Evidence Confidence Model

---

### 4.13 Authorization Discovery

#### 4.13.1 Purpose
Discover and document the authorization (access control) mechanisms used by the unknown system. [Ref: §25.2 Security Layer]

#### 4.13.2 Inputs
- Security discovery outputs (§4.11). [Ref: §25.2]
- Authentication discovery outputs (§4.12). [Ref: §25.2]
- API discovery outputs (§4.8). [Ref: §25.2]

#### 4.13.3 Activities
- Discover authorization models (RBAC, ABAC, ACL, etc.), permission matrices, and access control enforcement points.
- Document authorization rules and policy definitions.
- Cross-validate static authorization configuration against runtime enforcement (DSC-3). [Ref: §25.4 DSC-3]
- Assign provenance and confidence level (§26). [Ref: §25.4 DSC-2]

#### 4.13.4 Outputs
- Authorization specification: discovered authorization mechanisms with provenance and confidence. [Ref: §25.2; §25.4 DSC-2]

#### 4.13.5 Evidence Produced
Authorization records MUST carry provenance (KN-1) and confidence (§26). [Ref: §25.4 DSC-2]

#### 4.13.6 Verification
Authorization discovery outputs MUST be verified through cross-validation (DSC-3). [Ref: §25.4 DSC-3]

#### 4.13.7 Tools
The SDD does not specify tools for this activity. [Ref: §25]

#### 4.13.8 Mistakes
- Recording authorization mechanisms without provenance (DSC-2). [Ref: §25.4 DSC-2]
- Inferring authorization rules without runtime verification (DSC-6). [Ref: §25.4 DSC-6]

#### 4.13.9 References
- §25.2 Security Layer
- §25.4 DSC-2, DSC-3, DSC-6
- §26 Evidence Confidence Model

---

### 4.14 Event Discovery

#### 4.14.1 Purpose
Discover and document the events (messages, signals, notifications) produced and consumed by the unknown system. [Ref: §25.2 Behavior Layer]

#### 4.14.2 Inputs
- Module discovery outputs (§4.7). [Ref: §25.2]
- API discovery outputs (§4.8). [Ref: §25.2]
- Static analysis outputs (§4.18). [Ref: §25.2]
- Dynamic analysis outputs (§4.19). [Ref: §25.2]

#### 4.14.3 Activities
- Discover event types, event producers, event consumers, and event schemas.
- Document event flows and delivery guarantees.
- Cross-validate static event declarations against runtime observation (DSC-3). [Ref: §25.4 DSC-3]
- Assign provenance and confidence level (§26). [Ref: §25.4 DSC-2]

#### 4.14.4 Outputs
- Event inventory: discovered events with schemas, flows, provenance, and confidence. [Ref: §25.2; §25.4 DSC-2]

#### 4.14.5 Evidence Produced
Event records MUST carry provenance (KN-1) and confidence (§26). [Ref: §25.4 DSC-2]

#### 4.14.6 Verification
Event discovery outputs MUST be verified through cross-validation (DSC-3). [Ref: §25.4 DSC-3]

#### 4.14.7 Tools
The SDD does not specify tools for this activity. [Ref: §25]

#### 4.14.8 Mistakes
- Recording events without provenance (DSC-2). [Ref: §25.4 DSC-2]
- Missing asynchronous events that only appear at runtime (DSC-4: sufficiency for mission). [Ref: §25.4 DSC-4]

#### 4.14.9 References
- §25.2 Behavior Layer
- §25.4 DSC-2, DSC-3, DSC-4
- §26 Evidence Confidence Model

---

### 4.15 Workflow Discovery

#### 4.15.1 Purpose
Discover and document the business and operational workflows implemented by the unknown system. [Ref: §25.2 Behavior Layer]

#### 4.15.2 Inputs
- Event discovery outputs (§4.14). [Ref: §25.2]
- Execution flow recovery outputs (§4.16). [Ref: §25.2]
- Module discovery outputs (§4.7). [Ref: §25.2]
- API discovery outputs (§4.8). [Ref: §25.2]

#### 4.15.3 Activities
- Discover workflow steps, decision points, actor roles, and data transformations.
- Document workflow triggers and outcomes.
- Cross-validate inferred workflows against runtime observation (DSC-3). [Ref: §25.4 DSC-3]
- Assign provenance and confidence level (§26). [Ref: §25.4 DSC-2]

#### 4.15.4 Outputs
- Workflow specification: discovered workflows with steps, actors, provenance, and confidence. [Ref: §25.2; §25.4 DSC-2]

#### 4.15.5 Evidence Produced
Workflow records MUST carry provenance (KN-1) and confidence (§26). Every workflow MUST be documented (INT-7). [Ref: §25.4 DSC-2; §40.1 INT-7]

#### 4.15.6 Verification
Workflow discovery outputs MUST be verified through cross-validation (DSC-3). [Ref: §25.4 DSC-3]

#### 4.15.7 Tools
The SDD does not specify tools for this activity. [Ref: §25]

#### 4.15.8 Mistakes
- Recording workflows without provenance (DSC-2). [Ref: §25.4 DSC-2]
- Failing to document workflows (INT-7 violation). [Ref: §40.1 INT-7]
- Inventing workflows without evidence (DSC-6). [Ref: §25.4 DSC-6]

#### 4.15.9 References
- §25.2 Behavior Layer
- §25.4 DSC-2, DSC-3, DSC-6
- §26 Evidence Confidence Model
- §40.1 INT-7

---

### 4.16 Execution Flow Recovery

#### 4.16.1 Purpose
Recover the execution flow (control flow and data flow) through the unknown system. [Ref: §25.2 Behavior Layer]

#### 4.16.2 Inputs
- Module discovery outputs (§4.7). [Ref: §25.2]
- Dependency discovery outputs (§4.6). [Ref: §25.2]
- Static analysis outputs (§4.18). [Ref: §25.2 Analysis Methods]
- Dynamic analysis outputs (§4.19). [Ref: §25.2 Analysis Methods]

#### 4.16.3 Activities
- Recover control flow paths through functions, modules, and services.
- Recover data flow paths showing how data moves through the system.
- Cross-validate static control flow against runtime traces (DSC-3). [Ref: §25.4 DSC-3]
- Assign provenance and confidence level (§26). [Ref: §25.4 DSC-2]

#### 4.16.4 Outputs
- Execution flow model: recovered control and data flows with provenance and confidence. [Ref: §25.2; §25.4 DSC-2]

#### 4.16.5 Evidence Produced
Execution flow records MUST carry provenance (KN-1) and confidence (§26). [Ref: §25.4 DSC-2]

#### 4.16.6 Verification
Execution flow recovery outputs MUST be verified through cross-validation between static and dynamic analysis (DSC-3). [Ref: §25.4 DSC-3]

#### 4.16.7 Tools
The SDD does not specify tools for this activity. Tool selection is out of core scope (CN-1). [Ref: CN-1]

#### 4.16.8 Mistakes
- Recording execution flows without provenance (DSC-2). [Ref: §25.4 DSC-2]
- Relying solely on static analysis without runtime validation (DSC-3). [Ref: §25.4 DSC-3]
- Presenting inferred flows as observed (DSC-6). [Ref: §25.4 DSC-6]

#### 4.16.9 References
- §25.2 Behavior Layer
- §25.4 DSC-2, DSC-3, DSC-6
- §26 Evidence Confidence Model

---

### 4.17 Runtime Observation

#### 4.17.1 Purpose
Observe the unknown system at runtime to gather dynamic evidence of its behavior. [Ref: §25.2 Behavior Layer]

#### 4.17.2 Inputs
- Runtime environment detection outputs (§4.5). [Ref: §25.2]
- Technology detection outputs (§4.3). [Ref: §25.2]
- Active Mission defining observation scope (§32). [Ref: §32]

#### 4.17.3 Activities
- Observe system behavior at runtime: method calls, memory usage, network traffic, log output, error behavior.
- Record runtime observations as raw, pre-verification data (§31.2 Observed Facts). [Ref: §31.2]
- Runtime observation produces Level-A evidence (observed directly at runtime), the highest confidence level. [Ref: §26.2]
- Assign provenance and confidence level (§26). [Ref: §25.4 DSC-2]

#### 4.17.4 Outputs
- Runtime observation log: observed behaviors with timestamps, provenance, and confidence Level A. [Ref: §25.2; §26.2]

#### 4.17.5 Evidence Produced
Runtime observations are raw, pre-verification data (§31.2 Observed Facts). Each observation MUST carry provenance (KN-1) and confidence Level A (§26.2). [Ref: §25.4 DSC-2; §31.2; §26.2]

#### 4.17.6 Verification
Runtime observations MUST pass through the Evidence Chain (§28) before becoming engineering facts: Observation -> Evidence -> Verification -> Fact. [Ref: §28.2; ECH-1] Where Level-A evidence conflicts with B/C, the conflict MUST be recorded as a finding/risk; the higher-fidelity (runtime) evidence governs the recorded behavior (EVC-6). [Ref: §26.4 EVC-6]

#### 4.17.7 Tools
The SDD does not specify tools for this activity. [Ref: §25]

#### 4.17.8 Mistakes
- Treating raw runtime observations as verified facts without passing through the Evidence Chain (ECH-1). [Ref: §28.3 ECH-1]
- Recording observations without provenance (DSC-2). [Ref: §25.4 DSC-2]
- Silently resolving conflicts between runtime and static evidence instead of recording them (EVC-6). [Ref: §26.4 EVC-6]

#### 4.17.9 References
- §25.2 Behavior Layer
- §25.4 DSC-2
- §26 Evidence Confidence Model
- §26.2 (Level-A evidence)
- §26.4 EVC-6
- §28 Engineering Evidence Chain
- §31.2 Observed Facts

---

### 4.18 Static Analysis

#### 4.18.1 Purpose
Analyze the unknown system without executing it, to extract structural and behavioral facts. [Ref: §25.2 Analysis Methods]

#### 4.18.2 Inputs
- Asset inventory (§4.1). [Ref: §25.2]
- Repository inventory (§4.2). [Ref: §25.2]
- Source code, configuration files, build scripts, and other static artifacts.

#### 4.18.3 Activities
- Parse and analyze source code to extract: dependencies, control flow, data flow, API signatures, and structural metrics.
- Analyze configuration files for settings, overrides, and environment-specific values.
- Produce Level-B evidence (confirmed by implementation / source code). [Ref: §26.2]
- Cross-validate static analysis findings with dynamic analysis (DSC-3). [Ref: §25.4 DSC-3]
- Assign provenance and confidence level (§26). [Ref: §25.4 DSC-2]

#### 4.18.4 Outputs
- Static analysis report: extracted facts with provenance and confidence classification (Level B). [Ref: §25.2; §26.2; §25.4 DSC-2]

#### 4.18.5 Evidence Produced
Static analysis outputs produce Level-B evidence (confirmed by source code). [Ref: §26.2] Each output MUST carry provenance (KN-1) and confidence (§26). [Ref: §25.4 DSC-2]

#### 4.18.6 Verification
Static analysis findings MUST be cross-validated with dynamic analysis where possible (DSC-3). Where Level-A (runtime) evidence conflicts with B (static), the conflict MUST be recorded as a finding/risk (EVC-6). [Ref: §25.4 DSC-3; §26.4 EVC-6]

#### 4.18.7 Tools
The SDD does not specify tools for this activity. Tool selection is out of core scope (CN-1) and MAY be an extension (§19). [Ref: CN-1; §19]

#### 4.18.8 Mistakes
- Relying solely on static analysis without dynamic cross-validation (DSC-3). [Ref: §25.4 DSC-3]
- Treating static analysis findings as highest-confidence without runtime corroboration (DSC-6; EVC-6). [Ref: §25.4 DSC-6; §26.4 EVC-6]
- Recording findings without provenance (DSC-2). [Ref: §25.4 DSC-2]

#### 4.18.9 References
- §25.2 Analysis Methods
- §25.4 DSC-2, DSC-3, DSC-6
- §26 Evidence Confidence Model
- §26.2 (Level-B evidence)
- §26.4 EVC-6
- §28 Engineering Evidence Chain

---

### 4.19 Dynamic Analysis

#### 4.19.1 Purpose
Analyze the unknown system by executing it, to gather behavioral and runtime facts. [Ref: §25.2 Analysis Methods]

#### 4.19.2 Inputs
- Runtime environment detection outputs (§4.5). [Ref: §25.2]
- Build system detection outputs (§4.4). [Ref: §25.2]
- Static analysis outputs (§4.18) for cross-validation. [Ref: §25.2]

#### 4.19.3 Activities
- Execute the system under controlled conditions.
- Collect runtime traces, performance metrics, memory profiles, and behavioral observations.
- Produce Level-A evidence (observed directly at runtime), the highest confidence level. [Ref: §26.2]
- Cross-validate dynamic findings with static analysis (DSC-3). [Ref: §25.4 DSC-3]
- Assign provenance and confidence level (§26). [Ref: §25.4 DSC-2]

#### 4.19.4 Outputs
- Dynamic analysis report: observed behaviors with provenance and confidence classification (Level A). [Ref: §25.2; §26.2; §25.4 DSC-2]

#### 4.19.5 Evidence Produced
Dynamic analysis outputs produce Level-A evidence (observed directly at runtime). [Ref: §26.2] Each output MUST carry provenance (KN-1) and confidence (§26). [Ref: §25.4 DSC-2]

#### 4.19.6 Verification
Dynamic analysis findings MUST be cross-validated with static analysis (DSC-3). Where Level-A evidence conflicts with B/C, the conflict MUST be recorded as a finding/risk (EVC-6). [Ref: §25.4 DSC-3; §26.4 EVC-6]

#### 4.19.7 Tools
The SDD does not specify tools for this activity. Tool selection is out of core scope (CN-1) and MAY be an extension (§19). [Ref: CN-1; §19]

#### 4.19.8 Mistakes
- Relying solely on dynamic analysis without static cross-validation (DSC-3). [Ref: §25.4 DSC-3]
- Recording findings without provenance (DSC-2). [Ref: §25.4 DSC-2]
- Inferring static structure from runtime behavior without corroboration (DSC-6). [Ref: §25.4 DSC-6]

#### 4.19.9 References
- §25.2 Analysis Methods
- §25.4 DSC-2, DSC-3, DSC-6
- §26 Evidence Confidence Model
- §26.2 (Level-A evidence)
- §26.4 EVC-6
- §28 Engineering Evidence Chain

---

### 4.20 Cross Validation

#### 4.20.1 Purpose
Cross-validate (triangulate) findings from static analysis and dynamic analysis; record disagreements rather than silently resolving them. [Ref: §25.2 Analysis Methods; §25.4 DSC-3]

#### 4.20.2 Inputs
- Static analysis outputs (§4.18). [Ref: §25.2]
- Dynamic analysis outputs (§4.19). [Ref: §25.2]
- Runtime observation outputs (§4.17). [Ref: §25.2]
- Knowledge from other discovery activities.

#### 4.20.3 Activities
- Compare static findings against dynamic findings for the same system element.
- Record agreements (corroborated facts) and disagreements (conflicts requiring resolution).
- Apply triangulation (KN-6): corroborate facts by more than one source class before recording as authoritative. [Ref: §14.3 KN-6]
- Where Level-A evidence conflicts with B/C, record the conflict as a finding/risk (EVC-6). [Ref: §26.4 EVC-6]
- Divergences MUST be recorded as findings and MAY raise Decisions (§35) or Risks (§21); they MUST NOT be silently reconciled (CPM-3). [Ref: §37.3 CPM-3]
- Assign provenance and confidence level (§26) to cross-validated findings. [Ref: §25.4 DSC-2]

#### 4.20.4 Outputs
- Cross-validation report: corroborated facts, recorded disagreements, and resolution status for each, with provenance and confidence. [Ref: §25.2; §25.4 DSC-3; §25.4 DSC-2]

#### 4.20.5 Evidence Produced
Cross-validation outputs MUST carry provenance (KN-1) and confidence (§26). Disagreements are recorded as findings with provenance (DSC-3). [Ref: §25.4 DSC-2; DSC-3]

#### 4.20.6 Verification
Cross-validation is itself a verification activity. Its outputs MUST be verified against the Evidence Chain (§28). [Ref: §28.2]

#### 4.20.7 Tools
The SDD does not specify tools for this activity. [Ref: §25]

#### 4.20.8 Mistakes
- Silently resolving disagreements between static and dynamic analysis instead of recording them (DSC-3; CPM-3). [Ref: §25.4 DSC-3; §37.3 CPM-3]
- Recording cross-validated findings without provenance (DSC-2). [Ref: §25.4 DSC-2]
- Promoting single-source findings to authoritative without multi-source corroboration (KN-6). [Ref: §14.3 KN-6]

#### 4.20.9 References
- §25.2 Analysis Methods
- §14.3 KN-6
- §25.4 DSC-2, DSC-3
- §26 Evidence Confidence Model
- §26.4 EVC-6
- §28 Engineering Evidence Chain
- §35 Engineering Decision Model
- §37.3 CPM-3

---

### 4.21 Architecture Recovery

#### 4.21.1 Purpose
Synthesize architectural views (components, connectors, styles, constraints) from verified discovery facts. [Ref: §25.2 Synthesis]

#### 4.21.2 Inputs
- All layer discovery outputs (Inventory, Structure, Security, Behavior). [Ref: §25.2]
- Cross-validation outputs (§4.20). [Ref: §25.2]
- Verified facts from static and dynamic analysis (§4.18, §4.19). [Ref: §25.2]

#### 4.21.3 Activities
- Synthesize architectural components, connectors, styles, and constraints from verified facts.
- Produce architectural views consistent with the C4 model (referenced in Appendix A). [Ref: Appendix A]
- Cross-validate recovered architecture against source evidence (DSC-3). [Ref: §25.4 DSC-3]
- Assign provenance and confidence level (§26). [Ref: §25.4 DSC-2]
- Recovery MUST produce higher-level abstractions from lower-level artifacts, each evidenced (§26) and provenanced (§28). [Ref: §30.3 REV-2]

#### 4.21.4 Outputs
- Recovered architecture: architectural views with provenance and confidence classification. [Ref: §25.2 Synthesis; §25.4 DSC-2]

#### 4.21.5 Evidence Produced
Architecture recovery outputs MUST carry provenance (KN-1) and confidence (§26). Each recovered abstraction MUST be evidenced (§26) and provenanced (§28). [Ref: §25.4 DSC-2; §30.3 REV-2]

#### 4.21.6 Verification
Architecture recovery outputs MUST pass through the Evidence Chain (§28): Unknown Observation -> Evidence -> Verification -> Engineering Fact. [Ref: §28.2; ECH-1] Recovery outputs are Verified Facts or Engineering Knowledge per §31.2. [Ref: §31.2]

#### 4.21.7 Tools
The SDD does not specify tools for this activity. [Ref: §25]

#### 4.21.8 Mistakes
- Inventing architectural abstractions without evidence from lower-level artifacts (DSC-6; REV-2). [Ref: §25.4 DSC-6; §30.3 REV-2]
- Recording recovered architecture without provenance (DSC-2). [Ref: §25.4 DSC-2]
- Skipping cross-validation of recovered views (DSC-3). [Ref: §25.4 DSC-3]

#### 4.21.9 References
- §25.2 Synthesis
- §25.4 DSC-2, DSC-3, DSC-6
- §26 Evidence Confidence Model
- §28 Engineering Evidence Chain
- §30 Reverse Engineering Architecture
- §31 Repository Knowledge Architecture

---

### 4.22 Knowledge Extraction

#### 4.22.1 Purpose
Transform verified facts into synthesized engineering knowledge per the Knowledge Model (§14) and Repository Knowledge Architecture (§31). [Ref: §25.2 Synthesis]

#### 4.22.2 Inputs
- Verified facts from cross-validation (§4.20). [Ref: §25.2]
- Architecture recovery outputs (§4.21). [Ref: §25.2]
- All verified discovery layer outputs. [Ref: §25.2]

#### 4.22.3 Activities
- Transform verified facts into Engineering Knowledge (synthesized understanding from verified facts per §31.2). [Ref: §31.2]
- Classify knowledge per §31.2: Observed Facts, Verified Facts, Engineering Knowledge, Design Decisions, Architecture Decisions, Operational Knowledge. [Ref: §31.2]
- Every recorded fact MUST carry provenance (KN-1). [Ref: §14.3 KN-1]
- Apply triangulation (KN-6): corroborate facts by more than one source class before recording as authoritative. [Ref: §14.3 KN-6]
- Mark hypotheses as hypotheses (KN-3); they MUST NOT be recorded as facts until verified. [Ref: §14.3 KN-3]
- Knowledge MUST progress Observed -> Verified -> Engineering Knowledge only via the Evidence Chain (§28) (RKA-2). [Ref: §31.3 RKA-2]

#### 4.22.4 Outputs
- Engineering Knowledge records per §31.2, each with provenance, confidence, and authority classification. [Ref: §25.2 Synthesis; §31.2; §25.4 DSC-2]

#### 4.22.5 Evidence Produced
Knowledge extraction outputs are Engineering Knowledge (authoritative per §31.2). Each record MUST carry provenance (KN-1) and confidence (§26). [Ref: §14.3 KN-1; §25.4 DSC-2; §31.2]

#### 4.22.6 Verification
Knowledge extraction outputs MUST be verified against the Evidence Chain (§28) and the Knowledge Model rules (§14.3): KN-1 (provenance), KN-3 (hypothesis marking), KN-6 (triangulation). [Ref: §28.2; §14.3]

#### 4.22.7 Tools
The SDD does not specify tools for this activity. [Ref: §25]

#### 4.22.8 Mistakes
- Recording assumptions as facts (KN-1 + KN-3 + KN-6 is the structural defense against this). [Ref: §14.4]
- Promoting Observed Facts to Engineering Knowledge without passing through Verification (RKA-2; ECH-1). [Ref: §31.3 RKA-2; §28.3 ECH-1]
- Extracting knowledge without provenance (DSC-2; KN-1). [Ref: §25.4 DSC-2; §14.3 KN-1]

#### 4.22.9 References
- §25.2 Synthesis
- §14 Knowledge Model
- §14.3 KN-1, KN-3, KN-6
- §14.4 Anti-Assumption Discipline
- §25.4 DSC-2
- §26 Evidence Confidence Model
- §28 Engineering Evidence Chain
- §31 Repository Knowledge Architecture

---

### 4.23 Evidence Collection

#### 4.23.1 Purpose
Preserve all supporting evidence with provenance and confidence, realizing the Evidence Chain (§28). [Ref: §25.2 Synthesis; §28]

#### 4.23.2 Inputs
- All discovery outputs from Inventory, Structure, Security, Behavior layers. [Ref: §25.2]
- Analysis method outputs (static, dynamic, cross-validation). [Ref: §25.2]
- Synthesis outputs (architecture recovery, knowledge extraction). [Ref: §25.2]

#### 4.23.3 Activities
- Collect and organize all evidence items supporting discovery conclusions.
- Every evidence item MUST carry provenance (§28) and confidence (§26). [Ref: §25.4 DSC-2; §28]
- Every engineering fact MUST contain: Confidence Level; Evidence Source; Verification Status; Timestamp; Repository Reference (§26.3). [Ref: §26.3]
- Chain of custody MUST be preserved: each link MUST preserve provenance to its predecessor (ECH-2). [Ref: §28.3 ECH-2]
- Evidence collection feeds the Repository Knowledge Architecture (§31). [Ref: §31]

#### 4.23.4 Outputs
- Evidence collection: a provenance-preserving collection of all evidence items with confidence, verification status, timestamps, and repository references. [Ref: §25.2 Synthesis; §26.3; §28]

#### 4.23.5 Evidence Produced
Evidence collection outputs are the backbone of the Evidence Chain (§28). Each item MUST carry all five mandatory fact fields (§26.3): Confidence Level, Evidence Source, Verification Status, Timestamp, Repository Reference. [Ref: §26.3 EVC-2]

#### 4.23.6 Verification
Evidence collection MUST be verified against the Evidence Chain (§28): unbroken chain of custody (ECH-2), no observation recorded as fact without verification (ECH-1), every decision traces backward to verified facts (ECH-3). [Ref: §28.3 ECH-1, ECH-2, ECH-3]

#### 4.23.7 Tools
The SDD does not specify tools for this activity. [Ref: §25]

#### 4.23.8 Mistakes
- Collecting evidence without provenance (DSC-2; ECH-2). [Ref: §25.4 DSC-2; §28.3 ECH-2]
- Missing mandatory fact fields (EVC-2). [Ref: §26.4 EVC-2]
- Breaking the chain of custody (ECH-2). [Ref: §28.3 ECH-2]
- Hypotheses (confidence E) passing verification without being verified (ECH-5). [Ref: §28.3 ECH-5]

#### 4.23.9 References
- §25.2 Synthesis
- §25.4 DSC-2
- §26 Evidence Confidence Model
- §26.3 Mandatory Fact Fields
- §26.4 EVC-2
- §28 Engineering Evidence Chain
- §28.3 ECH-1, ECH-2, ECH-3, ECH-5

---

### 4.24 Documentation

#### 4.24.1 Purpose
Produce documentation from discovery outputs, classified per the Documentation Model (§38). [Ref: §25.2 Output; §38]

#### 4.24.2 Inputs
- All discovery layer outputs (Inventory, Structure, Security, Behavior). [Ref: §25.2]
- Synthesis outputs (architecture recovery, knowledge extraction, evidence collection). [Ref: §25.2]
- Cross-validation outputs (§4.20). [Ref: §25.2]

#### 4.24.3 Activities
- Author or generate documentation units from discovery outputs.
- Classify each documentation unit as exactly one of: Observed, Verified, Planned, Implemented, Validated, Historical, Deprecated, Generated, or Authoritative (§38.2). [Ref: §38.2]
- Each documentation unit MUST declare its category (§38.2) and its authority class (§11.2) (DOC-2). [Ref: §38.3 DOC-2]
- Generated documentation MUST NOT be hand-edited and MUST be reproducible (DOC-3). [Ref: §38.3 DOC-3]
- Observed/Planned documentation MUST NOT be presented as Verified/Validated without passing the Evidence Chain (§28) / Validation (§16) (DOC-4). [Ref: §38.3 DOC-4]
- Documentation MUST NOT mix the §38.2 categories within one authoritative unit (DOC-1). [Ref: §38.3 DOC-1]

#### 4.24.4 Outputs
- Documentation units per §38.2 categories, each with declared category, authority class, and provenance. [Ref: §25.2 Output; §38.2; §38.3 DOC-2]

#### 4.24.5 Evidence Produced
Documentation outputs MUST carry provenance (§28) and confidence (§26). Each unit's category and authority class are recorded as metadata (DOC-2). [Ref: §38.3 DOC-2; §25.4 DSC-2]

#### 4.24.6 Verification
Documentation MUST be reviewed per §15 (RV-1). [Ref: §15.2 RV-1] Generated documentation MUST be verified as reproducible from its authoritative source (RA-4). [Ref: §10.2 RA-4]

#### 4.24.7 Tools
The SDD does not specify tools for this activity. [Ref: §25]

#### 4.24.8 Mistakes
- Mixing documentation categories within one authoritative unit (DOC-1). [Ref: §38.3 DOC-1]
- Presenting unverified documentation as verified (DOC-4). [Ref: §38.3 DOC-4]
- Hand-editing generated documentation (DOC-3; PR-6). [Ref: §38.3 DOC-3]
- Producing documentation without provenance (DSC-2). [Ref: §25.4 DSC-2]

#### 4.24.9 References
- §25.2 Output
- §11 Artifact Architecture
- §15 Review Model
- §25.4 DSC-2
- §38 Engineering Documentation Model

---

### 4.25 Verification

#### 4.25.1 Purpose
Verify discovery outputs against the "Discovery Complete" criteria (§27) and ensure all evidence satisfies the Evidence Chain (§28). [Ref: §25.2 Output; §27; §28]

#### 4.25.2 Inputs
- All discovery outputs from Inventory, Structure, Security, Behavior layers. [Ref: §25.2]
- Synthesis outputs (architecture recovery, knowledge extraction, evidence collection). [Ref: §25.2]
- Documentation outputs (§4.24). [Ref: §25.2]
- Discovery Complete criteria from §27. [Ref: §25.4 DSC-5]

#### 4.25.3 Activities
- Verify that discovery outputs satisfy the Discovery Complete criteria (§27) (DSC-5). [Ref: §25.4 DSC-5]
- Verify that every output carries provenance (KN-1) and confidence (§26) (DSC-2). [Ref: §25.4 DSC-2]
- Verify that static and dynamic analysis have been combined and cross-validated (DSC-3). [Ref: §25.4 DSC-3]
- Verify that no conclusion asserts confidence exceeding its evidence (DSC-6). [Ref: §25.4 DSC-6]
- Verify sufficiency for the mission (DSC-4: complete comprehension is NOT required). [Ref: §25.4 DSC-4]
- Apply the Evidence Chain (§28): ensure observations -> evidence -> verification -> facts. [Ref: §28.2]
- Verify against the Engineering Integrity Rules (§40): no undocumented dependency (INT-3), API (INT-4), database object (INT-5), configuration (INT-6), workflow (INT-7), security rule (INT-8), or assumption (INT-9). [Ref: §40.1]

#### 4.25.4 Outputs
- Verification report: objective pass/fail verdict against §27 criteria, with cited evidence. [Ref: §25.2 Output; §16.4 VL-1; §25.4 DSC-5]
- Discovery Complete status: asserted only when §27 criteria are objectively met. [Ref: §25.4 DSC-5]

#### 4.25.5 Evidence Produced
A conformance verdict MUST cite the evidence on which it rests (VL-4). [Ref: §16.4 VL-4] Verification outputs MUST carry provenance (§28). [Ref: §25.4 DSC-2]

#### 4.25.6 Verification
Verification itself is the capstone activity of Discovery. Discovery is complete only when the Discovery Complete criteria (§27) are objectively met (DSC-5). [Ref: §25.4 DSC-5] A completion state is reached only when its exit criteria are verified by a method in §16.2 (CMP-2). [Ref: §27.3 CMP-2]

#### 4.25.7 Tools
The SDD does not specify tools for this activity. [Ref: §25]

#### 4.25.8 Mistakes
- Asserting Discovery Complete without verifying against §27 criteria (DSC-5). [Ref: §25.4 DSC-5]
- Asserting conformance without cited evidence (VL-4). [Ref: §16.4 VL-4]
- Claiming complete comprehension when only mission sufficiency is required (DSC-4). [Ref: §25.4 DSC-4]
- Failing to verify provenance on all outputs (DSC-2). [Ref: §25.4 DSC-2]

#### 4.25.9 References
- §25.2 Output
- §16 Validation Model
- §16.4 VL-1, VL-4
- §25.4 DSC-2, DSC-4, DSC-5, DSC-6
- §27 Engineering Completion Criteria
- §27.3 CMP-2
- §28 Engineering Evidence Chain
- §40 Engineering Integrity Rules

---

## 5. Discovery Layers

This section maps the 25 discovery activities to their evidence layers per §25.2. [Ref: §25.2]

### 5.1 Inventory Layer
| Activity | Reference |
|---|---|
| Asset Inventory | §4.1 |
| Repository Inventory | §4.2 |
| Technology Detection | §4.3 |
| Build System Detection | §4.4 |
| Runtime Environment Detection | §4.5 |

### 5.2 Structure Layer
| Activity | Reference |
|---|---|
| Dependency Discovery | §4.6 |
| Module Discovery | §4.7 |
| API Discovery | §4.8 |
| Database Discovery | §4.9 |
| Configuration Discovery | §4.10 |

### 5.3 Security Layer
| Activity | Reference |
|---|---|
| Security Discovery | §4.11 |
| Authentication Discovery | §4.12 |
| Authorization Discovery | §4.13 |

### 5.4 Behavior Layer
| Activity | Reference |
|---|---|
| Event Discovery | §4.14 |
| Workflow Discovery | §4.15 |
| Execution Flow Recovery | §4.16 |
| Runtime Observation | §4.17 |

### 5.5 Analysis Methods
| Activity | Reference |
|---|---|
| Static Analysis | §4.18 |
| Dynamic Analysis | §4.19 |
| Cross Validation | §4.20 |

### 5.6 Synthesis
| Activity | Reference |
|---|---|
| Architecture Recovery | §4.21 |
| Knowledge Extraction | §4.22 |
| Evidence Collection | §4.23 |

### 5.7 Output
| Activity | Reference |
|---|---|
| Documentation | §4.24 |
| Verification | §4.25 |
| Discovery Complete (§27 criteria) | §25.2 Output; §25.4 DSC-5 |

---

## 6. Completion Criteria

Discovery is complete only when the following are satisfied: [Ref: §25.4 DSC-5; §27]

1. **DSC-1 satisfaction**: The unknown system has passed through Discovery before any modification. [Ref: §25.4 DSC-1]
2. **DSC-2 satisfaction**: Every discovery output carries provenance (KN-1) and a confidence level (§26). [Ref: §25.4 DSC-2]
3. **DSC-3 satisfaction**: Discovery has combined static and dynamic analysis and cross-validated (triangulated); disagreements have been recorded, not silently resolved. [Ref: §25.4 DSC-3]
4. **DSC-4 satisfaction**: Discovery has achieved sufficiency for the mission; complete comprehension has not been required. [Ref: §25.4 DSC-4]
5. **DSC-5 satisfaction**: The "Discovery Complete" criteria (§27) are objectively met. Discovery is complete only when the §27 criteria are objectively met. [Ref: §25.4 DSC-5; §27]
6. **DSC-6 satisfaction**: No discovery conclusion asserts confidence exceeding its evidence. [Ref: §25.4 DSC-6]
7. **Activity coverage**: All 25 discovery activities (§4.1–§4.25) have been executed and their outputs verified. [Ref: §25.3]
8. **Layer coverage**: All 7 discovery layers (§5.1–§5.7) have been addressed. [Ref: §25.2]
9. **Integrity rules**: No INT rule (§40) has been violated. [Ref: §40]
10. **Evidence chain**: All discovery outputs have passed through the Evidence Chain (§28). [Ref: §28]
