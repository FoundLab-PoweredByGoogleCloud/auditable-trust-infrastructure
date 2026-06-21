# Economic Binding Rules (Interface Contract)

How economic effects are constrained so they remain deterministic, policy-bound, and auditable. This file specifies the **classes** of economic effect and the invariants they MUST satisfy — not the thresholds, durations, or pricing curves, which are deployment policy.

---

## Effect classes

A deployment MAY define economic effects across these classes:

- **Slashing** — penalizing a stake or balance on a policy-defined trigger.
- **Hold durations** — pausing value movement for a bounded interval.
- **Dynamic limits** — adjusting transaction limits as a function of reputational state.
- **Pricing adjustments** — varying cost/friction with risk.
- **Collateralization** — requiring collateral proportional to assessed risk.

---

## Invariants

Every economic effect MUST be:

1. **Deterministic** — the same `(Fact, Capsule, Policy)` yields the same economic effect, every time.
2. **Policy-bound** — the parameters (thresholds, durations, curves) live in the signed policy; changing them changes the `PolicyID`.
3. **Bounded** — effects are drawn from the closed [Burn Engine effect set](../burn-engine/effect_set.md); there is no open-ended economic action.
4. **Fully auditable in Veritas** — each economic effect, and the policy version that authorized it, is bound into the decision's evidence and independently re-verifiable.
5. **Fail-closed** — when a safe economic effect cannot be computed, the engine falls back to the safest policy-defined effect, never the most permissive.

---

## Guarantees & non-guarantees

- **Guaranteed:** the *space* and *determinism* of economic effects are auditable in advance; no economic action escapes the evidence chain.
- **Not specified here:** the slashing thresholds, hold durations, dynamic-limit formulas, pricing curves, and collateral ratios — all deployment-calibrated policy, not public constants.

---

[⬅️ F2F-RAaT](README.md) · [Policy Governance](policy_governance.md) · [Burn Engine Effect Set](../burn-engine/effect_set.md)
