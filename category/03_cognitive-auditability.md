# 3. Cognitive Auditability: Taming Probabilistic AI (Veritas 3.0)

The adoption of Generative AI in finance introduces a new, more complex challenge: **The Cognitive Audit Paradox**. How can you audit the reasoning of an AI that is inherently probabilistic and whose internal thoughts are a "black box"?

The Veritas 3.0 evolution of the ATI is designed to solve this by imposing deterministic, auditable controls on the AI's cognitive process.

---

### Mitigating Opacity: The Rationale Extraction (REX) Pattern

The core innovation is the **Rationale Extraction (REX) pattern**, which transforms the AI from an opaque oracle into a transparent, accountable agent.

- **The Problem:** Advanced models may expose only limited inspectability into their internal reasoning, and some encapsulate intermediate reasoning in ways that are not directly auditable.
- **The Solution:** The REX pattern forces the AI to **externalize its reasoning** into a structured, human-readable text field (`rationale_text`) *before* it can output a final decision. This rationale must be legally defensible.
- **Deterministic Proof:** The AI is run with `temperature` set near zero (0.0-0.1) to ensure its output is replicable. The **cryptographic hash** of this rationale (`rationale_hash`) is then recorded in the Veritas WORM ledger, creating an immutable proof that auditable reasoning took place.

---

### Mitigating Data Leakage: Reinforcing Zero-Persistence with AI

The ATI's Zero-Persistence pillar is not just compatible with AI; it's enhanced by it.

- **The Problem:** Traditional AI workflows (especially RAG) often require creating persistent Vector Databases, which re-introduces a massive privacy risk.
- **The Solution:** Large-context models allow dossiers and regulatory documents to be loaded into volatile memory per inference. In selected deployment profiles this **reduces reliance on persistent retrieval stores** (e.g. vector databases), reinforcing the Zero-Persistence thesis — it does not remove retrieval architecture in all cases.
- **Zero Data Retention (ZDR):** Provider-side caching and logging are minimized per deployment. These controls **reduce retention and leakage surface**; they are configured per deployment and are not a blanket guarantee that sensitive data never leaves every operational boundary.

---

### Active Intervention & Antifragility

The ATI's cognitive components provide an active, real-time defense system.

- **In-Perimeter Intelligence:** This is the system's "immune system," using in-perimeter inference to detect anomalies and risks in real time. Its scope extends to auditing Infrastructure-as-Code (IaC) to find compliance vulnerabilities before they are deployed.
- **Burn Engine:** This is the system's "actuator." Upon high-confidence detection by the In-Perimeter Intelligence layer (e.g., impossible-travel geo-velocity), the Burn Engine executes irreversible, programmatic actions in real time—blocking transactions, revoking API keys, or triggering crypto-shredding.
- **Antifragility:** Detected anomalies, attacks, and errors feed evaluation, review, and policy-hardening loops. They are **not** automatically converted into training data — that requires an approved data-governance basis for the deployment.

**Próximo:** [Strategic Impact — Operational Alpha](./04_strategic-impact.md)
