# Changelog

All notable changes to the ATI public canon are documented here.
This repository follows Semantic Versioning (`MAJOR.MINOR.PATCH`).

## 2.0.0 — Re-based on ATI as the category

This is a clean re-foundation of the public repository. The base identity is now
**ATI — Auditable Trust Infrastructure** (the category), with the prior F2F-RAaT
specification re-positioned as one framework among several.

### Changed
- Repository root is now the **category**: `README.md` is the ATI manifesto; the
  four-part narrative lives in `category/`.
- Frameworks (`f2f-raat`, `spezzatura`, `state-capsule`, `burn-engine`, `veritas`,
  `threat-model`) moved under `modules/frameworks/`.
- Products moved under `modules/products/` (REX Guard is the reference product).
- Supporting pillars promoted to clear top-level folders: `governance/`,
  `compliance/`, `interface-contracts/`, `cookbooks/`, `whitepaper/`,
  `reference-architecture/`. Glossary promoted to root `GLOSSARY.md`.
- All directory names normalized to lowercase-kebab; internal cross-links rewritten
  to the new structure.

### Fixed
- Corrected a swapped pair in the category narrative (the "Cognitive Auditability"
  and "Strategic Impact" files had their contents transposed) and the broken
  self-referencing navigation link.
- Removed an unverifiable financial proof claim from the strategic narrative and
  added an honest note on the provenance of efficiency figures.

### Removed (noise / non-public)
- Duplicated v1.0 specification tree that shadowed the canonical v1.1 content.
- A document classified *Confidential — Controlled Circulation* that did not belong
  in a public repository.
- An internal Firebase infrastructure blueprint, an internal onboarding roadmap,
  an internal work-summary, and a stale "Production Ready"-badged draft README whose
  license and status claims conflicted with the canon.

## 1.1.0 — F2F-RAaT specification update
- OpenAPI updated to 1.1.0; full T² vector set (U, R, Â) added; `effects` map added
  to the execution result.
- Hardened State Capsule schema; concrete numeric examples for vector calculation;
  standardized Fact schemas; updated cookbooks.

## 1.0.0 — Initial public specification
- Core whitepaper, execution contract and invariants.
- Spezzatura, State Capsule, Burn Engine, and Veritas specifications.
- Initial threat model and governance documents.
