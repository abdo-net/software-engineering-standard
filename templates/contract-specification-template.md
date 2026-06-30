# Contract Specification Template

---

## Artifact Metadata

| Field | Value |
|---|---|
| **Artifact ID** | [CONTRACT_ID] |
| **Artifact Type** | Contract Specification [Ref: §11.3] |
| **Authority Class** | Authoritative [Ref: §11.1] |
| **Object Type** | Artifact (Knowledge — Contract) [Ref: §42.2, §14.2] |
| **Owner** | [OWNER] [Ref: §11.2] |
| **Version** | [VERSION] [Ref: §18] |
| **Status** | [STATUS] [Ref: §11.2] |
| **Format Agnostic Note** | This template is format-agnostic per CN-1; the contract MAY be expressed in OpenAPI, AsyncAPI, Protocol Buffers, or any other agreed format [Ref: §14.2, CN-1] |
| **Immutability Rule** | Changes to contracts MUST pass through governance and versioning per KN-4 [Ref: KN-4] |
| **Created Timestamp** | [TIMESTAMP] [Ref: §26.3] |
| **Decision References** | [DECISION_REFERENCE] [Ref: §43.2] |

---

## 1. Contract Identity

> Field definition per §11.3: Contract Specification — the agreed interface + semantics across a boundary [Ref: §11.3].
> Normative rule: INT-4: Every API MUST have a contract [Ref: §40.1, INT-4].

**Contract Name:** [CONTRACT_NAME]

**Contract Identifier:** [CONTRACT_ID]

**Contract Type:** [CONTRACT_TYPE]

Allowed values: Synchronous / Asynchronous / Data / Configuration / Security / Other

**Interface Format:** [INTERFACE_FORMAT]

Allowed values per §14.2: OpenAPI / AsyncAPI / Protocol Buffers (proto) / gRPC / Custom / Other

**Format Version:** [FORMAT_VERSION]

---

## 2. Interface Definition

> Field definition per §14.2: Contracts are agreed interfaces + semantics across boundaries [Ref: §14.2].
> This section SHALL contain the actual interface definition, expressed in the chosen format.

**Interface Description:** [INTERFACE_DESCRIPTION]

**Interface Location (repository path or inline):** [INTERFACE_LOCATION]

**Interface Definition:**

```
[INTERFACE_DEFINITION_BODY]
```

**Endpoint / Channel Definitions:** [ENDPOINT_OR_CHANNEL_DEFINITIONS]

**Message / Payload Schemas:** [MESSAGE_OR_PAYLOAD_SCHEMAS]

**Authentication / Authorization Requirements:** [AUTH_REQUIREMENTS]

---

## 3. Semantics

> Field definition per §11.3: The agreed semantics across the boundary [Ref: §11.3].
> Normative rule: CPM-1: Every comparison MUST produce engineering evidence, never subjective judgment [Ref: §37.3, CPM-1].

**Behavioral Semantics:** [BEHAVIORAL_SEMANTICS]

**Preconditions:** [PRECONDITIONS]

**Postconditions:** [POSTCONDITIONS]

**Error Conditions:** [ERROR_CONDITIONS]

**Error Responses:** [ERROR_RESPONSES]

**Ordering / Sequencing Rules:** [ORDERING_RULES]

**Idempotency:** [IDEMPOTENCY_GUARANTEE]

**Consistency Model:** [CONSISTENCY_MODEL]

**Rate Limiting / Throttling:** [RATE_LIMITING_RULES]

**Deprecation Policy:** [DEPRECATION_POLICY] [Ref: VS-6, RFC 8594]

---

## 4. Version

> Field definition per §18: Contracts SHALL carry a semantic version [Ref: §18].

**Current Version:** [CURRENT_VERSION]

**Version History:**

| Version | Date | Change Description | Change Reference |
|---|---|---|---|
| [V_1] | [V_1_DATE] | [V_1_CHANGE] | [V_1_REF] |
| [V_2] | [V_2_DATE] | [V_2_CHANGE] | [V_2_REF] |
| [V_N] | [V_N_DATE] | [V_N_CHANGE] | [V_N_REF] |

**Breaking Changes Since Last Version:** [BREAKING_CHANGES]

**Migration Notes:** [MIGRATION_NOTES] [Ref: VS-4]

---

## 5. Owner

> Field definition per §11.2: Every artifact SHALL carry an owner [Ref: §11.2].

**Contract Owner:** [OWNER_NAME]

**Owner Contact:** [OWNER_CONTACT]

**Owning Team / Organization:** [OWNING_TEAM]

**Consumer(s):** [CONSUMER_LIST]

**Provider:** [PROVIDER_NAME]

---

## 6. Comparison Pairs

> Field definition per §37.2: The model SHALL support comparison between defined pairs [Ref: §37.2].
> This section SHALL define which comparison pairs apply to this contract.

| Comparison Pair (§37.2) | Applicable | Evidence Produced By | Confidence Level |
|---|---|---|---|
| Implementation vs Contract | [IMPL_VS_CONTRACT_APPLICABLE] | [IMPL_VS_CONTRACT_EVIDENCE] | [IMPL_VS_CONTRACT_CONFIDENCE] |
| API vs Documentation | [API_VS_DOC_APPLICABLE] | [API_VS_DOC_EVIDENCE] | [API_VS_DOC_CONFIDENCE] |
| System vs Documentation | [SYS_VS_DOC_APPLICABLE] | [SYS_VS_DOC_EVIDENCE] | [SYS_VS_DOC_CONFIDENCE] |
| Version vs Version | [VER_VS_VER_APPLICABLE] | [VER_VS_VER_EVIDENCE] | [VER_VS_VER_CONFIDENCE] |
| Runtime vs Source | [RUN_VS_SRC_APPLICABLE] | [RUN_VS_SRC_EVIDENCE] | [RUN_VS_SRC_CONFIDENCE] |

**Comparison Results Reference:** [COMPARISON_RESULTS_ID] [Ref: §37]

**Divergence Handling:** [DIVERGENCE_HANDLING] [Ref: CPM-3, §37.3]

---

## 7. Governance & Traceability

> Normative rule: KN-4: Contracts and invariants are authoritative and changes MUST pass through governance + versioning [Ref: KN-4, §14.3].

**Authorizing Decision:** [AUTHORIZING_DECISION_ID] [Ref: §35]

**Traceability Links:** [TRACEABILITY_LINKS] [Ref: §48]

**Review Record Reference:** [REVIEW_RECORD_ID] [Ref: §15]

**Related Invariants:** [RELATED_INVARIANT_IDS] [Ref: §40.1]

**Related Contracts:** [RELATED_CONTRACT_IDS]

**Related Requirements:** [RELATED_REQUIREMENT_IDS]

**Evidence References:** [EVIDENCE_REFERENCES] [Ref: §28]

---

## 8. Change Log

> Normative rule: VS-2: Every change MUST be recorded in a changelog [Ref: §18, VS-2].

| Version | Date | Author | Change | Governance Reference |
|---|---|---|---|---|
| [CHG_1_VER] | [CHG_1_DATE] | [CHG_1_AUTHOR] | [CHG_1_DESC] | [CHG_1_GOV_REF] |
| [CHG_2_VER] | [CHG_2_DATE] | [CHG_2_AUTHOR] | [CHG_2_DESC] | [CHG_2_GOV_REF] |
| [CHG_N_VER] | [CHG_N_DATE] | [CHG_N_AUTHOR] | [CHG_N_DESC] | [CHG_N_GOV_REF] |
