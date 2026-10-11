# Risk Assessment Methodology

Assessment date: 2026-10-10. These are proposed lab judgments for a fictional business, not empirical probabilities, CVSS scores or CMMC scoring.

## Scales

| Score | Likelihood anchor | Impact anchor for the simulated business |
| --- | --- | --- |
| 1 | Rare: multiple unusual prerequisites | Negligible: brief local inconvenience |
| 2 | Unlikely: restricted path and substantial prerequisites | Minor: limited rework or short single-function disruption |
| 3 | Possible: credible path with enabling conditions | Moderate: material workflow disruption or limited sensitive-data exposure |
| 4 | Likely: weak protection against a plausible repeated threat | Major: extended critical-service disruption or broad exposure |
| 5 | Very likely: easily repeatable path with little resistance | Severe: enterprise identity/trust compromise or major simulated mission harm |

Risk score = likelihood x impact. Proposed bands: 1-4 Low; 5-9 Moderate; 10-16 High; 17-25 Critical. Thresholds are analyst assumptions, not framework-prescribed values. No likelihood value is a measured annual event frequency. Exposure uncertainty is recorded in each rationale.

## Initial Baseline Ratings

The values below are the original pre-remediation judgments, retained for traceability. They are not current residual ratings. REM-01/02/03 now substantiate AD configuration remediation for R-006/R-007; enforcement tests remain pending.

| Risk | Likelihood | Impact | Score | Band | Main judgment |
| --- | --- | --- | --- | --- | --- |
| R-001 OIDC cutover incomplete | 3 | 4 | 12 | High | Intended identity enforcement is not promoted; existing Basic service is not assumed unauthenticated |
| R-002 CA key on application host | 3 | 5 | 15 | High | Host compromise could expand into certificate-signing trust compromise |
| R-003 AD DNS inconsistency | 3 | 3 | 9 | Moderate | Root-query discrepancy could disrupt dependent workflows; complete DNS outage is not established |
| R-004 broad NAT-side SSH rule | 3 | 4 | 12 | High | Management rule is broader than needed; real NAT forwarding/Internet reachability is unknown |
| R-005 development-file database | 3 | 4 | 12 | High | Operator-confirmed configuration lacks proven production persistence/restore suitability |
| R-006 minimum password length 7 | 4 | 4 | 16 | High | Short passwords raise guessing risk despite complexity; actual password strength is unknown |
| R-007 lockout threshold disabled | 4 | 5 | 20 | Critical | Repeated AD guesses lack demonstrated attempt limiting; alternatives are not assessed |
| R-008 incomplete Windows Security Audit Coverage | 3 | 4 | 12 | High | Proposed initial coverage-risk judgment; selected settings remediated, but full event/SACL/persistence/retention/collection assurance pending |

R-006 and R-007 interact; do not sum scores or treat them as independent financial losses. Impact 5 for R-007 reflects potential identity compromise, not an observed compromise. Missing controls are uncertainty, not proof that all compensating controls are absent.

## Treatment and Acceptance

R-008 uses the existing proposed 1-5 scoring scheme; its 12/High is an initial readiness judgment, not a measured residual score. Configuration before/after, one 4688 event and one successful policy refresh are observed; other categories, SACLs and full operational coverage remain unverified. [Audit report](../Reports/Windows-Audit-Policy-Remediation.md) defines closure evidence. No existing R-001 through R-007 score/status changed.

Five records remain Open. R-006/R-007 are configuration remediated, enforcement testing pending; R-008 is configuration remediated, validation pending. None is closed. Proposed treatment is Mitigate. Owner roles and dates are planning suggestions, not assignments or agreed SLAs. Due dates use calendar days from the 2026-10-10 assessment baseline and require stakeholder approval. No regulatory CMMC POA&M deadline or eligibility is inferred.

Closure needs owner-produced evidence, independent verification where feasible, and risk-owner approval. Repeat ratings after tests. Leave residual scores unassessed until enforcement verification; configuration checks alone do not justify a measured risk reduction. The fictional sponsor would approve scope, parameters and risk acceptance, but no acceptance decision exists.

Use examination, operator statements and targeted future tests. This review is evidence-limited and nonintrusive. Full assessment would require policies, interviews, configuration exports and assessment-objective testing across the actual boundary.

## RMF Learning Workflow

The expanded [RMF lifecycle](../RMF/RMF-Lifecycle.md) defines each step, current artifacts and proposed review gates, including hypothetical categorization and simulated authorization. The [six-field matrix](../Control-Mapping/Control-Assessment-Matrix.md) uses Met, Partially Demonstrated, Not Met and Not Assessed as local readiness labels, explicitly distinct from formal CMMC findings. [Evidence traceability](../Control-Mapping/Evidence-Traceability.md) separates observed screenshots, operator-confirmed details, historical configurations and missing evidence. No risk rating or closure changed as a result of this mapping.

This table applies the [SP 800-37 Rev. 2 process](https://csrc.nist.gov/pubs/sp/800/37/r2/final) to a simulated engagement. It is not an official authorization package.

| RMF step | Project artifact / activity | Actual status |
| --- | --- | --- |
| Prepare | Fictional mission, boundary, assets and proposed responsible roles | Drafted; stakeholder approval not obtained |
| Categorize | Describe simulated information and potential business impacts in SSP/BIA | Proposed context only; no official FIPS 199 determination |
| Select | Identify selected control themes and readiness gaps | Partial mapping; no complete baseline or tailoring approval |
| Implement | Describe safeguards, AD configuration remediation and remaining actions | Operator completed AD changes; maintainer only organized evidence/documents |
| Assess | Review screenshots, distinguish gaps and propose verification | Evidence-limited review; full objective coverage missing |
| Authorize | Present executive decision recommendation and residual uncertainty | No authority-to-operate or risk acceptance granted |
| Monitor | Propose recurring evidence/risk review and change-triggered reassessment | Planning assumption; monitoring program not verified |

Phase 5 BIA provides proposed business impacts and recovery priorities for Prepare/Categorize discussions; it does not establish an official security category. Its investment model supports a hypothetical management decision, not Authorize or formal residual-risk acceptance. The [selected control review](../Control-Mapping/NIST-CMMC-Control-Assessment.md) lists observed safeguards, gaps and assessor evidence still required. R-006/R-007 remain pending enforcement, and no status changes result from BIA arithmetic alone.
