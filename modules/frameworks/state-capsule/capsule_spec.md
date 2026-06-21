# State Capsule — Specification (Interface Contract)

The State Capsule is a **PII-free, non–Turing-complete, schema-bound** artifact that represents reputational state and carries it across trust boundaries. This file specifies what it may and may not contain, and the guarantees that follow — not the concrete field schema, which is normative in [`capsule_schema.json`](capsule_schema.json).

---

## What it carries

A capsule is a strictly typed object. It **MAY** contain:

- Reputational primitives derived from the Spezzatura (T²) and Sigmoid P(x) layers.
- Policy flags and PII-free XAI / reason tokens.
- Cryptographic proofs and commitments (binding to prior state and FACT digests).
- Constraints, origin, and version metadata.

It **MUST NOT** contain:

- PII, raw documents, free text, embeddings, or arbitrary payloads.
- Any executable code.

The boundary is the point of the artifact: it is the *only* thing that crosses the [Airlock](../../../GLOSSARY.md) from the volatile decision runtime into persisted state.

---

## Why it exists

It resolves the privacy–utility conflict in portability: *how do you convey "this subject is trusted" to another party without conveying the subject's history?* You convey the capsule — reputational state without identity, verification without exposure.

---

## Invariants & guarantees

- **PII-free by construction** — reputation travels; identity does not. This is what lets the capsule be retained, ported, and verified while the personal data is independently minimized and erasable.
- **Verifiable lineage** — its embedded proofs let a verifier confirm it descends from legitimate prior state and facts, without the underlying payload.
- **Schema- and version-bound** — every capsule names the schema/version it conforms to; validation precedes any use (see [constraints](constraints.md)).
- **Inert** — being non–Turing-complete and code-free, a capsule cannot carry execution; it is evaluated, never run.

> Coupling note: the concrete field shape is normative in [`capsule_schema.json`](capsule_schema.json); keep this spec, the schema, the [constraints](constraints.md), and the F2F-RAaT [invariants](../f2f-raat/invariants.md) consistent.

---

[⬅️ State Capsule](README.md) · [Constraints](constraints.md) · [Frameworks](../README.md)
