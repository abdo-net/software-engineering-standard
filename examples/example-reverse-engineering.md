# Example: SES Applied to a Reverse Engineering Engagement — ReconSys Binary Analysis

> **NON-NORMATIVE** — This document is a worked example for illustrative purposes only.
> It demonstrates how the Software Engineering Standard (SES) MAY be applied to a project
> in the reverse engineering domain. [Ref: §4.2 Domains the SES Must Cover; §30 Reverse Engineering Architecture; §24 Phase 9 — Worked examples]
> This example introduces no new rules and extends no architecture.

---

## Artifact Metadata

| Field | Value |
|---|---|
| **Object ID** | EX-REV-001 |
| **Object Type** | Example |
| **Authority Class** | Generated |
| **Owner** | SES Phase 9 — Example Writer |
| **Lifecycle State** | COMPLETED |
| **Status** | Accepted |
| **Version** | 0.1.0 |
| **Parent Objects** | SES v0.4.0 |
| **Repository Location** | `examples/example-reverse-engineering.md` |
| **Generated From** | SDD v0.4.0 §30.2, §30.4, §32.2, §25.3, §35.2, §13.2, §16.5 |

---

## 1. Fictional Project Context

**Project name:** ReconSys Legacy Protocol Recovery (codename: "ReconSys")
**Domain:** Reverse engineering — binary protocol recovery for inter-process communication
**Context:** A logistics company has a 20-year-old Windows executable (`LogisticsCore.exe`, ~3.2MB, no source code) that handles shipment routing. The executable communicates with a label printer daemon via an undocumented binary protocol over TCP port 9147. The company needs to build a modern replacement for the printer daemon in Go, which requires reverse engineering the protocol. The organization has the legal right to reverse engineer this software (authorized by the original license agreement for interoperability purposes per §30.4).

**Distinction per §30.4:** This is a **binary reverse engineering** context — source code is unavailable. The activity model (§30.2) still applies; techniques are context-bound. [Ref: §30.4 Competing Contexts]

---

## 2. Mission Creation (§32.2)

The Mission is created following the eight-element structure mandated by §32.2. [Ref: §32.2 Mission Structure; MIS-1, MIS-2]

| Mission Element | Content |
|---|---|
| **Objective** | Reverse engineer the undocumented binary protocol between `LogisticsCore.exe` and the printer daemon (TCP port 9147) to produce a protocol specification sufficient for building a compatible replacement daemon in Go. |
| **Scope** | In scope: Protocol message format recovery (request/response pairs); state machine recovery (connection lifecycle); data type mapping; error code catalog; protocol specification document. Out of scope: Reverse engineering of shipment routing logic; UI behavior; database schema recovery; modification of `LogisticsCore.exe`. |
| **Constraints** | CN-LEGAL: Reverse engineering authorized only for interoperability (license clause 4.2). CN-ALTER: MUST NOT modify `LogisticsCore.exe` (examination only per REV-1). CN-SCOPE: Protocol on TCP port 9147 only. CN-OUTPUT: Protocol spec must be complete enough for independent reimplementation. |
| **Expected Deliverables** | (1) ADR for reverse engineering technique selection; (2) Protocol message format specification; (3) Recovered state machine diagram; (4) Error code catalog with observed triggers; (5) Characterization test suite (mock daemon validating protocol compliance); (6) Knowledge preservation record per REV-5. |
| **Success Criteria** | SC-PROTO: Mock daemon passes 100% of captured protocol exchanges (47 request/response pairs). SPEC-COMP: Specification covers all message types observed. SPEC-STATE: State machine accounts for all observed transitions. |
| **Allowed Operations** | DISCOVER, ANALYZE, TRACE, VERIFY, DOCUMENT, COMPARE, PLAN, VALIDATE, REVIEW [Ref: §34.2 Operations and Governing Sections] |
| **Forbidden Operations** | IMPLEMENT — implementation of the replacement daemon is a separate Mission requiring its own authorization per MIS-4. Any modification of `LogisticsCore.exe` per REV-1. Decompilation for purposes beyond interoperability. |
| **Evidence Requirements** | All facts carry confidence level per §26; all decisions recorded per §35; protocol facts triangulated via dynamic + static analysis per DSC-3; all hypotheses marked per KN-3. |

> **Mission validation note:** The Mission above defines all eight elements required by MIS-2. Allowed Operations exclude IMPLEMENT because implementation is a distinct Mission per MIS-4. The Forbidden Operations reflect REV-1 (examination must not alter the subject system). [Ref: MIS-2; MIS-4; REV-1]

---

## 3. Discovery Activities (§25.3)

Discovery is performed following the mandated activity set from §25.3. [Ref: §25.3 Mandated Discovery Activities; DSC-1, DSC-2, DSC-3]

### 3.1 Discovery Results Summary

| Activity Layer | Activities Performed | Key Findings | Confidence |
|---|---|---|---|
| **Inventory Layer** | Asset Inventory; Repository Inventory; Technology Detection; Build System Detection; Runtime Environment Detection | Single binary: `LogisticsCore.exe` (PE32, compiled 2004-08-12). No source, no build system. Windows XP VM runtime. TCP port 9147 listener spawned by binary. Printer daemon: `PrintDaemon.exe` (companion binary, also PE32). | B (binary analysis) |
| **Structure Layer** | Dependency Discovery; Module Discovery; API Discovery; Database Discovery; Configuration Discovery | Binary imports: `ws2_32.dll` (Winsock), `kernel32.dll`, `user32.dll`, `msvcrt.dll`. No database imports. Registry key: `HKLM\Software\LogisticsCore\PrinterIP`. Static strings: "LP_MSG_", "ERR_", "PRINT_OK" patterns. | B (static analysis) |
| **Security Layer** | Security Discovery; Authentication Discovery; Authorization Discovery | No encryption on port 9147 (plaintext binary protocol). No authentication handshake observed. Source IP filtering: only accepts connections from localhost or configured PrinterIP. | A (runtime-confirmed) |
| **Behavior Layer** | Event Discovery; Workflow Discovery; Execution Flow Recovery; Runtime Observation | Connection workflow: `CONNECT → HELLO → JOB_START → [DATA*] → JOB_END → DISCONNECT`. Message types identified: 8 request types, 6 response types. Heartbeat every 30 seconds. Timeout: 60 seconds idle disconnect. | A (runtime-confirmed) |
| **Analysis Methods** | Static Analysis; Dynamic Analysis; Cross-Validation (triangulation) | Static: IDA Pro disassembly of message handler function at offset `0x00402A10`. Dynamic: Wireshark capture of 47 complete sessions. Triangulation: disassembly shows switch on message type byte (offset 0x04) matching observed values in packet captures. One divergence: static shows 0x07 case not observed in runtime — marked as hypothesis H-REV-001. | D (triangulated) |
| **Synthesis** | Architecture Recovery; Knowledge Extraction; Evidence Collection; Documentation; Verification | Recovered: simple request-response protocol with 1-byte message type, 2-byte length prefix, variable payload, 1-byte checksum (XOR). State machine: 5 states, 14 transitions. Knowledge preserved in `docs/discovery/reconsys-protocol-knowledge.md` per REV-5. | D |

### 3.2 Discovery Evidence Sample — Binary vs. Source-Available Context

| Fact ID | Statement | Confidence | Evidence Source | Verification Status |
|---|---|---|---|---|
| F-REV-001 | Protocol uses TCP port 9147 with 1-byte message type at payload offset 0x04 | A | Wireshark capture of 47 sessions; IDA disassembly of `0x00402A10` shows `movzx eax, byte ptr [esi+4]` then `jmp ds:off_402BC0[eax*4]` (switch table) | Runtime + static triangulated |
| F-REV-002 | Message type 0x01 = HELLO, 0x02 = JOB_START, 0x03 = DATA, 0x04 = JOB_END, 0x05 = DISCONNECT | A | Wireshark: 47 sessions show these type values at corresponding protocol phases; mock daemon replays confirm expected responses | Runtime-confirmed with replay validation |
| F-REV-003 | Checksum is XOR of all payload bytes, verified by server | B | IDA: function `0x00403120` loops through payload with `xor al, [esi+edx]`; runtime: modified checksum byte elicits ERR_CHECKSUM (0xFE) response | Static + runtime triangulated |
| F-REV-004 | Message type 0x07 exists in switch table but was not observed in 47 captured sessions | E | IDA: switch table has entry for index 0x07 pointing to handler `0x00402F80`. No runtime observation. | Hypothesis per KN-3; EVC-3 |
| F-REV-005 | Connection accepts only from localhost or configured PrinterIP (registry key) | A | Registry value `PrinterIP=192.168.1.50`; runtime: connection from `192.168.1.51` rejected with RST; localhost accepted | Runtime observation |

> **Discovery completeness:** Discovery is goal-directed per DSC-4 — sufficiency for the Mission is the criterion, not full comprehension. The distinction between source-available and binary reverse engineering (§30.4) is observed: the activity model is common, but technique is context-bound. Static analysis uses disassembly instead of source code reading; dynamic analysis (packet capture) provides the primary evidence source per confidence Level A. Hypothesis F-REV-004 is correctly marked at confidence E per KN-3 and EVC-3. [Ref: DSC-2; DSC-3; DSC-4; EVC-1; EVC-3; KN-3]

---

## 4. Key Decisions (§35.2)

Decisions are recorded following the nine-field structure from §35.2. [Ref: §35.2 Decision Structure; DEC-1]

### Decision 1: Reverse Engineering Technique Selection

| Field | Content |
|---|---|
| **Decision** | Combined dynamic analysis (primary) + static analysis (confirmatory) — not decompilation to pseudo-code. Protocol recovered from runtime observation, validated against disassembly. |
| **Decision Context** | Binary reverse engineering context (§30.4): source unavailable. Need to recover protocol semantics. Decompilation (Hex-Rays) produces readable C but may introduce artifacts that are not in the binary. |
| **Alternatives** | Alt-A: Pure dynamic analysis (capture + replay only). Alt-B: Decompilation to pseudo-code, then analysis. Alt-C: Combined dynamic + static without decompilation (selected). |
| **Evidence** | §30.4: "Source-available reverse engineering and binary/protocol reverse engineering differ in technique... the activity model is common to both, while technique is context-bound." Alt-A risks missing unobserved message types (e.g., 0x07). Alt-B introduces decompilation artifacts that may be mistaken for facts (KN-3 risk). Alt-C captures runtime behavior (Level A evidence) while using static analysis for triangulation (DSC-3). |
| **Impact** | + Highest-confidence evidence from runtime. + Static analysis confirms without decompilation artifacts. + Unobserved message type (0x07) discovered via static analysis, correctly marked as hypothesis. ~ Requires more analyst time than pure dynamic. |
| **Dependencies** | §30.2 activity model; §30.4 context distinction; DSC-3 (triangulation). |
| **Approval** | Approved by Reverse Engineering Lead on 2024-07-08. |
| **Status** | Approved |
| **Superseded By** | — |

### Decision 2: Scope of Protocol Specification

| Field | Content |
|---|---|
| **Decision** | Protocol spec will document all observed message types (0x01–0x06) plus the unobserved type 0x07 as "reserved/unconfirmed" with its discovered handler address but without claimed semantics. |
| **Decision Context** | F-REV-004 (message type 0x07 exists in switch table but unobserved). Risk: documenting 0x07 with guessed semantics would violate KN-3 (hypothesis as fact) and EVC-3 (Level E must not be authoritative). |
| **Alternatives** | Alt-A: Document only observed types (0x01–0x06). Alt-B: Document 0x07 with guessed semantics. Alt-C: Document 0x07 as reserved/unconfirmed with raw evidence (selected). |
| **Evidence** | KN-3: "A hypothesis MUST be marked as a hypothesis until verified by evidence." EVC-3: "A Level-E fact is a hypothesis and MUST NOT be treated as authoritative." Alt-B would violate both. Alt-C preserves evidence for a future Mission while not overclaiming. |
| **Impact** | + Preserves knowledge without overclaiming. + Future Mission (implementation) can decide whether to handle 0x07. + Demonstrates anti-assumption discipline per §14.4. |
| **Dependencies** | F-REV-004. KN-3. EVC-3. §14.4 Anti-Assumption Discipline. |
| **Approval** | Approved by Engineering Lead on 2024-07-10. |
| **Status** | Approved |
| **Superseded By** | — |

> **Decision integrity note:** Both decisions are immutable per DEC-3. If either needs change, a new Decision would supersede it. Every artifact produced traces to exactly one Decision per DEC-4. [Ref: DEC-3; DEC-4]

---

## 5. Stage Progression (§13.2)

Stage progression follows the mandatory schema from §13.2. [Ref: §13.2 Mandatory Stage Schema] For brevity, two representative stages are shown.

### Stage 1: Protocol Discovery

| Field | Content |
|---|---|
| **Entry Criteria** | Mission active. Legal authorization for reverse engineering confirmed. Binary obtained and execution environment reproduced (Windows XP VM). Decision 1 (technique selection) is Approved. |
| **Inputs** | `LogisticsCore.exe` binary; `PrintDaemon.exe` binary; Windows XP VM; Mission constraints (CN-LEGAL, CN-ALTER). |
| **Activities** | Run `LogisticsCore.exe` + `PrintDaemon.exe` in VM; capture TCP port 9147 traffic with Wireshark; perform 10 distinct operations (create shipment, print label, cancel job, etc.) to exercise protocol; label message types; extract static strings; perform initial IDA disassembly of message handler. |
| **Outputs** | Wireshark capture file `reconsys-47-sessions.pcapng` (Generated). `docs/discovery/message-types-initial.md` — Authoritative artifact. IDA database `LogisticsCore.idb` (Generated). |
| **Evidence Produced** | 47 complete sessions captured. 8 request message types identified. 6 response message types identified. Connection state machine: 5 states tentatively identified. All outputs carry provenance and confidence per DSC-2. |
| **Exit Criteria** | ≥20 distinct sessions captured across all printer operations. Message type labels tentative but consistent. No modification of binary (REV-1 verified). |
| **Verification Criteria** | Capture file integrity hash (SHA-256) recorded. Binary checksum matches original. Log confirms no binary modification. [Ref: §16.2] |
| **Review Type** | Walkthrough per §15.1 (early-stage understanding/recovery). [Ref: §15.1] |

### Stage 2: Protocol Specification

| Field | Content |
|---|---|
| **Entry Criteria** | Stage 1 exit criteria verified. Decision 2 (specification scope) is Approved. Impact analysis record IMP-REV-001 reviewed. Repository Readiness gate "Implementation Ready" satisfied per §41.2 (for specification production). |
| **Inputs** | Discovery facts F-REV-001 through F-REV-005; Decisions DEC-REV-001, DEC-REV-002; Wireshark capture; IDA disassembly; mock daemon skeleton. |
| **Activities** | Map each message type to request/response schema; document field offsets, lengths, and encodings; construct state machine from session traces; build mock daemon that replays captured sessions; validate specification against all 47 captures; write protocol specification document. |
| **Outputs** | `specs/reconsys-protocol-v1.md` — Authoritative artifact. `tests/mock_daemon.c` — Authoritative artifact. State machine diagram (Generated). Specification review record. |
| **Evidence Produced** | Mock daemon: 47/47 captured sessions replay successfully (100% pass). Specification covers 6 confirmed message types + 1 reserved (0x07). State machine: 5 states, 14 transitions, all observed in traces. |
| **Exit Criteria** | All 47 sessions replay successfully. Specification reviewed and approved. State machine covers all observed transitions. Hypothesis 0x07 correctly marked per KN-3/EVC-3. |
| **Verification Criteria** | Mock daemon replay report (Test). Specification review checklist (Inspection). State machine trace coverage (Analysis). [Ref: §16.2] |
| **Review Type** | Inspection per §15.1 (for protocol specification — accuracy-critical). [Ref: RV-1] |

> **Stage rules observed:** SG-1 — exit criteria verified before stage declared complete. SG-2 — outputs classified per Artifact Authority Model (§11.1). SG-4 — validation responsibility (mock daemon authoring) kept distinct from specification authoring per PR-8. [Ref: SG-1; SG-2; SG-4]

---

## 6. Conformance Assertion (§16.5)

The conformance assertion is recorded following §16.5. [Ref: §16.5 Conformance / Certification Concept; FR-15; VL-1, VL-4]

| Field | Value |
|---|---|
| **Project** | ReconSys Protocol Recovery |
| **Standard Version** | SES v0.4.0 |
| **Assertion Date** | 2024-09-05 |
| **Asserted By** | Reverse Engineering Lead (with Independent Reviewer confirmation per RV-4) |
| **Conformance Scope** | Partial conformance — Protocol reverse engineering engagement only. Implementation of replacement daemon is a separate Mission not assessed. |
| **Evidence Summary** | All required artifacts present: Mission (8 elements, §32.2), 2 Decisions (9 fields each, §35.2), Discovery record (§25.3 activities with confidence/provenance, §26.2), Stage records (§13.2 schema), Review records (§15.1 types), Validation records (§16.2 methods). Activity model from §30.2 followed. Binary/source-available distinction from §30.4 observed. REV-1 (examination only) verified throughout. |
| **Pass/Fail Verdict** | **PASS** — All applicable SES requirements for this Mission scope are satisfied. |
| **Cited Evidence** | Mission record: MS-REV-001. Decisions: DEC-REV-001, DEC-REV-002. Discovery: DSC-RPT-REV-001. Stages: STG-REV-001, STG-REV-002. Reviews: RV-WALK-001, RV-SPEC-001. Validation: VAL-RPT-REV-001. |
| **Limitations** | Hypothesis H-REV-001 (message type 0x07) remains unverified — a future Mission may investigate. Binary reverse engineering techniques are context-bound per §30.4 and not generalizable to all reverse engineering contexts. Legal authorization scope (interoperability only) constrains use of recovered knowledge. |

> **Verifiability note:** The assertion cites specific evidence records per VL-4 and names the standard version per VS-3. The verdict is objective pass/fail per VL-1. [Ref: VL-1; VL-4; VS-3]

---

## 7. SES Sections Cited in This Example

| SDD Section | How Demonstrated |
|---|---|
| §4.2 (reverse engineering domain) | Example context: fictional ReconSys protocol recovery |
| §11.1 (Artifact Authority Model) | Outputs classified as Authoritative/Generated |
| §11.2 (Artifact Metadata) | Metadata header on this example document |
| §13.2 (Mandatory Stage Schema) | Two stages with all 8 fields populated |
| §14.4 (Anti-Assumption Discipline) | Hypothesis 0x07 marked per KN-3/EVC-3 |
| §15.1 (Review Types) | Walkthrough + Inspection applied |
| §16.2 (Verification Methods) | Test, Analysis used |
| §16.5 (Conformance Assertion) | Recorded verdict with evidence |
| §25.3 (Discovery Activities) | All 6 activity layers demonstrated |
| §26.2 (Confidence Levels) | Facts graded A–E; hypothesis at Level E |
| §30.2 (Activity Model) | Unknown → Discovery → Recovery → Understanding → Documentation → Planning → Modification → Validation → Knowledge Preservation |
| §30.4 (Competing Contexts) | Binary RE distinguished from source-available; legal constraints noted |
| §32.2 (Mission Structure) | Mission with all 8 elements |
| §34.2 (Operations) | Allowed Operations drawn from closed set; IMPLEMENT excluded |
| §35.2 (Decision Structure) | Two decisions with all 9 fields |
| §41.2 (Readiness Gates) | Implementation Ready gate referenced |

---

> **End of Example.** This document is NON-NORMATIVE and exists solely to demonstrate SES application. [Ref: §24 Phase 9; §10.3 Authority Rule]
