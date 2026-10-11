# NIST RMF Lifecycle - Simulated Lab Assessment

Date: 2026-10-10. System: fictional OmniVerse Defense Systems engineering workspace. This document applies the seven-step structure of [NIST SP 800-37 Rev. 2](https://csrc.nist.gov/pubs/sp/800/37/r2/final) as a portfolio learning exercise. It does not execute every RMF task or issue an authorization. No actual authorizing official, federal system, defense contract or real CUI exists.

## Prepare

v1.0 package status: [finalization review](../Reports/Finalization-v1.0.md). The [Atlantic Defense Cloud Services due-diligence exercise](../Vendor-Assessment/Atlantic-Defense-Cloud-Services-Assessment.md) adds five unverified supplier questions, not an approved dependency, ninth confirmed technical risk or inherited safeguard. Defer vendor approval pending documentation. Documentation finalization does not alter the simulated authorization recommendation.

**Current artifacts:** [asset inventory](../Asset-Inventory.csv), [SSP boundary](../SSP/System-Security-Plan.md), [risk methodology](../Risk-Assessment/Methodology.md), [BIA](../BIA/Business-Impact-Analysis.md) and simulated vendor questions. Boundary includes OV-DC01, Ubuntu, Kali and the VirtualBox host; shared disks, power, virtual networking, trust material and outbound paths matter. No AD-to-Keycloak federation is verified.

**Proposed responsibilities:** fictional sponsor/risk owner approves scope and resources; GRC maintains assessment; AD, IAM, PKI and platform roles implement safeguards; independent reviewer examines closure evidence. These are roles, not assigned staff. Next gate: approve scope, data types, dependencies, risk tolerance and evidence-handling rules. Never introduce real CUI into this lab.

## Categorize - Hypothetical Only

Illustrative scenario: future sensitive contractor engineering records could suffer consequential unauthorized disclosure, modification or service disruption. For this exercise only, propose confidentiality Moderate, integrity Moderate and availability Moderate, with a Moderate high-water-mark system category. This is an assumed scenario, not a determination about the existing dummy data, actual CUI types, mission impact or contractual obligations.

The severity logic is informed by [FIPS 199](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.199.pdf); actual categorization would require information-type analysis, business-owner input and approval. A hypothetical Moderate category does not automatically prescribe CMMC obligations or select a full federal baseline. Proposed AD/DNS and Keycloak RTO/RPO are 2h/1h; portal 4h/2h. None is measured or approved. Next gate: validate information types and consequences before any real categorization.

## Select

The [control matrix](../Control-Mapping/Control-Assessment-Matrix.md) contains selected SP 800-53 Rev. 5 catalog references and separately identified SP 800-171 Rev. 2/CMMC Level 2 requirements. These are educational, evidence-driven selections, not an approved SP 800-53B baseline, complete tailoring record or all 110 requirements.

Next gate: establish applicable framework/contract, approved baseline or requirement scope, organization-defined parameters, inherited controls, exceptions and assessment objectives. Do not infer framework equivalence from related topics. CMMC applicability is not established merely by choosing a fictional defense-contractor scenario.

## Implement

Observed safeguards include UFW default-deny inbound/source restrictions, later CA-verified HTTPS, test-app role behavior, firewall logs and AD configuration remediation. Earlier HTTP/Basic authentication was superseded by HTTPS Basic on managed port 8443; OIDC/RBAC remains on manually launched test port 8445. Keycloak uses 8444. OIDC production cutover and reboot persistence remain incomplete.

AD minimum length changed 7 to 14, threshold 0 to 10; complexity remains enabled and duration/window remain 30 minutes. The operator made these changes; the maintainer reviewed evidence only. Implementation narratives are in the [SSP](../SSP/System-Security-Plan.md) and [AD report](../Reports/AD-Password-Policy-Remediation.md).

Next gate: approve and implement remaining changes through controlled workflows, protect keys/secrets, document rollback and obtain sanitized evidence. This assessment does not modify VMs or execute remediations.

## Assess

Method: examine existing files and screenshots, compare before/after and independent command outputs, and distinguish operator reports from visual observations. No live VM tests or formal assessor interviews occurred. [Traceability](../Control-Mapping/Evidence-Traceability.md) lists exact sources and gaps. Narrow positive/negative tests support safeguards, not full objective coverage.

The matrix uses local readiness statuses, not official CMMC findings. No full MET determination is issued. R-006/R-007 remain configuration remediated, enforcement testing pending. Historical recovery establishes stop/start of the earlier 8080 app only; no current-stack restore, valid-login retest or achieved BIA target is inferred. Eight risks remain unclosed.

Next gate: use approved assessment plan, full applicable objectives and independent examination/interview/testing; corroborate OIDC status/identity, AD enforcement, effective network paths, TLS/key management, retention and data restoration. The BIA's financial model is hypothetical analysis, not technical effectiveness evidence.

## Authorize - Simulated Recommendation Only

**Recommended fictional decision:** continue isolated lab learning and controlled evidence collection; do not approve production use, introduce real CUI, claim CMMC compliance or issue an actual ATO on this package. This is an advisory simulation, not a signed risk acceptance, operational authorization or denial by a real official.

Decision inputs: [executive report](../Reports/Executive-Security-Assessment.md), draft SSP, selected matrix, eight-risk register and [POA&M](../POAM/Plan-of-Action-and-Milestones.csv). R-001 cutover, R-002 signing-key separation, R-003 DNS, R-004 broad SSH and R-005 database remain Open. R-006/R-007 require enforcement verification and acceptance. Scores/owners/dates are proposed; no residual ratings or risk acceptance are established.

Before any real authorization recommendation: validate scope and evidence completeness, resolve or formally treat applicable findings, verify required controls and recovery capabilities, obtain business-owner input and route the package to the legitimate decision authority. Completion of these eight actions alone would not establish enterprise or CMMC readiness.

## Monitor

R-008 audit configuration is remediated with one process-event and one refresh observation, but full event/SACL/persistence/retention/central-collection validation remains pending. This complements, rather than establishes, the proposed monitoring program. See the [audit report](../Reports/Windows-Audit-Policy-Remediation.md). No authorization or residual-risk acceptance changed.

Proposed cadence: review evidence/risk/POA&M monthly and after material changes; review privileged membership, failed logons, firewall denials, IdP/app events, certificate expiry and configuration drift. Define owners, retention, alert escalation and reassessment triggers. No operating continuous-monitoring program is claimed.

Triggers include OIDC promotion, Keycloak/database changes, CA custody changes, DNS correction, network/host changes, AD policy changes and recovery tests. For each, capture sanitized before/after evidence, update SSP/matrix/risks and obtain closure acceptance. New findings must not be hidden by marking a portfolio deliverable complete.

## Readiness Gates

| Gate | Current state / required next evidence |
| --- | --- |
| Scope and categorization | Fictional scope documented; category proposed only; real approval absent |
| Selection and parameters | Selected references verified; full baseline, tailoring and requirement coverage not performed |
| Implementation assurance | Useful local safeguards; managed OIDC, key separation, DNS, SSH and database gaps open |
| AD enforcement | Configuration corroborated; dedicated-account enforcement/recovery evidence pending |
| Recovery capability | Historical restart only; approved backups/restoration and measured RTO/RPO absent |
| Assessment and acceptance | Evidence-limited local review; no official CMMC findings or residual-risk acceptance |
| Publication | No approval; preserve originals, exclude actual secrets and follow current supporting/archive screenshot dispositions, resolve sibling-link portability |

Portfolio documentation can describe these completed assessment activities honestly while remediation remains unfinished. Documentation completeness is not system readiness, full Zero Trust, certification or an ATO.
