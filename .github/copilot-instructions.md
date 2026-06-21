# Copilot / AI-agent instructions — ATI repository

This repository is the **public canon of Auditable Trust Infrastructure (ATI)**: the
category narrative, its open frameworks, the products built on them, and the
cryptographic contracts that make ATI's claims verifiable. Treat every normative file
as a specification, not prose to be casually paraphrased.

## Mental model

ATI resolves the **Retention Paradox** — the law demands both immutable retention and
on-request erasure — by replacing policy-based trust with *physics-based* trust:
Zero-Persistence runtime, an immutable WORM ledger of proofs, and crypto-shredding.

The runtime loop is: **Fact -> State Capsule -> Burn Engine decision -> Veritas proof -> feedback.**

## Where things live

- `category/` — the four-part narrative that defines the category. Conceptual source of truth.
- `modules/frameworks/` — the normative specifications:
  - `f2f-raat/` — the execution contract and invariants (the Law).
  - `spezzatura/` — the T-squared reputation model (the Brain).
  - `state-capsule/` — the PII-free boundary object: `capsule_schema.json` + spec (the Memory).
  - `burn-engine/` — deterministic authorization logic and effect set (the Hammer).
  - `veritas/` — proof spec and audit rules (the Truth).
  - `threat-model/` — adversarial vectors and mitigations (the Defenses).
- `modules/products/` — deployables (e.g. `rex-guard/`).
- `compliance/`, `governance/`, `interface-contracts/`, `cookbooks/`,
  `reference-architecture/`, `whitepaper/` — supporting pillars.

## Editing rules

- **Normative coupling.** Changing the State Capsule shape means updating
  `modules/frameworks/state-capsule/capsule_schema.json` and its spec, and checking
  whether the invariants in `modules/frameworks/f2f-raat/invariants.md` are affected.
- **New decision type.** Adding a Burn Engine decision means updating
  `modules/frameworks/burn-engine/burn_engine_spec.md` and the f2f-raat execution
  contract together. Keep test vectors in sync.
- **Claims hygiene.** This is a verifiability repository. Do not introduce
  unverifiable metrics, "production-ready" assertions, or unconditional legal-erasure
  claims. Crypto-shredding is a technical inaccessibility control; describe it as such.
  Prefer "architected for / aligned with" over "certified / compliant" unless a
  per-deployment certification is being referenced.
- **Cross-links.** Use relative paths consistent with the lowercase-kebab structure.
