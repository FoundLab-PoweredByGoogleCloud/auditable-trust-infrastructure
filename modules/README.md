# Modules

The category is abstract. The modules are concrete. This folder holds the two kinds of building block that turn **Auditable Trust Infrastructure** from a thesis into a system.

```text
modules/
├── frameworks/   # open specifications — the primitives ATI is made of
└── products/     # what gets built on the frameworks — the things you deploy
```

---

## Frameworks — the primitives

Normative specifications. Each one is a self-contained subsystem with its own contract, schema, and invariants. They compose into the closed loop **Fact → State → Decision → Proof → Feedback**.

| Framework | Role | One line |
| :--- | :--- | :--- |
| **[f2f-raat](frameworks/f2f-raat/)** | The Law | *From Fact to Feedback* — the deterministic execution contract and its invariants. |
| **[spezzatura](frameworks/spezzatura/)** | The Brain | The T² reputation model — the math that turns behavior into a score. |
| **[state-capsule](frameworks/state-capsule/)** | The Memory | The PII-free, cryptographically verifiable boundary object. |
| **[burn-engine](frameworks/burn-engine/)** | The Hammer | Deterministic authorization — applies policy to capsule and emits a binding action. |
| **[veritas](frameworks/veritas/)** | The Truth | Immutable audit trail and cryptographic proofs of causality. |
| **[threat-model](frameworks/threat-model/)** | The Defenses | Adversarial vectors (poisoning, replay) and their mitigations. |

Full index: **[frameworks/README.md](frameworks/README.md)**.

---

## Products — the deployables

What an institution actually buys and runs. Products consume one or more frameworks and wrap them in an operable surface.

| Product | Built on | One line |
| :--- | :--- | :--- |
| **[rex-guard](products/rex-guard/)** | f2f-raat · veritas · burn-engine | Cryptographic governance layer for generative AI — reconciles immutable auditability with the right to erasure. |

Full index: **[products/README.md](products/README.md)**.

---

[⬅️ Back to the ATI Index](../README.md) · [Read the category narrative](../category/README.md)
