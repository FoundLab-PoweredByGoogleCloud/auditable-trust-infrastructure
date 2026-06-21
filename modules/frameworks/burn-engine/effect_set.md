# Burn Engine — Effect Set (Interface Contract)

The Burn Engine MUST select exactly one decision from a **finite, closed, policy-defined** set of effects. This file specifies the canonical effect set and the rules that govern it — not the policy logic that chooses between them.

---

## The canonical effects

| Effect | Intent |
| :--- | :--- |
| `ALLOW` | Proceed normally. |
| `ALLOW_WITH_CONDITIONS` | Proceed with added friction or constraints. |
| `RATE_LIMIT` | Throttle execution. |
| `ESCROW_OR_HOLD` | Pause for a bounded interval. |
| `QUARANTINE` | Isolate the subject's session/context. |
| `FLAG_ONLY` | Record a signal without altering flow. |
| `DENY` | Hard block. |
| `EMERGENCY_HALT` | Circuit breaker — **policy-gated**, never reachable by ordinary scoring. |

---

## Invariants

A conforming Burn Engine MUST:

1. **Closed set** — emit exactly one effect from this finite set; an effect outside the set is a conformance failure. Extending the set is a MAJOR policy change requiring external audit (see [policy governance](../f2f-raat/policy_governance.md)).
2. **Determinism** — for the same `(Fact, Capsule, Policy)`, select the same effect every time.
3. **Fail-closed** — if a safe effect cannot be computed, fall back to the safest policy-defined effect (typically `DENY` or a hold), never to `ALLOW`.
4. **Gated escalation** — high-consequence effects (e.g. `EMERGENCY_HALT`) are reachable only through explicit policy gates, not as a direct function of score.
5. **Evidence-bound** — the selected effect, and the policy version that authorized it, are bound into the decision's Veritas proof.

---

## Guarantees & non-guarantees

- **Guaranteed:** the *space* of possible actions is bounded and auditable in advance; a regulator can enumerate every action the engine could take before it runs.
- **Not specified here:** the policy logic, thresholds, and conditions that map a given state to a given effect. That mapping is deployment policy — not public canon.

---

[⬅️ Burn Engine](README.md) · [Burn Engine Spec](burn_engine_spec.md) · [Frameworks](../README.md)
