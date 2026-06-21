# ATI — Master Index

> Navigate the canon by what you need to do.

---

## Understand the category (start here)

The "why" before the "how". Read in order:

0. **[The Category Thesis](category/00_category-thesis.md)** — the founding document: why policy-based trust fails, why GRC/XAI/SIEM/observability don't solve it, the definition, and the invariants as the membership test.
1. **[The Regulatory Paradox](category/01_the-regulatory-paradox.md)** — why institutions are trapped between retention and erasure.
2. **[Trust by Physics](category/02_trust-by-physics-pillars.md)** — the three pillars: Zero-Persistence, WORM, Crypto-Shredding.
3. **[Cognitive Auditability](category/03_cognitive-auditability.md)** — imposing deterministic, provable controls on generative AI.
4. **[Strategic Impact](category/04_strategic-impact.md)** — how the architecture turns compliance into operational advantage.

Overview: **[category/README.md](category/README.md)**

The non-negotiable rules every ATI deployment must satisfy: **[The Category Invariants](category/invariants.md)**.

---

## For architects & product owners

How the system is built and behaves.

- **[Modules overview](modules/README.md)** — frameworks vs products.
- **[ATI Reference Stack](reference-architecture/ati-reference-stack.md)** — the L0 + five-layer composition that bridges the category to a deployment.
- **[Reference Architecture (public SAD)](reference-architecture/README.md)** — sanitized baseline for regulated GenAI.
- **[Cookbook · Pix fraud attack](cookbooks/01_pix_hft_attack.md)** — a real-world walkthrough.
- **[Cookbook · Merchant trust growth](cookbooks/02_merchant_gradual_trust.md)** — how reputation scales over time.
- **[Governance & policy control](governance/README.md)** — who controls the rules.

---

## For engineers & developers

How to implement and integrate.

- **[API specification (OpenAPI)](interface-contracts/f2f-raat-api.yaml)** — the REST contract.
- **[Fact schemas](interface-contracts/FACT_SCHEMAS/)** — JSON Schemas for standard input facts.
- **[State Capsule schema](modules/frameworks/state-capsule/capsule_schema.json)** — the structure of reputation.
- **[Burn Engine logic](modules/frameworks/burn-engine/burn_engine_spec.md)** — how decisions are computed.
- **[Spezzatura T² model](modules/frameworks/spezzatura/README.md)** — the reputation math.
- **[Compliance test vectors](compliance/compliance_vectors_v1.json)** — QA cases.

---

## For auditors & security

How to prove it is safe and compliant.

- **[Veritas proof spec](modules/frameworks/veritas/veritas_proof_spec.md)** — how the audit trail works.
- **[Threat model](modules/frameworks/threat-model/README.md)** — defense against poisoning and adversarial vectors.
- **[Compliance matrix](compliance/COMPLIANCE_MATRIX.md)** — regulatory mapping (LGPD / GDPR / EU AI Act / CMN-BCB / SOX).
- **[Cognitive Auditability](category/03_cognitive-auditability.md)** — proving AI intent.

---

## For executives & strategy

The value and the moat.

- **[Strategic Impact](category/04_strategic-impact.md)** — operational advantage from architectural compliance.
- **[The Regulatory Paradox](category/01_the-regulatory-paradox.md)** — the problem in one page.
- **[Whitepaper](whitepaper/f2f-raat/F2F-RAAT_WHITEPAPER_v1.1.md)** — the full theory.
- **[REX Guard whitepaper](modules/products/rex-guard/rex-guard-whitepaper.md)** — the product thesis.

---

## Vocabulary

When a term is unfamiliar, check the **[Glossary](GLOSSARY.md)** first.
