# Spezzatura — Score Bands (Interface Contract)

This file specifies the **shape** of how a Spezzatura score maps to a decision band. It is deliberately parameter-free: the calibrated thresholds are deployment policy, not public constants.

---

## What a band is

The engine emits a scalar reputation score on a bounded scale. A **policy** partitions that scale into an ordered set of decision bands. The canonical partition is three bands:

| Band | Meaning |
| :--- | :--- |
| **BLOCK** | Score below the lower policy threshold `τ_block`. |
| **REVIEW** | Score between `τ_block` and the upper threshold `τ_review`. |
| **ALLOW** | Score at or above `τ_review`. |

`τ_block` and `τ_review` are **policy parameters, calibrated per deployment** — they are not fixed in this public canon. A deployment MAY define additional intermediate bands, provided the invariants below hold.

---

## Invariants

A conforming band mapping MUST satisfy:

1. **Monotonicity** — a higher score never maps to a stricter band. The mapping is a non-increasing function from score to restriction.
2. **Total coverage** — every point on the score scale maps to exactly one band; there are no gaps and no overlaps.
3. **Ordered thresholds** — `τ_block ≤ τ_review`; thresholds are non-decreasing across the band order.
4. **Policy-bound** — thresholds are carried in the signed policy and bound, by digest, into the decision's evidence (see the [Veritas proof spec](../veritas/veritas_proof_spec.md)). Changing a threshold changes the `PolicyID`.
5. **Determinism** — for a fixed score and a fixed policy version, the band is identical on every evaluation.

---

## Guarantees & non-guarantees

- **Guaranteed:** given a score and the policy version active at decision time, any auditor can recompute the band without access to the underlying personal data.
- **Not specified here:** the numeric value of any threshold, the calibration procedure, and how the score itself is computed from vectors. Those live in deployment policy and the internal model — not in this public canon.

> The example thresholds shown in some narrative material are illustrative of band *structure*, not normative values.

---

[⬅️ Spezzatura](README.md) · [T² Spec](spezzatura_t2_spec.md) · [Frameworks](../README.md)
