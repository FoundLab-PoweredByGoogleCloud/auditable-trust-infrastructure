# Veritas Proof Specification (Interface Contract)

This specifies **what a Veritas proof binds** and **what it guarantees** — not the cryptographic construction, parameters, or anchoring schedule, which are deployment-internal.

---

## The binding

Each decision emits a `VeritasProof` that binds, by cryptographic digest, the artifacts that fully determine the decision:

| Field | Binds |
| :--- | :--- |
| `FactDigest` | The input event, hashed — never the raw PII. |
| `CapsuleHash` | The reputational state used at decision time. |
| `PolicyID` | The exact policy version in force. |
| `RuntimeVersion` | The runtime that executed the decision. |
| `RationaleDigest` | The PII-free, bounded-output rationale, hashed. |
| `DecisionID` | The immutable identifier of this decision. |

The proof is the *commitment*, not the data: it lets a third party confirm a past decision was produced by a specific policy over specific inputs, without holding those inputs.

---

## Invariants

A conforming proof MUST:

1. **Bind, not store** — carry digests/commitments only; no PII, raw documents, or free text appear in the proof.
2. **Be reconstructable** — given the retained digests and the capsule, a competent auditor can recompute the decision and confirm it matches the recorded outcome.
3. **Be append-only** — proofs are written to an append-only, tamper-evident evidence record; terminal evidence is sealed by signed export to storage under a retention lock (see the [Compliance Matrix](../../../compliance/COMPLIANCE_MATRIX.md)).
4. **Survive erasure** — destroying a subject's encryption key (crypto-shredding) renders the associated personal data technically inaccessible **without** invalidating or deleting the proof.
5. **Be policy-pinned** — the proof identifies *which* policy version was active; a different `PolicyID` is a different, distinguishable decision.

---

## Guarantees & non-guarantees

- **Guaranteed:** integrity binding (any alteration of input, capsule, policy, or outcome breaks verification) and independent re-verification from retained digests.
- **Anchoring:** proofs SHOULD be anchored in an append-only ledger (e.g. WORM / hash-chain) with terminal sealing as above. The specific ledger, hash function, signature scheme, and anchoring cadence are **deployment-internal** and not fixed here.
- **Not a claim:** this canon does not assert that history is mathematically impossible to rewrite — it asserts that rewriting is **tamper-evident** under the configured controls.

---

[⬅️ Veritas](README.md) · [Audit Rules](audit_rules.md) · [Frameworks](../README.md)
