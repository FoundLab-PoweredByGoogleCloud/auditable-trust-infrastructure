# Products

Where the frameworks become deployable. A product takes the abstract primitives of **Auditable Trust Infrastructure** and gives an institution something it can run, point an auditor at, and defend in a deposition.

---

## REX family

The **REX** line is named for the **Rationale Extraction** pattern at the heart of the category: forcing an AI system to externalize a provable, hashed rationale before it is allowed to act.

| Product | Status | Built on | Purpose |
| :--- | :--- | :--- | :--- |
| **[rex-guard/](rex-guard/)** | Specification + whitepaper | f2f-raat · veritas · burn-engine | Cryptographic separation and deterministic legal-state governance for immutable auditability in generative AI — reconciling the immutability of evidence with the mutability of privacy obligations. |

> Additional REX-family surfaces (agent-execution evidence, voice acceptance governance) are part of the broader roadmap and are not specified in this public canon.

---

## What makes something an ATI product

A product earns the label only if it preserves the non-negotiable invariants of the category:

1. **Fail-closed.** If the proof layer or key layer is unavailable, the system blocks — it does not silently proceed.
2. **Non-coresidence.** Raw PII and key material never land in the immutable ledger.
3. **Evidence ≠ data.** The ledger holds hashes and signatures, never the sensitive payload.
4. **Crypto-shredding is a technical inaccessibility control** — described precisely, never overclaimed as unconditional legal erasure.

---

[⬅️ Back to Modules](../README.md) · [ATI Index](../../README.md)
