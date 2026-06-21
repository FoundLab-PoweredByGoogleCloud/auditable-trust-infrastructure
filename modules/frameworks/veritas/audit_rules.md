# Veritas — Audit Rules (Interface Contract)

What an auditor or regulator MUST be able to do against a Veritas evidence chain, stated as capabilities the architecture guarantees — not the verification implementation.

---

## Required auditor capabilities

A conforming deployment MUST allow an auditor or regulator to:

1. **Recompute** — given the recorded digests and the capsule, recompute a past decision and confirm it matches the recorded outcome.
2. **Verify versions** — confirm that the runtime version and policy version bound to the proof match the expected, published values.
3. **Confirm non-exposure** — confirm that **no PII was required or exposed** to perform the audit; verification runs over digests and the PII-free capsule.
4. **Confirm integrity** — detect any alteration of input, capsule, policy, or outcome as a verification failure (tamper-evidence).
5. **Audit across erasure** — perform all of the above for a decision **even after** the subject's personal data has been crypto-shredded; erasure of the data does not impair verification of the proof.

---

## Invariants

- **Independence** — verification does not require trusting the operator's logs; it is recomputation from committed digests.
- **Reproducibility** — the same proof verified by different parties yields the same result.
- **PII-free audit** — auditability never re-introduces the personal data it was designed to exclude.

---

## Guarantees & non-guarantees

- **Guaranteed:** decisions are independently re-verifiable from retained evidence, without the original payload.
- **Not specified here:** the verification tooling, hash/signature schemes, and ledger internals — deployment-internal. See the [proof spec](veritas_proof_spec.md) for the binding contract.

---

[⬅️ Veritas](README.md) · [Proof Spec](veritas_proof_spec.md) · [Frameworks](../README.md)
