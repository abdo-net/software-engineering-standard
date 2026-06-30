# Example: SES Applied to an Analysis System — InsightFlow Analytics Platform

> **NON-NORMATIVE** — This document is a worked example for illustrative purposes only.
> It demonstrates how the Software Engineering Standard (SES) MAY be applied to a project
> in the analysis systems domain. [Ref: §4.2 Domains the SES Must Cover; §24 Phase 9 — Worked examples]
> This example introduces no new rules and extends no architecture.

---

## Artifact Metadata

| Field | Value |
|---|---|
| **Object ID** | EX-ANL-001 |
| **Object Type** | Example |
| **Authority Class** | Generated |
| **Owner** | SES Phase 9 — Example Writer |
| **Lifecycle State** | COMPLETED |
| **Status** | Accepted |
| **Version** | 0.1.0 |
| **Parent Objects** | SES v0.4.0 |
| **Repository Location** | `examples/example-analysis.md` |
| **Generated From** | SDD v0.4.0 §32.2, §25.3, §35.2, §13.2, §16.5 |

---

## 1. Fictional Project Context

**Project name:** InsightFlow Analytics Platform (codename: "InsightFlow")
**Domain:** Data analysis system — real-time stream processing, aggregation, and visualization
**Context:** A 3-year-old analytics platform processing 2.4M events/minute from IoT sensors. Built in Python (Apache Spark Streaming) with a PostgreSQL metadata store, Redis cache, and a React frontend. The organization needs to add anomaly detection capabilities while maintaining sub-second query latency for dashboard users.

---

## 2. Mission Creation (§32.2)

The Mission is created following the eight-element structure mandated by §32.2. [Ref: §32.2 Mission Structure; MIS-1, MIS-2]

| Mission Element | Content |
|---|---|
| **Objective** | Add statistical anomaly detection to InsightFlow for 12 KPI streams, maintaining sub-second dashboard query latency and without dropping events from the existing ingestion pipeline. |
| **Scope** | In scope: Anomaly detection engine design and implementation; statistical model training pipeline; integration with existing Spark Streaming jobs; dashboard alert UI component; characterization of current ingestion throughput. Out of scope: Machine learning model retraining automation; mobile push notifications; changes to data collection agents. |
| **Constraints** | CN-LATENCY: Dashboard p99 query latency must remain <1s. CN-THROUGHPUT: Ingestion pipeline must sustain ≥2.4M events/minute. CN-DATA: Training data limited to 90 days retention (storage policy). CN-STACK: Must use existing Python/Spark infrastructure. |
| **Expected Deliverables** | (1) ADR for anomaly detection algorithm selection; (2) Anomaly detection microservice specification; (3) Integration design for Spark Streaming; (4) Characterization test report for ingestion throughput; (5) Performance benchmark report; (6) Updated API contracts for alert endpoints. |
| **Success Criteria** | SC-DETECT: ≥95% precision on known anomaly patterns (test set of 47 historical incidents). SC-LATENCY: p99 dashboard query <1s under load. SC-THROUGHPUT: Zero events dropped at 2.4M events/minute. SC-COVERAGE: All 12 KPI streams monitored. |
| **Allowed Operations** | DISCOVER, ANALYZE, TRACE, VERIFY, DOCUMENT, COMPARE, PLAN, IMPLEMENT, VALIDATE, REVIEW [Ref: §34.2 Operations and Governing Sections] |
| **Forbidden Operations** | Direct modification of raw event storage schema; changes to existing aggregation logic without impact analysis; deployment without performance validation. |
| **Evidence Requirements** | All facts carry confidence level per §26; all decisions recorded per §35; throughput claims validated by benchmark; all performance tests reproducible. |

> **Mission validation note:** The Mission above defines all eight elements required by MIS-2. Allowed Operations are drawn from the closed set in §34.2 per MIS-3. [Ref: MIS-2; MIS-3]

---

## 3. Discovery Activities (§25.3)

Discovery is performed following the mandated activity set from §25.3. [Ref: §25.3 Mandated Discovery Activities; DSC-1, DSC-2, DSC-3]

### 3.1 Discovery Results Summary

| Activity Layer | Activities Performed | Key Findings | Confidence |
|---|---|---|---|
| **Inventory Layer** | Asset Inventory; Repository Inventory; Technology Detection; Build System Detection; Runtime Environment Detection | Polyrepo: 4 repos (`ingestion`, `aggregation`, `api`, `frontend`). Python 3.10, Spark 3.4, PostgreSQL 15, Redis 7, React 18. Poetry + Docker Compose local, Kubernetes production. AWS EKS cluster (6 nodes). | B (source-confirmed) |
| **Structure Layer** | Dependency Discovery; Module Discovery; API Discovery; Database Discovery; Configuration Discovery | Ingestion repo: 12 Python modules. Aggregation repo: 8 Spark jobs. API repo: FastAPI with 34 endpoints. PostgreSQL: 67 tables. Redis: key patterns `agg:*` and `session:*`. API depends on PostgreSQL + Redis. | B (source) |
| **Security Layer** | Security Discovery; Authentication Discovery; Authorization Discovery | API uses OAuth2 (Auth0). Role-based: `ANALYST`, `ADMIN`, `SYSTEM`. Spark jobs use IAM role-based auth to S3. No mTLS between services. | B/C (mixed) |
| **Behavior Layer** | Event Discovery; Workflow Discovery; Execution Flow Recovery; Runtime Observation | Ingestion workflow: `Kafka → Spark Streaming → S3 (parquet) → Aggregation Job → PostgreSQL/Redis`. Dashboard query path: `React → API → PostgreSQL/Redis`. Peak: 2.7M events/min (observed). | A (runtime-confirmed) |
| **Analysis Methods** | Static Analysis; Dynamic Analysis; Cross-Validation (triangulation) | PyCharm static analysis: 312 type-check warnings. Triangulation: Spark UI confirms DAG structure from static code analysis. Runtime JMX confirms heap usage patterns match static allocation analysis. | D (triangulated) |
| **Synthesis** | Architecture Recovery; Knowledge Extraction; Evidence Collection; Documentation; Verification | Recovered: Lambda architecture (batch + speed layers). Speed layer: Spark Streaming. Batch layer: nightly Spark jobs. Serving layer: FastAPI + PostgreSQL/Redis. Knowledge extracted to `docs/discovery/insightflow-knowledge.md`. | D |

### 3.2 Discovery Evidence Sample

| Fact ID | Statement | Confidence | Evidence Source | Verification Status |
|---|---|---|---|---|
| F-101 | Ingestion pipeline uses Spark Streaming with Kafka source | B | `ingestion/jobs/streaming.py` contains `KafkaUtils.createDirectStream` | Source inspection |
| F-102 | API layer has 34 endpoints in 4 router modules | B | `api/routers/` contains 4 files with 34 `@router.*` decorators | Source inspection |
| F-103 | Peak observed throughput is 2.7M events/minute | A | Grafana dashboard `ingestion.throughput` shows 2.7M max over 30 days | Runtime observation |
| F-104 | Dashboard query p99 latency is 780ms under normal load | A | Datadog APM trace metrics for `GET /api/v1/dashboard` | Runtime observation |
| F-105 | PostgreSQL `events_raw` table has 90-day retention via partition drop | B | `schema/events.sql` contains `PARTITION BY RANGE (event_date)` with 90-day policy | Source inspection |

> **Discovery completeness:** Discovery is goal-directed per DSC-4 — sufficiency for the Mission is the criterion, not full comprehension. Discovery evidence carries provenance and confidence per DSC-2 and EVC-1. [Ref: DSC-2; DSC-4; EVC-1]

---

## 4. Key Decisions (§35.2)

Decisions are recorded following the nine-field structure from §35.2. [Ref: §35.2 Decision Structure; DEC-1]

### Decision 1: Anomaly Detection Algorithm

| Field | Content |
|---|---|
| **Decision** | Use Isolation Forest for anomaly detection (via scikit-learn), deployed as a separate microservice called `anomaly-detector`, invoked asynchronously from the Spark Streaming job via Redis pub/sub. |
| **Decision Context** | Mission requires statistical anomaly detection on 12 KPI streams. Latency constraint (<1s dashboard queries) means detection cannot run synchronously in the API path. Must work with 90-day data retention limit. |
| **Alternatives** | Alt-A: LSTM neural network (PyTorch). Alt-B: Statistical z-score with sliding window. Alt-C: Isolation Forest (selected). |
| **Evidence** | F-105 (90-day data limit — insufficient for deep learning). Impact analysis: Alt-A requires >90 days for good accuracy, violates CN-DATA. Alt-B is simpler but produces 3x false positives on seasonal data (benchmark test). Alt-C achieves 96% precision on test set with 90-day window. |
| **Impact** | + 96% precision exceeds SC-DETECT target. + Asynchronous design does not add latency to API path. ~ New operational component (`anomaly-detector`) to monitor. − Requires Redis pub/sub (already available per F-102). |
| **Dependencies** | F-102 (Redis available). F-103 (throughput baseline). F-105 (data retention limit). |
| **Approval** | Approved by Data Science Lead + Engineering Lead on 2024-06-10. |
| **Status** | Approved |
| **Superseded By** | — |

### Decision 2: Integration Pattern — Synchronous vs. Asynchronous

| Field | Content |
|---|---|
| **Decision** | Asynchronous: Spark Streaming publishes events to Redis pub/sub; `anomaly-detector` consumes and publishes alerts back to Redis; API reads alerts for dashboard display. |
| **Decision Context** | CN-LATENCY requires sub-second dashboard queries. Synchronous call to anomaly detector in API path would add unpredictable latency. |
| **Alternatives** | Alt-A: Synchronous (API calls detector directly). Alt-B: Asynchronous via message queue (selected). Alt-C: Embedded in Spark job with alert storage in PostgreSQL. |
| **Evidence** | F-104 (current p99 is 780ms — only 220ms headroom). Benchmark: synchronous call adds 350ms avg latency (exceeds budget). Alt-C couples detection to Spark job lifecycle, preventing independent scaling. |
| **Impact** | + Preserves latency budget. + Detector scales independently. ~ Eventual consistency: alerts appear within 5 seconds of anomaly (acceptable per stakeholders). |
| **Dependencies** | Decision 1 (algorithm choice). F-102 (Redis infrastructure). |
| **Approval** | Approved by Architect on 2024-06-12. |
| **Status** | Approved |
| **Superseded By** | — |

> **Decision integrity note:** Both decisions are immutable per DEC-3. If either needs change, a new Decision would supersede it. Every implementation below traces to exactly one Decision per DEC-4. [Ref: DEC-3; DEC-4]

---

## 5. Stage Progression (§13.2)

Stage progression follows the mandatory schema from §13.2. [Ref: §13.2 Mandatory Stage Schema] For brevity, two representative stages are shown.

### Stage 1: Throughput Characterization

| Field | Content |
|---|---|
| **Entry Criteria** | Discovery Complete for ingestion pipeline. Mission active with expected deliverable #4 (characterization test report). |
| **Inputs** | Discovery facts F-101 through F-105; existing Grafana dashboards; Spark UI metrics. |
| **Activities** | Instrument ingestion pipeline with JMX metrics; run 72-hour load test at 1.0x, 1.1x, 1.2x expected throughput; record event drop count, latency distribution, resource utilization. |
| **Outputs** | `reports/throughput-characterization.md` — Authoritative artifact. JMX metrics export (Generated). Load test configuration (Authoritative). |
| **Evidence Produced** | Throughput at 1.2x (2.88M events/min): zero drops, CPU 78%, memory 82%. Headroom analysis: can sustain 1.35x before drops occur. |
| **Exit Criteria** | 72-hour load test completed. Event drop count = 0 at 1.2x throughput. All metrics recorded with timestamps. |
| **Verification Criteria** | Load test report reviewed. Metrics reproducible from test script. Demonstration: re-run of test script produces comparable results. [Ref: §16.2] |
| **Review Type** | Technical Review per §15.1. [Ref: §15.1] |

### Stage 2: Anomaly Detection Implementation

| Field | Content |
|---|---|
| **Entry Criteria** | Stage 1 exit criteria verified. Decision 1 and Decision 2 are Approved. Impact analysis record IMP-ANL-001 covers all 12 KPI streams. Repository Readiness gate "Implementation Ready" satisfied per §41.2. |
| **Inputs** | Decisions DEC-001, DEC-002; characterization report; `anomaly-detector` service specification; Spark Streaming job source code. |
| **Activities** | Implement `anomaly-detector` microservice; train Isolation Forest on 90-day historical data; integrate Redis pub/sub into Spark Streaming; implement alert API endpoints; write unit + integration tests; run performance validation. |
| **Outputs** | `anomaly-detector/` service code (Authoritative). Updated Spark Streaming job (Authoritative). Alert API contract update (Authoritative). Test suite (Authoritative). Performance benchmark report. |
| **Evidence Produced** | Unit tests: 47/47 pass. Integration tests: 18/18 pass. Precision on test set: 96.2% (47 historical incidents). p99 dashboard latency: 820ms (under 1s budget). Throughput test: zero drops at 2.4M events/min. |
| **Exit Criteria** | All tests pass. Precision ≥95%. Dashboard p99 <1s. Zero event drops at baseline throughput. Code review completed. |
| **Verification Criteria** | Unit/integration test report (Test). Precision calculation on held-out test set (Analysis). Dashboard latency benchmark (Demonstration). Throughput regression test (Test). [Ref: §16.2] |
| **Review Type** | Inspection per §15.1 (for API contract changes). [Ref: RV-1] |

> **Stage rules observed:** SG-1 — exit criteria verified before stage declared complete. SG-2 — outputs classified per Artifact Authority Model (§11.1). SG-4 — validation responsibility (test authoring) kept distinct from implementation per PR-8. [Ref: SG-1; SG-2; SG-4]

---

## 6. Conformance Assertion (§16.5)

The conformance assertion is recorded following §16.5. [Ref: §16.5 Conformance / Certification Concept; FR-15; VL-1, VL-4]

| Field | Value |
|---|---|
| **Project** | InsightFlow Anomaly Detection |
| **Standard Version** | SES v0.4.0 |
| **Assertion Date** | 2024-08-15 |
| **Asserted By** | Engineering Lead (with Independent Reviewer confirmation per RV-4) |
| **Conformance Scope** | Partial conformance — Anomaly detection module and integration with ingestion pipeline only. Frontend visualization and batch layer not assessed. |
| **Evidence Summary** | All required artifacts present: Mission (8 elements, §32.2), 2 Decisions (9 fields each, §35.2), Discovery record (§25.3 activities with confidence/provenance, §26.2), Stage records (§13.2 schema), Review records (§15.1 types), Validation records (§16.2 methods). |
| **Pass/Fail Verdict** | **PASS** — All applicable SES requirements for this Mission scope are satisfied. |
| **Cited Evidence** | Mission record: MS-101. Decisions: DEC-101, DEC-102. Discovery: DSC-RPT-101. Stages: STG-101, STG-102. Reviews: RV-CHAR-001, RV-IMPL-101. Validation: VAL-RPT-101. |
| **Limitations** | Conformance limited to anomaly detection scope. Full InsightFlow platform conformance would require separate Missions for ingestion, aggregation, and frontend modules. |

> **Verifiability note:** The assertion cites specific evidence records per VL-4 and names the standard version per VS-3. The verdict is objective pass/fail per VL-1. [Ref: VL-1; VL-4; VS-3]

---

## 7. SES Sections Cited in This Example

| SDD Section | How Demonstrated |
|---|---|
| §4.2 (analysis systems domain) | Example context: fictional InsightFlow platform |
| §11.1 (Artifact Authority Model) | Outputs classified as Authoritative/Generated |
| §11.2 (Artifact Metadata) | Metadata header on this example document |
| §11.3 (Contract Specification) | Alert API contract as authoritative artifact |
| §13.2 (Mandatory Stage Schema) | Two stages with all 8 fields populated |
| §15.1 (Review Types) | Technical Review + Inspection applied |
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
