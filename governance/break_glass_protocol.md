# Break-Glass Protocol (Interface Contract)

How a human authority overrides the engine **without** escaping the audit trail. This specifies the contract and its invariants, not the operational runbook.

---

## The contract

1. **Outside the runtime** — break-glass actions occur strictly **outside** the decision runtime; they are not a path through ordinary execution.
2. **Typed, not ad-hoc** — every override MUST be encoded as a typed `OverrideFact` object. It is a structured, signed transaction — never a database edit.
3. **Dual-control** — overrides MUST require dual-control / multi-sig authorization; no single actor can exercise one alone.
4. **Recorded as evidence** — every override MUST be recorded as a reputational event, visible to Veritas and bound into the evidence chain.

---

## Invariants

- **No silent override** — an override that is not recorded in the evidence chain is not a valid override. You can override the engine; you cannot conceal that you did.
- **Attributable** — the override binds the authorizing identities (under dual-control) and the policy context at the time.
- **Non-destructive** — an override adds a signed event; it does not rewrite or remove prior evidence.

---

## Guarantees & non-guarantees

- **Guaranteed:** human authority is preserved for genuine exceptions, while every exercise of it becomes permanent, attributable evidence.
- **Not specified here:** the quorum parameters, the operational escalation runbook, and stakeholder roles — deployment-internal and, for stakeholder accountability, held in a confidential artifact outside this repository.

---

[⬅️ Governance](README.md) · [Policy Signing](policy_signing.md) · [Override Fact](override_fact.md)
