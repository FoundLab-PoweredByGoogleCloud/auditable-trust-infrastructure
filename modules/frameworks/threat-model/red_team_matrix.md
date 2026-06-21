# Red Team Matrix (Analysis Frame)

The structured frame for analyzing each adversarial vector against an ATI deployment. This file defines the **axes** of analysis; the calibrated results — which mitigations are tuned to which thresholds — are deployment-internal and not published here.

---

## Analysis axes

Each [adversarial vector](adversarial_vectors.md) SHOULD be analyzed across:

| Axis | Question |
| :--- | :--- |
| **Attacker capability** | Low / medium / high — what access and resources does the attack require? |
| **Economic motivation** | What is the payoff, and does the architecture make it negative-expected-value? |
| **Regulatory impact** | Which obligation (retention, erasure, integrity, explainability) does a successful attack threaten? |
| **Detection difficulty** | Is the attack tamper-evident in the evidence chain, or does it require external detection? |
| **Mitigation class** | Which architectural property (determinism, fail-closed, multi-sig, non-coresidence, crypto-shredding) counters it — *by physics, not by promise*? |

---

## How to read a row

A vector is considered **architecturally addressed** when its mitigation derives from a structural invariant (something the attacker cannot do) rather than a policy promise (something the operator pledges not to do). Vectors whose only mitigation is procedural are flagged as residual risk and escalated.

---

## Guarantees & non-guarantees

- **Guaranteed framing:** every vector is mapped to a mitigation *class*, and the residual (procedural-only) vectors are made explicit.
- **Not published here:** the per-vector calibrated thresholds, detection tuning, and quantified likelihood/impact scores — these are deployment-internal red-team artifacts.

> The fully populated matrix is maintained per deployment; this public canon specifies its structure, not its tuned contents.

---

[⬅️ Threat Model](README.md) · [Adversarial Vectors](adversarial_vectors.md) · [Mitigations](mitigations.md)
