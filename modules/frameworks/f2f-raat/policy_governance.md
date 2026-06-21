# Policy Governance (Interface Contract)

The change-control contract for policy: who may change a policy, and what a change MUST pass through before it can take effect. This specifies the process invariants, not the quorum parameters.

---

## The contract

- **Separation of duties** — policy definitions MUST be controlled under strict separation of duties. The roles that **propose**, **sign**, and **publish** a policy SHOULD be distinct.
- **Controlled change path** — policy updates SHOULD pass through:
  1. **Capability diffing** — confirm the change introduces no unintended escalation of authority or effects.
  2. **Independent review** — external or independent review for MAJOR changes.
  3. **Re-identification** — regeneration of the `PolicyID` and signatures, so the new policy is a distinct, attributable version.
- **Audited expansion** — any addition to the effect set MUST require a **MAJOR** version bump and external audit.

---

## Invariants

- **No unilateral change** — no single role can both author and authorize a policy into effect.
- **No silent change** — every change produces a new `PolicyID` and checksum; a change that does not is not representable.
- **No undetected escalation** — capability diffing makes an authority increase explicit and reviewable before activation.
- **Evidence continuity** — each decision binds the `PolicyID` active at its time, so a policy change is visible as a boundary in the evidence record.

---

## Guarantees & non-guarantees

- **Guaranteed:** policy change is attributable, reviewed proportionally to its blast radius, and bound into the audit trail.
- **Not specified here:** the quorum (M-of-N) sizes, time-lock durations, and reviewer composition — deployment-internal. Signing mechanics are in [policy signing](../../../governance/policy_signing.md).

---

[⬅️ F2F-RAaT](README.md) · [Economic Binding](economic_binding.md) · [Governance](../../../governance/README.md)
