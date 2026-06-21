# REX Guard

### Cryptographic governance layer for generative AI.

REX Guard is the reference **product** of the ATI category. It reconciles a hard conflict: regulated generative-AI systems need durable, immutable evidence of every decision, while data-protection law grants subjects the right to have personal data erased.

Its core mechanism is a strict **separation of planes**:

- an **Immutable Evidence Ledger** (proofs only),
- a **Mutable Key & Retention Plane** (where erasure happens, by key destruction),
- an **Encrypted Sensitive Payload Store**, and
- an **Operational Analytics Plane**.

The central invariant is **Non-Coresidence**: raw PII and cryptographic key material must never be committed to the immutable ledger. A pre-commit **Airlock Quarantine Protocol** enforces this before any WORM retention lock is applied. A deterministic legal-state machine executes a versioned retention-precedence matrix without deciding substantive law. Crypto-shredding is formalized as a *technical inaccessibility control* — not an unconditional claim of legal erasure.

---

## Read it

- **[rex-guard-whitepaper.md](rex-guard-whitepaper.md)** — the full architecture: the erasure–immutability paradox, the Non-Coresidence invariant, the Airlock Quarantine Protocol, the deterministic retention state machine, cryptographic topology, end-to-end lifecycle, and failure modes.

## How it maps to the frameworks

| REX Guard plane | ATI framework |
| :--- | :--- |
| Immutable Evidence Ledger | [veritas](../../frameworks/veritas/) |
| Decision / authorization | [burn-engine](../../frameworks/burn-engine/) |
| Execution contract & invariants | [f2f-raat](../../frameworks/f2f-raat/) |
| Regulatory mapping | [compliance](../../../compliance/COMPLIANCE_MATRIX.md) |

REX Guard is **L1 (the Inference Proxy / Product Runtime)** in the [ATI Reference Stack](../../../reference-architecture/ati-reference-stack.md) — the fail-closed layer that the rest of the stack executes around.

---

> **Status.** REX Guard is published here as a specification and architectural whitepaper. Production and certification status are tracked per deployment; this document does not assert blanket production readiness.

[⬅️ Back to Products](../README.md) · [ATI Index](../../../README.md)
