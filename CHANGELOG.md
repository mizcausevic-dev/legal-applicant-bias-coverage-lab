# Changelog

## [0.1] — 2026-05-30

### Added

- Initial profile.
- 8 subgroup taxonomies including three LegalTech-unique: indigent_defendant_status (Sixth Amendment), immigration_status_disclosed (INA), criminal_history_band (FBI NCIC).
- 11 coverage statuses including two LegalTech-unique: compas-cautionary-pattern-detected (ProPublica 2016 reference) + batson-pattern-detected (Batson v. Kentucky framework). Plus indigent-defendant-disparity-detected (Sixth Amendment effective assistance).
- 12 required metrics including legal-specific: ediscovery-tar-precision-recall-per-document-language, interpreter-availability-attestation-when-LEP-disclosed, appeal-overturn-rate-of-ai-recommended-outcomes-per-subgroup, human-attorney-override-rate-per-subgroup.
- 7 additional dimensions covering case venue, matter funding source, eDiscovery document language, represented-vs-pro-se, outcome path, appellate stage, interpreter requirement.
- High-stakes freshness window (P30D) for sentencing recommendations, pretrial detention risk, immigration triage, and criminal defense strategy.
- Audit-stream coupling: supervising-attorney review required on four trigger categories (four-fifths-violation, compas-cautionary-pattern-detected, batson-pattern-detected, indigent-defendant-disparity-detected).
- Cross-reference to all 5 LegalTech 6-pack siblings.

### Not yet

- Court-system AI (judicial use rules — bind judges not attorneys).
- Tribal court systems.
- Foreign jurisdictions (Solicitors Regulation Authority bias frameworks).
- Per-state overlay datasets (state bar disparate-impact opinions are referenced inside families).
