# State Capsule — Constraints (Interface Contract)

The constraints a State Capsule MUST satisfy to be valid. These are membership conditions for the artifact, not its internal field layout (that lives in [`capsule_schema.json`](capsule_schema.json)).

---

## Invariants

A valid capsule MUST:

1. **Be schema-bound** — conform to a versioned, published schema; anything that does not validate is rejected before processing.
2. **Be versioned** — carry an explicit schema/version identifier, so a verifier knows exactly which rules apply.
3. **Be bound to lineage** — include cryptographic proofs binding it to its prior state and to the FACT digests that produced it, so its provenance is verifiable.
4. **Be PII-free by construction** — contain only reputational primitives, flags, tokens, proofs, and version metadata. It MUST NOT contain PII, raw documents, free text, embeddings, or arbitrary payloads.
5. **Be inert** — contain no executable code; the capsule is data, never logic.
6. **Be origin- and time-bounded** — carry origin and validity metadata (e.g. namespace, timestamp, TTL) so stale or out-of-context capsules can be rejected by policy.

---

## Guarantees & non-guarantees

- **Guaranteed:** a capsule can cross trust boundaries (the [Airlock](../../../GLOSSARY.md)) and be verified by a counterparty **without** exposing the personal data it was derived from.
- **Not specified here:** the exact set of reputational primitives, the digest/commitment scheme, and the TTL/origin policy values — these are schema- and deployment-defined.

> Coupling note: changes to these constraints must stay consistent with [`capsule_schema.json`](capsule_schema.json), the [capsule spec](capsule_spec.md), and the F2F-RAaT [invariants](../f2f-raat/invariants.md).

---

[⬅️ State Capsule](README.md) · [Capsule Spec](capsule_spec.md) · [Frameworks](../README.md)
