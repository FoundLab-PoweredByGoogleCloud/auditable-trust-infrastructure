# The Category Invariants

> **ATI makes proof durable and data destructible.** The proof survives. The payload does not have to.

Auditable Trust Infrastructure exists because regulated AI systems must satisfy two properties that normally conflict. They must **preserve evidence** — what was requested, what policy was active, what decision was made, why, and whether the execution path was authorized — and they must **preserve privacy** — sensitive personal data must stay controllable, minimizable, and technically removable from access paths when retention authority expires or an elimination event is triggered.

ATI resolves the conflict by separating the *proof of execution* from the *payload that made the execution possible*. The result is not a better log. It is a different infrastructure category, defined by the ten invariants below. A deployment that violates any of them is not an ATI deployment.

---

### Invariant 1 — Evidence must be separable from data

An ATI system must never require raw sensitive data to remain readable in order to prove that a regulated decision occurred. The evidence plane stores **commitments, not plaintext**.

It **may** store: canonical hashes, policy-snapshot hashes, model/runtime identifiers, decision identifiers, sequencing metadata, signed evidence envelopes, airlock certificates, and retention-state references.

It **must not** store: raw prompts, raw model outputs containing PII, retrieved context containing PII, plaintext identifiers, decryptable key material, embedded secrets, or operational logs that reconstruct the sensitive payload.

> The system preserves the proof of the decision, not the personal data used to produce it.

In REX Guard this is the **Non-Coresidence Invariant**: raw PII and cryptographic key material must never be committed to the immutable evidence ledger.

### Invariant 2 — Proof must survive deletion

ATI does not make immutable storage mutable — that would destroy audit integrity. Instead, it makes personal data **cryptographically detachable** from immutable proof.

On a lawful deletion, expiration, or retention-state transition, the system disables and/or schedules destruction of the key material required to decrypt the sensitive payload. The immutable evidence remains intact; the payload becomes technically inaccessible through the controlled system.

```text
disable_or_destroy(key_material)  =>  payload_access = false
                                       ledger_integrity = true
```

The ledger can still prove a decision occurred, under which policy version, against which payload hash, on which runtime, at which sequence position, sealed in which evidence envelope — but it cannot reconstruct the payload. This is ATI's answer to the Retention Paradox: **deletion affects access to sensitive data; it does not erase the existence of the regulated decision.**

> **Precision required (verified against Cloud KMS, Jun 2026).** Key destruction is **scheduled, not immediate**: Cloud KMS holds the version in a *scheduled-for-destruction* state for a configurable window (**default 30 days**), during which it can be **restored**. After the window, destruction is irreversible and data encrypted with that version cannot be decrypted — the official term is *crypto-shredded*. After the window, logical deletion begins and key material may persist in Google systems for up to **45 days after the scheduled destruction time** (i.e., after the 30-day window — **not** a 45-day total). For an immediate access cut, the system **disables** the key version (effective at once) and then schedules destruction; ATI documents must not claim instant cryptographic erasure.

### Invariant 3 — Immutable proof must not contain the means of disclosure

Encryption alone is insufficient if the ciphertext, key reference, key state, and reconstruction metadata are co-located on the same immutable surface. ATI requires a strict split:

```text
Immutable Evidence Plane  !=  Mutable Key Plane
Immutable Evidence Plane  !=  Sensitive Payload Store
Immutable Evidence Plane  !=  Operational Analytics Plane
```

The evidence plane proves. The key plane governs access. The payload plane stores ciphertext. The analytics plane observes aggregate behavior. No single plane is allowed to become a privacy cemetery.

### Invariant 4 — Every decision must be reproducible without retaining the raw payload

Governance fails when an institution can only say "the model said so." A valid ATI proof binds: the canonical payload hash, the active policy hash, the model/runtime identifier, the decision-function version, the retention-state version, a timestamp/sequencing proof, the final decision, the rationale envelope, and the proof signature. An auditor can verify the institution followed the required path **even when the original sensitive payload is no longer decryptable**. The proof remains inspectable; the private data does not remain exposed.

### Invariant 5 — Policy must be versioned, signed, and bound to execution time

Policy is not documentation; in ATI it is **executable state**. Every regulated decision binds to the exact policy version active at execution: policy version, policy hash, approver/signer set, runtime version, effective timestamp, decision node or rule reference, and override status. A decision without policy binding is not auditable; a policy without versioning is not governance; a governance layer without cryptographic binding is process theater.

### Invariant 6 — Fail-open behavior is prohibited

If any required component cannot validate, seal, sequence, or enforce the decision, the inference path must stop.

```text
required_control_unavailable  =>  deny_or_defer
```

Prohibited: audit unavailable ⇒ allow; policy unavailable ⇒ allow; key-plane unavailable ⇒ allow; evidence write failed ⇒ allow; consent unknown ⇒ allow. Fail-closed execution is the operational boundary between AI governance and AI theater.

### Invariant 7 — Intelligence must not escape the protected perimeter

Contextual intelligence may enrich a decision but must not become a covert exfiltration channel. Risk inference, anomaly detection, and model monitoring execute **within** the protected boundary defined by the deployment profile. The system must prevent raw PII leaving the perimeter, prompts being retained as analytics artifacts, model traces becoming shadow data lakes, observability logs becoming re-identification surfaces, and risk outputs embedding sensitive payload fragments. The intelligence plane may inspect, classify, trigger policy evaluation, and emit aggregate risk signals — it must not become an uncontrolled copy of the data plane.

### Invariant 8 — Auditability must be causal, not decorative

A dashboard is not evidence; a log line is not governance; a policy PDF is not enforcement. ATI requires **causal** auditability — tracing a decision from fact, through state, through policy, through execution, into sealed proof.

```text
Fact -> State -> Policy -> Decision -> Effect -> Proof
```

The proof must answer what fact entered, what state existed before, what policy was active, what threshold fired, what decision was emitted, what effect was applied, what evidence was sealed, and what data (if any) remained decryptable afterward. Without causality, auditability is just storage.

### Invariant 9 — Scoring must not bypass prohibited-party controls

Risk scoring cannot sanitize prohibited activity. Hard exclusion checks — sanctions, prohibited parties, legal blocks, explicit deny-lists, mandatory regulatory constraints — execute **before** any reputational scoring influences a decision.

```text
hard_prohibition_check
  -> consent_and_authority_check
  -> evidence_admissibility_check
  -> contextual_risk_inference
  -> reputational_scoring
  -> deterministic_decision
  -> sealed_proof
```

A high reputation score must never override a non-negotiable legal prohibition.

### Invariant 10 — ATI must preserve institutional accountability

ATI does not eliminate accountability; it makes accountability **executable**. Cryptography does not replace legal judgment, regulatory interpretation, or institutional responsibility. Every deployment must distinguish technical proof from legal conclusion, technical inaccessibility from statutory erasure, policy execution from legal advice, evidence preservation from regulatory sufficiency, and model output from institutional decision.

> ATI is not a compliance opinion. ATI is the infrastructure that makes a compliance position technically testable.

---

[⬅️ Back to the Category Overview](./README.md) · [ATI Reference Stack](../reference-architecture/ati-reference-stack.md) · [ATI Index](../README.md)
