# ATI Glossary

The canonical vocabulary of the **Auditable Trust Infrastructure** category. Terms are defined at the level of *what they are* and *why they exist* — not their calibrated interior. Where a term names a mechanism, the definition states the contract, not the construction.

---

### Category & posture

- **ATI (Auditable Trust Infrastructure)**: A Layer-0 architectural category for regulated AI and data systems, in which the evidence that a decision occurred — and was constrained as claimed — is produced as an intrinsic property of execution, decoupled from the personal data that informed it. The evidence is independently retained and verifiable; the personal data is independently minimized and made technically inaccessible. See [the category thesis](category/00_category-thesis.md).
- **Retention Paradox**: The structural conflict between a legal **duty to retain** the evidence of a decision (cybersecurity, internal-controls, audit obligations) and a legal **duty to erase** the personal data behind it (data-protection law). Both are binding; retaining the data to satisfy one creates a standing violation of the other. ATI dissolves it by giving evidence and personal data *separate lifecycles*.
- **Trust by Physics**: The posture in which trust derives from what the architecture makes structurally possible, not from what the operator promises — *"the architecture leaves nothing to look at, and a proof that this was so"* — as opposed to **trust by policy** (*"we promise not to look"*).
- **Toxic Data Asset**: Personal data that carries regulatory liability whether it is retained (privacy exposure) or destroyed (evidence destruction). The asset ATI is designed to never hold in the first place.

---

### Core mechanisms (interface level)

- **Zero-Persistence**: The doctrine that the decision runtime processes sensitive data only in volatile memory, for the duration of a decision, and does not persist the personal payload. What crosses the boundary into stored state is the PII-free capsule, by construction. It supports erasure workflows by leaving no payload copy to delete; it is an architectural property, not a standalone legal-erasure guarantee.
- **WORM (Write-Once-Read-Many) ledger**: The evidence store, realized as an append-only audit/query ledger **plus signed export to storage under a retention lock** where terminal evidence must be sealed. Immutability is an engineered property of access controls and retention locks — not an inherent property of any single product.
- **Crypto-Shredding**: A **control of technical inaccessibility**. Records are encrypted under a customer-managed key; "erasing" a subject means destroying that key so the retained ciphertext can no longer be decrypted. It is **scheduled, not instantaneous** — it operates within the key-management lifecycle (key versions are disabled immediately, then scheduled for destruction over a configurable window). It renders data technically inaccessible; it is not a claim that data has ceased to exist.
- **REX (Rationale Extraction) pattern**: The pattern that forces a probabilistic model to externalize a structured, human-readable rationale *before* it may emit a decision, then binds the digest of that rationale into the evidence record. It converts an opaque model output into auditable evidence that reasoning of a defined shape took place. Productized as the [REX-Guard](modules/products/rex-guard/) family.

---

### Boundary & isolation primitives

- **Non-Coresidence**: The property that the personal-data plane and the evidence plane do not share storage or trust boundaries — the proof of a decision lives where the payload cannot, so that erasure on one plane never invalidates retention on the other.
- **Airlock**: The controlled boundary across which only PII-free, schema-bound artifacts (capsules, digests, proofs) may pass from the volatile decision runtime into persisted state. Raw payloads do not cross it.
- **Evidence Plane**: The retained, append-only, tamper-evident side of the architecture — proofs, digests, and sealed exports. Governed by retention controls outside the reach of the producing runtime.
- **Key & Retention Plane**: The control plane that governs encryption keys and retention locks — key lifecycle (disable, schedule-for-destruction, crypto-shred) and storage retention policy (bucket-lock / retention lock). The plane on which the erasure duty is discharged. *(Public name for the internal key/retention control plane.)*
- **In-Perimeter Intelligence**: Inference that runs inside the institution's own security perimeter (its VPC / confidential-computing profile), so that sensitive context is not exported to an external boundary to be reasoned over. *(Public name for the in-perimeter inference layer.)*

---

### Framework vocabulary

- **F2F-RAaT (From Fact to Feedback — Reputation-as-a-Transaction)**: A normative *execution framework within* ATI — not the category itself. It specifies how a typed Fact, a State Capsule, and a signed Policy combine to produce a bounded Decision, Effect, and Proof.
- **Spezzatura Engine (T²)**: The deterministic reputation engine that derives a score from explicit, traceable vectors rather than opaque machine learning. Named here at the level of *mechanism class*; calibrated constants and weights are not published.
- **Sigmoid P(x) layer**: The acute-reactivity layer that handles immediate, time-sensitive threats, complementing the slower temporal model. Shape only — no calibrated parameters.
- **State Capsule**: The PII-free, non–Turing-complete, schema-bound, cryptographically verifiable artifact that carries reputational state across the Airlock. It contains reputational primitives, flags, tokens, and proofs — never PII, raw documents, free text, embeddings, or executable code.
- **Burn Engine**: The deterministic actuator that consumes (Fact, Capsule, Policy) and selects exactly one effect from a finite, policy-defined effect set. Fail-closed, zero-persistence, deterministic IO.
- **Veritas Evidence Chain (Veritas Protocol)**: The protocol that seals each decision into a hash-linked, append-only evidence record binding the input digest, capsule hash, policy version, rationale digest, and decision identifier — enabling independent re-verification without the original payload. *(Public name for the internal evidence-chain mechanism.)*

---

### Decision & evidence objects

- **Fact**: A typed, minimal, formally-derived factual claim submitted to the engine. Validated against its schema before processing.
- **Policy**: A versioned, signed set of authorized rules and effects. The engine refuses to execute under an unsigned or unauthorized policy.
- **DecisionID**: An immutable identifier for a specific decision, used to retrieve and re-verify its evidence.
- **VeritasProof**: The evidence bundle emitted per decision — the set of digests and signatures that bind policy version, inputs, rationale, and outcome.
- **Bounded-Output Rationale**: A sealed, PII-free explanation with controlled entropy. Its digest is retained; the decision bands it supports are designed to leak minimal information about the input.
- **OverrideFact**: A signed, typed object recording a human break-glass intervention. It is not a database edit — it becomes part of the evidence chain, so an override can be exercised but not concealed.

---

[⬅️ Back to the ATI Index](README.md) · [Category Thesis](category/00_category-thesis.md)
