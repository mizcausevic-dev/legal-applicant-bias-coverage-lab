# legal-applicant-bias-coverage-lab

> **LegalTech Evidence Bundle (bias) — Spec #4 of the LegalTech 6-pack.** Profile of the [Evidence Bundle spec](https://github.com/mizcausevic-dev/evidence-bundle-spec) scoped to legal-AI bias evidence: AI-assisted jury selection (Batson framework), sentencing recommendations (post-ProPublica COMPAS cautionary), immigration triage, public defender caseload, eDiscovery predictive coding (TAR), civil rights case screening.

Part of the [Kinetic Gain Protocol Suite](https://suite.kineticgain.com).

> Status: v0.1 draft. Profile at [`profile.json`](./profile.json).

## Anchored to

- **Title VI** Civil Rights Act (federal financial assistance) + 28 CFR §42.405(d) LEP obligations
- **Title VII** Civil Rights Act (employment context — for in-house counsel)
- **Sixth Amendment** effective assistance of counsel (Gideon v. Wainwright + indigent defendant pathway)
- **Fourteenth Amendment** Equal Protection (criminal sentencing, jury selection)
- **Batson v. Kentucky** (peremptory challenge framework)
- **ABA Criminal Justice Standards** + ABA Standards on Sentencing
- **State bar disparate-impact frameworks** (state-specific overlays)

## Subgroup taxonomies (8)

| Taxonomy | Source |
| --- | --- |
| race_ethnicity | OMB SPD 15 (revised March 2024) |
| sex_at_birth | OMB SPD 15 |
| disability_status | ADA Title II + Section 504 |
| age_band | ADEA + juvenile-justice frameworks |
| limited_english_proficiency | Title VI implementing regulations |
| **indigent_defendant_status** | **Sixth Amendment + state public-defender eligibility** |
| **immigration_status_disclosed** | **INA + state-AG non-disclosure rules** |
| **criminal_history_band** | **FBI NCIC categories + state criminal-history** |

The bottom three are LegalTech-unique versus the sibling-vertical bias profiles — they exist because legal-AI tools must be evaluated for differential treatment by indigent vs retained-counsel clients, by immigration-status, and by criminal-history band.

## LegalTech-distinctive coverage statuses

Two coverage_status values that don't appear in sibling-vertical bias profiles:

- **`compas-cautionary-pattern-detected`** — matches the pattern ProPublica found in their 2016 COMPAS analysis (higher false-positive rate for one subgroup AND higher false-negative rate for another). Triggers model-card disclosure to client + tribunal.
- **`batson-pattern-detected`** — AI-assisted peremptory-strike recommendations show statistically significant subgroup-disparate pattern. Triggers Batson v. Kentucky framework review BEFORE attorney acts on the recommendation.

Plus **`indigent-defendant-disparity-detected`** — surfaces a different failure mode: when public-defender-assigned clients receive systematically lower-quality AI recommendations than retained-counsel clients. That's Sixth Amendment effective-assistance + state public-defender equity at the AI layer.

## Required metrics (12)

12 metrics per subgroup — including standard recommendation/rejection rates and selection-rate ratio, plus LegalTech-specific:
- `false-positive-rate-per-subgroup` + `false-negative-rate-per-subgroup` (driven by the COMPAS-cautionary check)
- `ediscovery-tar-precision-recall-per-document-language` (Title VI LEP + TAR predictive coding accuracy)
- `interpreter-availability-attestation-when-LEP-disclosed`
- `appeal-overturn-rate-of-ai-recommended-outcomes-per-subgroup`
- `human-attorney-override-rate-per-subgroup` — surfaces when supervising attorneys are routinely overriding the AI vs trusting it

## Audit-stream coupling

When coverage status triggers a finding, the lab emits to the sibling [`matter-decision-record-audit-stream`](https://github.com/mizcausevic-dev/matter-decision-record-audit-stream) with `supervising_attorney_review_required = true` on four trigger categories: `four-fifths-violation`, `compas-cautionary-pattern-detected`, `batson-pattern-detected`, `indigent-defendant-disparity-detected`. This is what couples the bias lab to the runtime audit stream — a bias finding can't sit in a spreadsheet; it becomes an audit event that blocks production-ready AI output until cleared.

## Use

```bash
# Validate the profile is well-formed
node -e "JSON.parse(require('fs').readFileSync('profile.json','utf8'))"
```

## Composes with

- [`evidence-bundle-spec`](https://github.com/mizcausevic-dev/evidence-bundle-spec) — the upstream spec this profile conforms to
- [`matter-decision-record-audit-stream`](https://github.com/mizcausevic-dev/matter-decision-record-audit-stream) — emits coverage-finding events into the audit-stream
- [`aba-rule-1-6-readiness-evidence-bundle`](https://github.com/mizcausevic-dev/aba-rule-1-6-readiness-evidence-bundle) — sibling compliance Evidence Bundle
- [`state-bar-ai-disclosure-tracker`](https://github.com/mizcausevic-dev/state-bar-ai-disclosure-tracker) — sibling state-bar lifecycle tracker
- [Kinetic Gain Protocol Suite](https://suite.kineticgain.com) — umbrella

## Compliance posture

**Bias-readiness scaffolding** for legal-AI tools. Producing a complete bundle is evidence of program maturity, not certification that an AI tool is non-discriminatory. Per the standing public-language guardrail across the Suite.

## License

Profile + supporting documentation: MIT.
