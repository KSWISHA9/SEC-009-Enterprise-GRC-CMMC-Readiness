# Atlantic Defense Cloud Services - Third-Party Risk Assessment

SEC-009 v1.0. Review date: 2026-10-10. **Fictional vendor; simulated due diligence only.** No vendor documentation was supplied. No contact, contract, service deployment, certification, CUI handling or vendor test is represented. Proposed owner: GRC Lead with IAM, platform and business-risk owners; no assignment or approval exists.

## Scope and Decision

Atlantic Defense Cloud Services is evaluated as a hypothetical future cloud/support and recovery supplier to fictional OmniVerse Defense Systems. Service scope, locations, subcontractors, administrative privileges, data access and shared responsibilities have not been established. These proposed use cases do not add the vendor to the current lab boundary or imply existing access.

**Recommendation: defer approval pending evidence.** All five safeguards below are unverified. Missing documentation is an assurance gap, not confirmed noncompliance, proof that a safeguard is absent, or an official NOT MET finding. No vendor risk score, approval, certification outcome or inherited control credit is assigned. This vendor exercise is separate from the eight technical risks; it does not invent R-009.

## Selected Safeguard Assessment

| ID | Safeguard / assessment objective | Evidence requested | Evidence received | Status | Proposed follow-up |
| --- | --- | --- | --- | --- | --- |
| V-01 | Incident response: determine readiness, coordination and customer notification for the proposed service | Scoped response plan, responsibilities/escalation contacts, sanitized exercise results, evidence-preservation process and proposed contractual notification terms | None supplied | Unverified | Obtain and review service-specific material; validate notification obligations against actual applicable contract rather than inventing deadlines |
| V-02 | Privileged MFA: determine whether all applicable administrative paths enforce MFA and controlled exceptions | Admin-path inventory, MFA policy, sanitized enforcement/negative-test evidence, emergency-access process and privileged-access review records | None supplied | Unverified | Verify scope, technical enforcement and exception monitoring; do not treat a marketing statement or product capability as implementation proof |
| V-03 | Encryption: determine protection of applicable data at rest/in transit and key custody | Scoped data-flow/crypto configuration, key ownership/access/lifecycle records, certificate/trust evidence and module assurance where applicable | None supplied | Unverified | Establish data types and requirements, then review actual configuration and key protection without requesting passwords or private keys |
| V-04 | Backup/recovery: determine recoverability and alignment with proposed business targets | Backup scope/schedules/retention, protected-copy architecture, restore reports with timestamps and recovered data points, dependencies and contractual RTO/RPO commitments | None supplied | Unverified | Compare verified service capabilities with the BIA after scope is defined; lab targets are proposals, not vendor commitments or achieved recovery |
| V-05 | Applicable CMMC evidence: determine applicability and scoped assurance for the proposed service | Contract/requirement basis, service/system boundary, shared-responsibility matrix, relevant current assessment/status/affirmation evidence where required, scope/period/exceptions and permitted supporting records | None supplied | Unverified | Determine obligations first, then validate authentic service-specific evidence and coverage; no assumed certification or exemption |

All requested documents and tests are future review inputs, not claims they exist. Accept only sanitized evidence through an approved process; do not store real CUI, raw secrets, private keys or restricted vendor reports in a public portfolio.

## Applicability and Assessor Limits

CMMC review must follow the actual requirement, service role and assessment boundary rather than assuming every supplier must hold the same status. The project distinguishes SP 800-53 Rev. 5 from SP 800-171 Rev. 2 and the incorporated Level 2 model. Contract applicability, provider scoping and authentic evidence would need review in a real engagement. See [official 32 CFR Part 170](https://www.govinfo.gov/link/cfr/32/170?link-type=pdf&year=mostrecent) and the project's [framework overview](../Control-Mapping/NIST-CMMC-Control-Assessment.md). No full requirement/objective assessment, official finding, CMMC certification or actual authorization is issued here.

The [BIA](../BIA/Business-Impact-Analysis.md) proposes AD/DNS and Keycloak RTO 2h/RPO 1h and portal RTO 4h/RPO 2h. These are hypothetical business inputs. Do not transpose them into supplier SLAs or presume the provider can meet them. The [SSP](../SSP/System-Security-Plan.md) includes only the existing local assets, not a vendor service. There is no approved third-party dependency to inherit.

## Evidence Gate Before Any Proposed Approval

1. Establish service/data/admin scope, locations, subcontractors, applicable obligations and shared responsibilities.
2. Collect the five scoped evidence packages; record provenance, dates, reviewer and validity without publishing sensitive records.
3. Assess coverage and exceptions using examination and approved tests/interviews; keep unanswered questions unverified.
4. Evaluate recovery dependencies and applicable requirements; obtain approved contract terms and proposed treatment for actual substantiated gaps.
5. Present a documented recommendation to the legitimate business-risk/procurement authority. Until then, maintain defer approval pending evidence.

No review date or procurement commitment is approved. [Finalization status](../Reports/Finalization-v1.0.md) tracks missing vendor evidence alongside lab validation gaps. The older [supplier-archetype questionnaire](Simulated-Vendor-Assessment.md) remains supplemental planning context, not vendor answers.
