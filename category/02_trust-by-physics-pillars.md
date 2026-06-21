# 2. The Three Pillars of Trust by Physics: The Veritas 2.0 Architecture

FoundLab's canonical architecture resolves the Retention Paradox by moving from process-level mitigation to **architectural decoupling of the risk**. This is achieved by physically and cryptographically decoupling the *proof of an event* from the *data of an event*.

This is **Trust by Physics**, built on three core pillars.

---

### Pillar 1: Zero-Persistence — Reducing Risk at the Source

**The safest data is data that no longer exists.** The Zero-Persistence doctrine dictates that sensitive data is only ever processed in volatile memory (RAM), never stored at rest.

- **Mechanism:** Sensitive data is processed within ephemeral, kernel-level isolated sandboxes (Google Cloud Run with gVisor). Upon completion of the task (e.g., an AI inference), the container is destroyed (`SIGKILL`) and its memory reclaimed — best-effort at the runtime layer, hardware-backed under a confidential-computing (TEE) profile.
- **Mandate Addressed:** This **supports** LGPD/GDPR erasure workflows by design — subject to legal basis, retention obligations, deployment controls, and customer approval. Where data is never persisted, there is no copy to delete; this is "compliance-as-infrastructure", not a standalone legal-erasure guarantee.

---

### Pillar 2: The Veritas Protocol — Mathematical Proof, Not Manual Process

In place of fallible human processes, Veritas provides an immutable, mathematical record that an event occurred and a decision was made, without holding the toxic data itself.

- **Mechanism:** Every decision generates a W3C Verifiable Credential, whose cryptographic hash is recorded in an immutable **WORM ledger** (Write-Once-Read-Many): an audit/query projection (e.g. BigQuery) with **terminal evidence sealed by signed export to Cloud Storage Bucket Lock** where required. IAM roles and retention locks prevent modification or deletion of sealed records.
- **Mandate Solved:** This satisfies the BACEN/SOX retention requirement by preserving a verifiable, tamper-proof audit trail for the required 5-10 year period.

---

### Pillar 3: Crypto-Shredding — The Right to Erasure, The Mandate to Retain

This is the engineering keystone that solves the paradox's final conflict. It allows a record to be both retained and "deleted" simultaneously.

- **Mechanism:** The data written to the WORM ledger is encrypted using a Customer-Managed Encryption Key (CMEK) via Google Cloud KMS. To honor an erasure request, the client **destroys the CMEK**.
- **Mandate Solved:**
    - The encrypted data (**ciphertext**) remains physically in the WORM ledger, satisfying the **retention mandate** (BACEN/SOX).
    - Without the key, the ciphertext becomes **irrecoverable mathematical entropy**—"cryptographic garbage". This satisfies the **erasure mandate** (LGPD).

> **Metaphor:** The ciphertext stays in a locked drawer (the WORM ledger), satisfying the auditor. The key is disabled and scheduled for destruction under the KMS lifecycle (crypto-shredding), making the contents technically inaccessible — a technical control, not a legal-erasure verdict.

**Next:** [Cognitive Auditability & AI](./03_cognitive-auditability.md)
