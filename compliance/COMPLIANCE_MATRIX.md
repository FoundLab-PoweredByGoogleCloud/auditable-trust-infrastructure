# ATI Compliance Matrix
> **"Compliance-as-Infrastructure"**

This document maps the architectural pillars of **Auditable Trust Infrastructure (ATI)** to specific regulatory articles in **GDPR (EU)**, **LGPD (Brazil)**, **EU AI Act**, and the **CMN / BCB** cybersecurity and internal-controls framework.

> **Scope of these claims.** ATI is *architected for* and *aligned with* the regulations below. This is an architectural mapping, not a certification. Certification and production status are tracked **per deployment**, never asserted blanket-wide. Where a row describes a technical control (e.g. crypto-shredding), it is a control of technical inaccessibility — not a legal-erasure verdict.

---

## 1. The Right to Erasure (Right to be Forgotten)

| Regulation | Article | Requirement | ATI architectural response |
| :--- | :--- | :--- | :--- |
| **GDPR** | Art. 17 | Data subjects have the right to obtain erasure of personal data without undue delay. | **Zero-Persistence**: the decision runtime processes personal data only in volatile memory and does not persist the payload, so there is no copy at rest to delete. |
| **LGPD** | Art. 16 · Art. 18 (VI) | The holder may petition for elimination of personal data processed with consent, and of unnecessary or excessive data. | **Crypto-Shredding**: where ciphertext is retained for the evidence duty, destroying the customer-managed key renders it technically inaccessible. This is a technical inaccessibility control — scheduled within the key lifecycle, not an immediate physical wipe — and is not, by itself, a legal-erasure guarantee. |
| **LGPD** | Art. 6º (III) | Data minimization: processing limited to the minimum necessary for its purpose. | **State Capsule**: only PII-free reputational state crosses the boundary into stored state; raw identity data is never carried forward. |
| **Circular BCB 3.978/2020 (PLD/FT)** *(amended by Res. BCB 282/2022)* | Art. 50 *(records of arts. 13 / 16 / 18 and Art. 28)* | Retain KYC and transaction records of a relationship for a minimum **10-year** term — the same personal data a subject may demand be erased under LGPD Art. 18, VI. | **Crypto-Shredding + Veritas Evidence Chain (reconciliation pattern)**: retain the ciphertext and sealed evidence for the regulatory term **while** rendering the personal-data plaintext technically inaccessible on a lawful erasure trigger. This is a technical inaccessibility control — scheduled within the key lifecycle, not an immediate physical wipe — and is not, by itself, a legal-erasure guarantee. |

> **Retention/erasure reconciliation.** The PLD/FT 10-year retention duty (BCB 3.978, Art. 50) and the LGPD erasure right (Art. 18, VI) bind the *same* records in opposite directions. ATI does not rank one duty over the other: the retained evidence is held for the regulatory term on the evidence plane, while the personal-data plaintext is rendered technically inaccessible on the data plane. This is a reconciliation *pattern*, not a legal ruling that either duty is thereby discharged.

---

## 2. Auditability, Logging & Explainability

| Regulation | Article | Requirement | ATI architectural response |
| :--- | :--- | :--- | :--- |
| **CMN 4.893/2021** *(as amended by CMN 5.274/2025)* · **BCB 538/2025** *(amending BCB 85/2021)* | Cybersecurity framework | Maintain the integrity and inspectability of records and ensure end-to-end integrity of information before signing (BCB 85, Art. 3º-A, I, 'e'). | **Veritas Evidence Chain**: an append-only, hash-linked audit/query ledger with terminal evidence sealed by signed export to storage under a retention lock — making any attempt to rewrite history tamper-evident, and binding integrity before the decision is sealed. |
| **EU AI Act** | Art. 12 | Automatic recording of events (logging) over the system's lifetime. | **Veritas Evidence Chain**: every decision emits a retained, re-verifiable evidence record (policy version + input digest + outcome). |
| **LGPD** | Art. 20 | Right to review of decisions taken solely by automated processing, and to request information about the criteria used. | **REX pattern + Bounded-Output Rationale**: each decision binds the digest of a structured, human-readable rationale and the active policy version, so the criteria of a past decision can be reconstructed and reviewed. |
| **GDPR** | Art. 22 | Safeguards around solely-automated decision-making. | **Deterministic execution**: a decision is a traceable product of explicit facts under a signed policy version — reconstructable rather than post-hoc rationalized. |

> **Note.** **CMN 4.893/2021** and **BCB 85/2021** are *cybersecurity* norms (as amended by **CMN 5.274/2025** and **BCB 538/2025** respectively, with an adequacy deadline of 01/03/2026). They are **not** AI-explainability mandates; the explainability anchor in Brazil is **LGPD Art. 20**. Do not cite the cybersecurity norms as standalone explainability requirements.

---

## 3. Data Minimization & Privacy by Design

| Regulation | Article | Requirement | ATI architectural response |
| :--- | :--- | :--- | :--- |
| **GDPR** | Art. 25 | Technical measures to ensure only necessary data is processed (privacy by design and by default). | **State Capsule**: the engine sees only the capsule (scores/flags/proofs), never raw PII or identity documents. |
| **LGPD** | Art. 46 | Adopt security, technical and administrative measures to protect personal data. | **Perimeter & runtime isolation**: workloads run under kernel-level / confidential-computing isolation; In-Perimeter Intelligence keeps sensitive context inside the institution's own boundary. |

---

## 4. Governance & Integrity

| Regulation | Article | Requirement | ATI architectural response |
| :--- | :--- | :--- | :--- |
| **CMN 4.968/2021** | Internal controls | Maintain internal-controls systems compatible with the institution's risk profile, with defined responsibility and oversight. | **Multi-Sig Policy Governance**: changes to rules require M-of-N consensus and separation of duties, preventing unilateral insider modification. |
| **CMN 4.893/2021** *(as amended by CMN 5.274/2025)* · **BCB 85/2021** *(as amended by BCB 538/2025)* | Cybersecurity controls | Restrict third-party access to private keys (BCB 85, Art. 3º-A, I, 'f'). | **Key & Retention Plane**: signing and retention keys are HSM-backed and governed so that third parties do not gain access to private key material; environments do not share keys. |
| **SOX** | Sec. 404 | Internal control report accreditation. | **Veritas proofs**: every decision emits evidence binding policy version + input + output, supporting independent attestation. |

---

[⬅️ Back to the ATI Index](../README.md) · [Category Thesis](../category/00_category-thesis.md) · [Compliance & QA Kit](README.md)
