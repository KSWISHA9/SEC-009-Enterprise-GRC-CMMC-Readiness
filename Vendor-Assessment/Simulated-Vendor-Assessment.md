# Simulated Vendor and Dependency Assessment

v1.0 named-vendor review: [Atlantic Defense Cloud Services](Atlantic-Defense-Cloud-Services-Assessment.md). All five selected safeguards are Unverified because no documentation was supplied; recommendation is defer approval pending evidence, not confirmed noncompliance. This older supplier-archetype questionnaire remains supplemental planning context and contains no vendor responses.

**Hypothetical due-diligence exercise only.** OmniVerse Defense Systems and the supplier archetypes below are fictional. No provider was contacted, contracted, audited or approved. No actual CUI, supplier response, certification report or contractual assurance exists. The local lab's VirtualBox/Keycloak usage does not establish a third-party managed-service engagement.

## Proposed Scope and Data Handling

Assess how a future support, backup or PKI dependency could affect identity, application availability and simulated sensitive-data handling. Determine data access, administrative reach, key access, backup contents, locations and subcontractors before selecting a provider. Criticality values and roles are planning assumptions; do not create an overall vendor compliance score from unanswered questions.

| Hypothetical supplier archetype | Proposed dependency / access | Proposed criticality | Evidence and disposition |
| --- | --- | --- | --- |
| Managed backup provider | VM/app/IdP configuration and potentially dummy engineering records | High: recovery and data-access dependency | No provider selected or responses received; Not assessed / approval pending |
| PKI signing service | Certificate issuance and CA signing process; not application credentials | High: signing-trust dependency | R-002 co-location motivates proposed separation; no provider or contract verified |
| Platform/identity support provider | Privileged maintenance of host, AD or Keycloak | High: administrative dependency | No actual external admin access verified; questions only |

## Proposed Questionnaire and Required Evidence

| Topic | Question / requested artifact | Current answer |
| --- | --- | --- |
| Scope/data location | What information, privileges, regions and subcontractors are involved? Provide a scoped data-flow and access inventory | Not provided |
| Access governance | Are named admin identities, MFA, least privilege, access reviews and offboarding enforced? Provide sanitized policy/test evidence | Not provided |
| Cryptography/key custody | Who controls CA/backup keys, what lifecycle applies, and what validated modules are used where required? Never request private keys | Not provided |
| Recovery | What RTO/RPO is contractually supported and what restore tests demonstrate it? Provide sanitized reports and coverage | Not provided; lab BIA targets are not supplier commitments |
| Incident response | What are reporting/escalation obligations, evidence preservation and notification timelines? Provide contractual commitments | Not provided; no invented legal deadline |
| Vulnerability/change management | How are patching, testing, rollback and supported versions maintained? Provide scoped process/evidence | Not provided |
| Assurance applicability | What independent assurance applies to the exact service/boundary and period? Validate scope and exceptions rather than relying on logos | Not provided; no certification asserted |
| Exit/return/deletion | How are access revoked, keys rotated, data returned/deleted and backups expired? Provide proposed contract terms | Not provided |

## Proposed Decision and Follow-Up

No supplier is approved. Proposed responsible role is the GRC lead with the platform/IAM/PKI owners; actual assignments and review dates remain unapproved. Any real contract/data requirement must be established before determining provider obligations. Selected NIST/CMMC mappings in this project do not constitute a provider certification.

Use [BIA](../BIA/Business-Impact-Analysis.md) targets as negotiation assumptions only. Evaluate shared responsibility and common-mode dependencies in the [SSP](../SSP/System-Security-Plan.md). Record actual responses, exceptions, compensating controls and acceptance authority if a real assessment is later authorized. This simulation does not itself add a technical risk or close any existing risk.
