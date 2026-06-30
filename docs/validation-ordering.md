# Validation Ordering

> **Authority Class:** Authoritative
> **SDD Authority:** §16.3
> **Status:** Draft
> **Version:** 0.4.0
> **Phase:** Phase 6

## 1. Purpose

This document defines the **validation ordering principle** for projects governed by the Software Engineering Standard (SES). It specifies the sequence in which validation activities **SHALL** be performed to maximize feedback speed and minimize the cost of defect detection. [Ref: §16.3]

This document is applicable to **software produced under** the standard. The ordering is presented as **converged practice**, not as a formally mandated sequence. [Ref: §16.3 honesty marker]

## 2. Validation Layers

The SES recognizes the following validation layers, ordered from fastest feedback to slowest: [Ref: §16.3]

| Order | Layer | Feedback Speed | Purpose |
|---|---|---|---|
| 1 | **Static analysis** | Fastest | Detect structural defects without execution |
| 2 | **Unit** | Fast | Verify individual components in isolation |
| 3 | **Integration** | Fast-medium | Verify component interactions |
| 4 | **Contract** | Medium | Verify interface agreements across boundaries |
| 5 | **Regression** | Medium | Verify that changes do not break existing behavior |
| 6 | **System / E2E** | Slow-medium | Verify end-to-end system behavior |
| 7 | **Non-functional (performance / security / resilience)** | Slow | Verify quality attributes under load or stress |
| 8 | **Runtime verification (canary + observability)** | Slowest | Verify behavior in production-like environments |
| 9 | **Review** | Parallel | Human/criteria-based examination (§15) |

## 3. Ordering Principle (fast-feedback-first)

The SES **SHALL** adopt a **fast-feedback-first** validation ordering. [Ref: §16.3]

The principle requires that:

- **OF-1.** Validation layers that execute faster and cost less **SHALL** be executed before layers that execute slower and cost more. [Ref: §16.3]
- **OF-2.** Defects **SHOULD** be detected at the earliest possible layer. [Ref: Converged practice — shift-left testing]
- **OF-3.** A layer **MAY** be skipped only if its concerns are demonstrably covered by another layer, and this coverage **MUST** be recorded as evidence. [Ref: VL-3]
- **OF-4.** The ordering **MUST NOT** be interpreted as a claim that later layers are optional; all applicable layers **MUST** be executed unless explicitly waived with evidence. [Ref: §16.3]

## 4. Layer Definitions

### 4.1 Static Analysis

Static analysis is the examination of source code or artifacts without execution. It is the fastest feedback layer because it requires no runtime environment. [Ref: §16.3]

Static analysis **MUST** detect, at minimum: syntax errors, type violations, style deviations (where project-defined), and structural anomalies. SDD does not specify the exact static analysis tools or rulesets. [Ref: §16.3]

### 4.2 Unit

Unit validation verifies individual components (functions, classes, modules) in isolation. It is the foundational execution-based verification layer. [Ref: §16.3]

Unit validation **MUST** be automated, deterministic, and fast enough to run on every change. [Ref: PR-9]

### 4.3 Integration

Integration validation verifies that components interact correctly. It follows unit validation because integration failures are only meaningful when units are individually correct. [Ref: §16.3]

Integration validation **MUST** verify: component wiring, data flow across boundaries, and protocol compliance. [Ref: §16.3]

### 4.4 Contract

Contract validation verifies interface agreements across system boundaries. It follows integration validation because contracts govern cross-boundary behavior. [Ref: §16.3]

Contract validation **MUST** verify: API request/response compliance, schema conformance, and semantic agreement per defined contracts. [Ref: §11.3 Contract Specification]

### 4.5 Regression

Regression validation verifies that changes do not break existing behavior. It follows contract validation because regressions are detected by comparing current behavior against established baselines. [Ref: §16.3]

Regression validation **MUST** be executed whenever implementation changes occur. [Ref: PR-9]

### 4.6 System / E2E

System validation (end-to-end) verifies complete user-facing or system-facing scenarios. It is slower than prior layers because it exercises the full system stack. [Ref: §16.3]

System validation **MUST** verify: complete workflows, user journeys, and cross-system scenarios. [Ref: §16.3]

### 4.7 Non-functional (Performance / Security / Resilience)

Non-functional validation verifies quality attributes under load, stress, or adversarial conditions. It is slower than functional validation because it requires specialized environments and measurements. [Ref: §16.3]

Non-functional validation **MUST** verify: performance characteristics, security posture, and resilience behavior per the project's non-functional requirements. [Ref: §9]

### 4.8 Runtime Verification (Canary + Observability)

Runtime validation verifies behavior in production or production-like environments using canary deployments and observability signals. It is the slowest layer because it operates on live systems. [Ref: §16.3]

Runtime validation **MUST** verify: production behavior matches expected behavior, observability signals (metrics, logs, traces) indicate health, and canary metrics pass defined thresholds. [Ref: §16.3]

### 4.9 Review

Review is a **human/criteria-based examination** that runs **in parallel** with the automated validation layers. It is complementary to, and **MUST NOT** be merged with, automated validation. [Ref: §15.3; PR-8]

Review **MUST** be performed per the Review Model (§15), against explicit, written criteria (RV-3). [Ref: §15.2 RV-3]

## 5. Honesty Marker (converged practice)

The *existence* of these verification layers is standardized (ISO/IEC/IEEE 29119, ISO/IEC/IEEE 1012). The *specific ordering and weighting* is **converged practice, not a formal standard**. [Ref: §16.3 honesty marker]

This **MUST** be presented as such in all SES documents and to all project teams. The ordering is the SES-adopted model, consistent with cited evidence, but it is not claimed as an ISO-mandated sequence. [Ref: §16.3; FR-12]

## 6. Competing Weightings

Two competing weightings for validation investment are recognized by the SES: [Ref: §16.3]

### 6.1 Testing Pyramid (Cohn / Fowler)

The testing pyramid advocates: many unit tests, fewer integration tests, fewer system tests. It prioritizes fast, cheap feedback and stable tests. [Ref: Cohn, *Succeeding with Agile*; Fowler, "TestPyramid"]

### 6.2 Testing Trophy (Dodds)

The testing trophy advocates maximum investment in integration tests, with unit tests for complex logic and fewer E2E tests. It prioritizes testing realistic user scenarios. [Ref: Dodds, "Testing Trophy"]

### 6.3 SES Position

The SES **MUST** present both weightings and context-bind the choice per PR-12: [Ref: §16.3; PR-12]

- Projects with high stability requirements and complex domain logic **MAY** weight unit tests more heavily (pyramid).
- Projects with high integration complexity and fewer domain edge cases **MAY** weight integration tests more heavily (trophy).
- Neither weighting **MAY** be mandated as universal; the choice **MUST** be justified per context. [Ref: PR-12]

## 7. Completion Criteria

This validation ordering document is complete when:

- **CC-1.** The fast-feedback-first ordering principle is defined. [Ref: §16.3]
- **CC-2.** All nine validation layers are enumerated in order. [Ref: §16.3]
- **CC-3.** The honesty marker (converged practice, not formal standard) is stated. [Ref: §16.3]
- **CC-4.** Competing weightings (pyramid vs trophy) are presented and context-bound. [Ref: §16.3; PR-12]
- **CC-5.** Every normative rule cites its SDD authority. [Ref: FR-11]
