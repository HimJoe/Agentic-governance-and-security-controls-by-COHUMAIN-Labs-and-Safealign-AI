# Changelog

All notable changes to this standard are documented here. Format follows
[Keep a Changelog](https://keepachangelog.com/); versioning is [SemVer](https://semver.org/).

## [Unreleased]
### Proposed
- Evidence grade (E0 asserted / E1 logged / E2 signed by the actor / E3 signed by the accountable human, independently verifiable) as an attribute per evidence item, with floors per tier; RFC by an implementer, see `docs/conformance.md`.
### Added
- `docs/implementations/xchk.md`: an implementer's self-assessment of a runtime authorization component against the 25 controls (not a conformance claim).

## [1.0.0], 2026
### Added
- Initial public release of the **Agentic Governance & Security Controls** standard.
- 25 controls across four pillars: Safety (5), Alignment (5), Governance (8), Security (7).
- Full mappings per control: MIT AI Risk Repository, MITRE ATLAS, MITRE ATT&CK (via the Anthropic LLM ATT&CK Navigator), and EU AI Act / NIST AI RMF / ISO 42001.
- Three conformance tiers (Foundational / Managed / Assured).
- Machine-readable `controls.json` and `controls.csv`.
- 14-tab companion workbook.
- GitHub Pages website.
