# Adversarial Vectors (High-Level)

The catalogue of adversary classes an ATI deployment is designed to counter, and the architectural property that addresses each. Stated at the level of *mechanism class* — not the calibrated detection logic.

---

## The vectors

| Vector | The attack | Architectural property that addresses it |
| :--- | :--- | :--- |
| **Authority Creep / Policy Capture** | An insider widens their own authority or rewrites rules to favor an attacker. | **Separation of duties + multi-sig governance** — policy changes require M-of-N consensus and leave evidence (see [policy governance](../f2f-raat/policy_governance.md)). |
| **Side-channel & timing analysis** | Inferring protected state from timing or resource observation. | **Bounded output** — decision bands are designed to leak minimal information about the input; minimized exposure window. |
| **Rollback / anti-slashing evasion** | Reverting to an earlier, more favorable state to dodge an effect. | **Append-only, lineage-bound evidence** — capsules bind to prior state; a rollback is tamper-evident. |
| **Fact forgery / evidence laundering** | Injecting a fabricated "fact" to manufacture a favorable decision. | **Typed, source-signed facts + digest binding** — unsigned or schema-invalid facts are rejected before processing. |
| **Economic gaming (sybil, fragmentation)** | Splitting activity across identities to stay under thresholds. | **Temporal weighting + relationship vectors** — trust that is expensive to fabricate over time; gaming is negative-expected-value. |
| **Break-glass abuse / insider collusion** | Misusing the human override to bypass the engine. | **Dual-control `OverrideFact` recorded as evidence** — overrides are possible but never concealable (see [break-glass](../../../governance/break_glass_protocol.md)). |

---

## Invariant behind the catalogue

Each vector is countered by a property the attacker **cannot circumvent structurally**, not by a promise the operator makes. Where only a procedural mitigation exists, the vector is treated as residual risk and surfaced in the [red-team matrix](red_team_matrix.md).

> Mechanism class is described here; the calibrated detection parameters and thresholds are deployment-internal.

---

[⬅️ Threat Model](README.md) · [Red Team Matrix](red_team_matrix.md) · [Mitigations](mitigations.md)
