# Policy Signing & Publication (Interface Contract)

How a policy becomes authoritative, and the guarantees that signing provides. This file specifies the contract, not the key ceremony, quorum sizes, or cryptographic parameters — those are deployment-internal.

---

## The contract

1. **Signed by institutional keys** — policies MUST be signed using institutional, **HSM-backed** keys. The runtime refuses to load or execute under an unsigned or improperly signed policy (fail-closed boot).
2. **Published identity** — publication SHOULD expose a public `PolicyID` and checksum, so any party can confirm *which* policy is active.
3. **Environment isolation** — dev / test / prod environments MUST NOT reuse signing keys; a signature valid in one environment is not valid in another.
4. **Key custody** — private key material is held within the [Key & Retention Plane](../GLOSSARY.md) and is not accessible to third parties, consistent with the CMN/BCB cybersecurity-framework restriction on third-party access to private keys.

---

## Invariants

- **Refuse-on-invalid** — no valid signature ⇒ no execution. There is no "unsigned fallback".
- **Tamper-evident identity** — any change to policy content yields a new `PolicyID` and checksum; a silent edit is not representable.
- **Evidence binding** — the active `PolicyID` is bound into every decision's Veritas proof, so each decision is attributable to a specific, verifiable policy version.

---

## Guarantees & non-guarantees

- **Guaranteed:** decisions are attributable to a named, signed policy version, and an unsigned policy cannot take effect.
- **Not specified here:** the signing algorithm, quorum (M-of-N) parameters, key-rotation cadence, and ceremony — all deployment-internal. See [policy governance](../modules/frameworks/f2f-raat/policy_governance.md) for the change-control process.

---

[⬅️ Governance](README.md) · [Break-Glass Protocol](break_glass_protocol.md)
