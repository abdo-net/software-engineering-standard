# Example: SES Applied to a RADIUS / Network Server — NetAuth RADIUS Infrastructure

> **NON-NORMATIVE** — This document is a worked example for illustrative purposes only.
> It demonstrates how the Software Engineering Standard (SES) MAY be applied to a project
> in the RADIUS / network servers domain. [Ref: §4.2 Domains the SES Must Cover; §24 Phase 9 — Worked examples]
> This example introduces no new rules and extends no architecture.

---

## Artifact Metadata

| Field | Value |
|---|---|
| **Object ID** | EX-RAD-001 |
| **Object Type** | Example |
| **Authority Class** | Generated |
| **Owner** | SES Phase 9 — Example Writer |
| **Lifecycle State** | COMPLETED |
| **Status** | Accepted |
| **Version** | 0.1.0 |
| **Parent Objects** | SES v0.4.0 |
| **Repository Location** | `examples/example-radius-network.md` |
| **Generated From** | SDD v0.4.0 §32.2, §25.3, §35.2, §13.2, §16.5 |

---

## 1. Fictional Project Context

**Project name:** NetAuth RADIUS Infrastructure (codename: "NetAuth")
**Domain:** Network authentication server — RADIUS protocol implementation for enterprise Wi-Fi and VPN access
**Context:** A 5-year-old RADIUS server handling 180K authentication requests/day for 12K active users across 340 Wi-Fi access points and 8 VPN concentrators. Written in C with an event-driven architecture (libevent), SQLite for local user cache, and PostgreSQL as the master user directory. The organization needs to add RFC 8049-compatible (RADIUS Accounting) support for usage-based billing while maintaining 99.99% availability.

---

## 2. Mission Creation (§32.2)

The Mission is created following the eight-element structure mandated by §32.2. [Ref: §32.2 Mission Structure; MIS-1, MIS-2]

| Mission Element | Content |
|---|---|
| **Objective** | Add RFC 8049-compatible RADIUS Accounting support to NetAuth enabling usage-based billing data collection (session duration, data volume, access point location) while maintaining 99.99% service availability and <50ms authentication response time. |
| **Scope** | In scope: RADIUS Accounting packet handling (Start/Stop/Interim-Update); accounting data persistence; billing record aggregation API; operational monitoring for accounting flow. Out of scope: Billing system integration (external consumer of API); changes to authentication logic; RADIUS CoA/Dynamic Authorization. |
| **Constraints** | CN-AVAIL: 99.99% uptime (max 4.32 min downtime/month). CN-LATENCY: Authentication response p99 <50ms. CN-RFC: Must comply with RFC 8049 (RADIUS Accounting). CN-PROTO: Must interoperate with existing 340 access points (mixed vendors: Cisco, Aruba, Ubiquiti). |
| **Expected Deliverables** | (1) ADR for accounting data storage approach; (2) RADIUS Accounting packet handler implementation; (3) Accounting database schema; (4) Aggregation API contract (OpenAPI); (5) Characterization tests for auth latency under accounting load; (6) Operational runbook for accounting monitoring. |
| **Success Criteria** | SC-RFC: Packet format validated by `radtest` against RFC 8049 test vectors. SC-LATENCY: p99 auth latency <50ms with accounting enabled. SC-AVAIL: Zero unplanned downtime during deployment. SC-DATA: 100% of Accounting-Stop packets persisted (zero loss). |
| **Allowed Operations** | DISCOVER, ANALYZE, TRACE, VERIFY, DOCUMENT, COMPARE, PLAN, IMPLEMENT, VALIDATE, REVIEW [Ref: §34.2 Operations and Governing Sections] |
| **Forbidden Operations** | Modification of Access-Request/Access-Accept packet handling logic; changes to SQLite schema for authentication cache; deployment without canary verification; removal of existing accounting attributes from Access-Accept. |
| **Evidence Requirements** | All facts carry confidence level per §26; all decisions recorded per §35; all protocol claims validated by RFC 8049 test vectors; latency claims validated by load test; availability measured by production monitoring. |

> **Mission validation note:** The Mission above defines all eight elements required by MIS-2. Allowed Operations are drawn from the closed set in §34.2 per MIS-3. [Ref: MIS-2; MIS-3]

---

## 3. Discovery Activities (§25.3)

Discovery is performed following the mandated activity set from §25.3. [Ref: §25.3 Mandated Discovery Activities; DSC-1, DSC-2, DSC-3]

### 3.1 Discovery Results Summary

| Activity Layer | Activities Performed | Key Findings | Confidence |
|---|---|---|---|
| **Inventory Layer** | Asset Inventory; Repository Inventory; Technology Detection; Build System Detection; Runtime Environment Detection | Single repo in Git. C11, libevent 2.1, SQLite 3.39, PostgreSQL 14, Docker for dev, bare metal production (2 nodes + HAProxy). GNU Autotools build. | B (source-confirmed) |
| **Structure Layer** | Dependency Discovery; Module Discovery; API Discovery; Database Discovery; Configuration Discovery | 8 modules: `radiusd`, `auth`, `client`, `config`, `db`, `log`, `utils`, `stats`. 0 existing accounting module. PostgreSQL: 4 tables (`users`, `nas`, `sessions`, `audit_log`). SQLite: 3 cache tables. Config: `radiusd.conf` with section-per-module. | B (source) |
| **Security Layer** | Security Discovery; Authentication Discovery; Authorization Discovery | RADIUS shared secret per-NAS in `nas` table. EAP-PEAP/MSCHAPv2 for Wi-Fi; PAP for VPN. No Accounting-Request signature validation (finding F-RAD-006 — risk). SQL injection mitigated via parameterized queries. | B (source) |
| **Behavior Layer** | Event Discovery; Workflow Discovery; Execution Flow Recovery; Runtime Observation | Auth workflow: `Access-Request → EAP identify → PEAP challenge → Access-Accept/Reject`. Event-driven: libevent handles UDP socket + timer events. 180K requests/day = ~2.08 req/s average, 45 req/s peak. | A (runtime-confirmed) |
| **Analysis Methods** | Static Analysis; Dynamic Analysis; Cross-Validation (triangulation) | Static: `clang-tidy` with 8 checks, 23 warnings. Triangulation: packet capture (tcpdump) confirms UDP port 1812 auth flow matches `radiusd.c` event handler code. Runtime `perf` confirms hot path is `sqlite3_step` (cache lookup). | D (triangulated) |
| **Synthesis** | Architecture Recovery; Knowledge Extraction; Evidence Collection; Documentation; Verification | Recovered: Reactor pattern (libevent) with single-threaded event loop + PostgreSQL connection pool (4 connections). No multi-threading. Signal-based config reload (SIGHUP). Knowledge extracted to `docs/discovery/netauth-knowledge.md`. | D |

### 3.2 Discovery Evidence Sample — Network Protocol Specific

| Fact ID | Statement | Confidence | Evidence Source | Verification Status |
|---|---|---|---|---|
| F-RAD-001 | NetAuth listens on UDP port 1812 for Authentication and 1813 for Accounting (currently unhandled) | A | `tcpdump -i eth0 port 1813` shows packets arriving; `netstat` confirms bind; `radiusd.c` line 142 binds `PF_INET, SOCK_DGRAM` on 1813 | Runtime + source triangulated |
| F-RAD-002 | Existing code has no handler for Accounting-Request (code 4) | B | `radiusd.c` switch on `pkt->code` has cases 1, 2, 3, 11 but no case 4; default path logs "unknown packet type" | Source inspection |
| F-RAD-003 | 340 NAS devices send Accounting-Start, Accounting-Stop, and Accounting-Interim-Update | A | Packet capture from 5 representative APs shows all 3 subtypes; NAS table has 340 entries with `accounting_enabled=1` | Runtime observation |
| F-RAD-004 | PostgreSQL `sessions` table tracks login time but not data volume or session termination | B | `schema/sessions.sql`: columns are `id`, `username`, `nas_ip`, `login_time`, `ip_address`; no `bytes_in`, `bytes_out`, `stop_time` | Source inspection |
| F-RAD-005 | Authentication p99 latency is 34ms under current load | A | Prometheus metric `radius_auth_latency_seconds` p99 = 0.034 over 7 days | Runtime observation |
| F-RAD-006 | Accounting-Request packets are not validated with shared secret (no Message-Authenticator) | B | `client.c` function `verify_packet()` is only called from auth path; accounting path falls through | Source inspection; recorded as security risk |

> **Discovery completeness:** Discovery is goal-directed per DSC-4 — sufficiency for the Mission is the criterion, not full comprehension. Network protocol considerations are discovered through Runtime Observation (packet capture) cross-validated with Static Analysis, per DSC-3 (triangulation). [Ref: DSC-2; DSC-3; DSC-4; EVC-1]

---

## 4. Key Decisions (§35.2)

Decisions are recorded following the nine-field structure from §35.2. [Ref: §35.2 Decision Structure; DEC-1]

### Decision 1: Accounting Data Storage Architecture

| Field | Content |
|---|---|
| **Decision** | Write accounting records to PostgreSQL (master) synchronously for billing-critical data, with a local SQLite ring buffer for resilience during PostgreSQL unavailability. |
| **Decision Context** | Mission requires zero Accounting-Stop packet loss (SC-DATA) and 99.99% availability. Single PostgreSQL instance is a SPOF. SQLite already used for auth cache. |
| **Alternatives** | Alt-A: SQLite only (local storage, no external dependency). Alt-B: PostgreSQL only (simpler, SPOF risk). Alt-C: PostgreSQL + SQLite buffer (selected). |
| **Evidence** | F-RAD-004 (existing `sessions` table schema). F-RAD-005 (latency headroom: 34ms used, 50ms budget). Impact analysis: Alt-A complicates billing aggregation across 2 nodes. Alt-B risks data loss on PostgreSQL outage. Alt-C adds ~2ms write latency (within budget) and provides resilience. |
| **Impact** | + Zero data loss during PostgreSQL outage (buffer drains on recovery). + Billing aggregation stays centralized. ~ Additional operational complexity: buffer monitoring, drain procedure. − 2ms latency addition (acceptable per latency budget). |
| **Dependencies** | F-RAD-004. Existing SQLite infrastructure. PostgreSQL connection pool (`db` module). |
| **Approval** | Approved by Network Engineering Lead + SRE Lead on 2024-04-10. |
| **Status** | Approved |
| **Superseded By** | — |

### Decision 2: Packet Validation for Accounting

| Field | Content |
|---|---|
| **Decision** | Implement shared-secret validation for Accounting-Request using standard RADIUS Request-Authenticator field (not Message-Authenticator attribute), consistent with RFC 8049 Section 4.1. |
| **Decision Context** | Discovery finding F-RAD-006: accounting packets are not validated. Security requirement: must validate packet origin. Must interoperate with 340 existing access points of mixed vendors. |
| **Alternatives** | Alt-A: Add Message-Authenticator attribute check (RFC 5997). Alt-B: Use Request-Authenticator hash validation per RFC 8049 (selected). Alt-C: Both. |
| **Evidence** | Vendor compatibility test: 3/5 tested AP vendors (Cisco, Aruba, Ubiquiti) do not send Message-Authenticator in Accounting-Request. RFC 8049 Section 4.1 specifies Request-Authenticator validation. Alt-C risks rejecting valid packets from legacy APs. |
| **Impact** | + Compliant with RFC 8049. + Compatible with all 340 existing APs. + Security gap closed (finding F-RAD-006 resolved). − Slightly weaker than Message-Authenticator (accepted risk per context). |
| **Dependencies** | F-RAD-006 (security finding). RFC 8049 compliance requirement. |
| **Approval** | Approved by Security Architect on 2024-04-12. |
| **Status** | Approved |
| **Superseded By** | — |

> **Decision integrity note:** Both decisions are immutable per DEC-3. If either needs change, a new Decision would supersede it. Every implementation below traces to exactly one Decision per DEC-4. [Ref: DEC-3; DEC-4]

---

## 5. Stage Progression (§13.2)

Stage progression follows the mandatory schema from §13.2. [Ref: §13.2 Mandatory Stage Schema] For brevity, two representative stages are shown.

### Stage 1: Protocol Characterization

| Field | Content |
|---|---|
| **Entry Criteria** | Discovery Complete for RADIUS protocol handling. Mission active with expected deliverable #5 (characterization tests). |
| **Inputs** | Discovery facts F-RAD-001 through F-RAD-006; packet capture files; RFC 8049 specification. |
| **Activities** | Capture Accounting packets from 5 representative AP vendors; analyze packet structure against RFC 8049; document vendor variations; write characterization tests for packet parsing; validate with `radtest` and `radclient`. |
| **Outputs** | `tests/protocol/test_accounting_packets.c` — Authoritative artifact. `docs/protocol/vendor-variations.md` — Authoritative artifact. Packet capture archive (Generated). |
| **Evidence Produced** | 47 packet samples analyzed. 3 vendor variations documented (Cisco includes ` Cisco-AVPair`; Aruba includes `Aruba-User-Role`; Ubiquiti minimal attributes). `radtest` validation: 12/12 RFC 8049 test vectors pass. |
| **Exit Criteria** | All RFC 8049 test vectors pass. Vendor variation document reviewed. Packet parser handles all 3 vendor formats. |
| **Verification Criteria** | `radtest`/`radclient` output (Test). Review record for vendor variation doc (Inspection). [Ref: §16.2] |
| **Review Type** | Walkthrough per §15.1 (early-stage protocol understanding). [Ref: §15.1] |

### Stage 2: Accounting Module Implementation

| Field | Content |
|---|---|
| **Entry Criteria** | Stage 1 exit criteria verified. Decision 1 and Decision 2 are Approved. Impact analysis record IMP-RAD-001 covers `radiusd`, `db`, and `client` modules. Repository Readiness gate "Implementation Ready" satisfied per §41.2. |
| **Inputs** | Decisions DEC-RAD-001, DEC-RAD-002; characterization test suite; existing `radiusd.c`, `db.c`, `client.c` source; RFC 8049 specification. |
| **Activities** | Implement `accounting.c` module with packet handler, PostgreSQL writer, SQLite buffer; integrate into `radiusd.c` event loop; write unit tests for packet validation, buffer drain, edge cases; run latency regression test; run availability failover test. |
| **Outputs** | `src/accounting.c`, `src/accounting.h` (Authoritative). Updated `src/radiusd.c`, `src/db.c` (Authoritative). Unit test suite (Authoritative). Latency regression report. Failover test report. |
| **Evidence Produced** | Unit tests: 34/34 pass. RFC 8049 test vectors: 12/12 pass. Latency: p99 41ms with accounting enabled (under 50ms budget). Failover: 0 packets lost during 30-second PostgreSQL outage (SQLite buffer drains on recovery). |
| **Exit Criteria** | All unit tests pass. RFC test vectors pass. Latency p99 <50ms. Zero packet loss during failover. Code review completed. Static analysis clean. |
| **Verification Criteria** | Unit test report (Test). `radtest` output (Test). Latency benchmark (Demonstration). Failover test log (Test). Static analysis report (Analysis). [Ref: §16.2] |
| **Review Type** | Inspection per §15.1 (for packet validation logic — security-critical). [Ref: RV-1] |

> **Stage rules observed:** SG-1 — exit criteria verified before stage declared complete. SG-2 — outputs classified per Artifact Authority Model (§11.1). SG-4 — validation responsibility (test authoring + failover test) kept distinct from implementation per PR-8. [Ref: SG-1; SG-2; SG-4]

---

## 6. Conformance Assertion (§16.5)

The conformance assertion is recorded following §16.5. [Ref: §16.5 Conformance / Certification Concept; FR-15; VL-1, VL-4]

| Field | Value |
|---|---|
| **Project** | NetAuth RADIUS Accounting |
| **Standard Version** | SES v0.4.0 |
| **Assertion Date** | 2024-06-20 |
| **Asserted By** | Network Engineering Lead (with Independent Reviewer confirmation per RV-4) |
| **Conformance Scope** | Partial conformance — RADIUS Accounting module only. Authentication and authorization modules not assessed. |
| **Evidence Summary** | All required artifacts present: Mission (8 elements, §32.2), 2 Decisions (9 fields each, §35.2), Discovery record (§25.3 activities with confidence/provenance, §26.2), Stage records (§13.2 schema), Review records (§15.1 types), Validation records (§16.2 methods). Protocol-specific discovery triangulated via packet capture + source analysis. |
| **Pass/Fail Verdict** | **PASS** — All applicable SES requirements for this Mission scope are satisfied. |
| **Cited Evidence** | Mission record: MS-RAD-001. Decisions: DEC-RAD-001, DEC-RAD-002. Discovery: DSC-RPT-RAD-001. Stages: STG-RAD-001, STG-RAD-002. Reviews: RV-PROTO-001, RV-IMPL-RAD-001. Validation: VAL-RPT-RAD-001. |
| **Limitations** | Conformance limited to Accounting module. Full NetAuth conformance would require separate Missions for authentication, authorization, and high availability. Security finding F-RAD-006 resolved by Decision 2. |

> **Verifiability note:** The assertion cites specific evidence records per VL-4 and names the standard version per VS-3. The verdict is objective pass/fail per VL-1. [Ref: VL-1; VL-4; VS-3]

---

## 7. SES Sections Cited in This Example

| SDD Section | How Demonstrated |
|---|---|
| §4.2 (RADIUS / network servers domain) | Example context: fictional NetAuth RADIUS server |
| §11.1 (Artifact Authority Model) | Outputs classified as Authoritative/Generated |
| §11.2 (Artifact Metadata) | Metadata header on this example document |
| §11.3 (Contract Specification) | Aggregation API contract (OpenAPI) |
| §13.2 (Mandatory Stage Schema) | Two stages with all 8 fields populated |
| §15.1 (Review Types) | Walkthrough + Inspection applied |
| §16.2 (Verification Methods) | Test, Analysis, Demonstration used |
| §16.5 (Conformance Assertion) | Recorded verdict with evidence |
| §25.3 (Discovery Activities) | All 6 activity layers demonstrated |
| §26.2 (Confidence Levels) | Facts graded A–E |
| §32.2 (Mission Structure) | Mission with all 8 elements |
| §34.2 (Operations) | Allowed Operations drawn from closed set |
| §35.2 (Decision Structure) | Two decisions with all 9 fields |
| §41.2 (Readiness Gates) | Implementation Ready gate referenced |

---

> **End of Example.** This document is NON-NORMATIVE and exists solely to demonstrate SES application. [Ref: §24 Phase 9; §10.3 Authority Rule]
