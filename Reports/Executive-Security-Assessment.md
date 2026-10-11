# Executive Security Assessment

Version: 1.0. Assessment date: 2026-10-10. Organization: fictional OmniVerse Defense Systems. **Simulated selected-control assessment finalized for portfolio review, not CMMC certification or production approval.** No real CUI or evidence of a security incident is present.

## Controlled Access-Control Addendum

[CMMC-AC-001](CMMC-AC-001-Controlled-Access-Control-Exercise.md) records 2,607 baseline users (2,594 enabled, 13 disabled), and Administrator as the sole listed Domain Admins/Enterprise Admins member. The operator intentionally gave a disabled test account Full Control on disposable simulated training data, then removed that explicit grant. ACL configuration is verified; no unauthorized access or exploitation was demonstrated. Later E-20/21 show a noninherited ACL with SYSTEM/Administrators Full Control and SECX002-Contractor-Readers Read, Synchronize; Users access removed. E-22 counters are 0 unexpected Allow ACEs, 1 reader ACE and Enabled False. The operator confirms PASS, but its printed line is not visible. **AC-007/008 now show read-only evaluated permissions for SECX002-Authorized and no evaluated grant for SECX002-Unauthorized. Current membership/nonmembership and both disabled states are operator-confirmed. No actual interactive login or file-read/denial attempt occurred.** The configured ACL matches the narrow lab policy, not complete operational authorization. No new scored risk, closure of the existing eight risks, CMMC certification or complete requirement satisfaction is inferred.

## Decision Summary

### Configuration Drift - CMMC-CM-001

The operator reports detecting simulated AuditLogging drift from Enabled to Disabled and restoring the setting to Enabled. The final SHA-256 differs from the original trusted baseline, so **exact byte-level recovery verification is OPEN, not PASS**. Original baseline/restored files, hashes, validator/output and screenshots are missing from the host package. See [drift and recovery record](CMMC-CM-001-Configuration-Drift-and-Recovery.md). This supplemental exercise is not an invented ninth scored risk, a successful restore or full compliance evidence.

[SOC-001: Entra Connect service-account authentication investigation](SOC-001-Entra-Connect-Service-Account-Authentication-Investigation.md) reviews same-second 4625/4624 events for ADSyncMSA7efbc$ and a currently running ADSync service. Assessment: possible transient credential issue, root cause unconfirmed, low observed security concern and no demonstrated malicious activity. Monitor recurrence and verify actual synchronization health; successful authentication/service status does not establish healthy synchronization. Do not reset service credentials without further diagnosis. Eight tracked risk statuses remain unchanged.

The lab demonstrates useful safeguards: active default-deny Ubuntu UFW, private-CA HTTPS, a running identity provider and operator-confirmed analyst/viewer RBAC on a test app. AD firewall profiles are enabled and password complexity is enabled. These are foundations, not proof that the intended identity deployment or all contract requirements are complete.

Eight risks remain unclosed: five Open, two AD configuration remediated/enforcement pending, and one Windows audit configuration remediated/validation pending. Original pre-remediation judgments were one Critical, six High and one Moderate; they are not current residual ratings, official CMMC scores or additive losses. Recommended decision for the fictional sponsor: continue verification and remediation; do not introduce real CUI or claim a compliant enclave on this evidence.

## Assessment Boundary and Technical Evidence

The [inventory](../Asset-Inventory.csv) contains three VirtualBox VMs: OV-DC01 (Windows Server 2022, 10.10.10.10, 8 GB/4 vCPU), Ubuntu-Server (10.10.10.101, 4 GB/2 vCPU) and Kali (10.10.10.100, 4 GB/2 vCPU). Each uses NAT plus host-only adapters. The Windows VirtualBox host is a fourth supporting asset inside the assessment boundary; its full specifications and protections remain unverified. Resources are guest allocations, not four separately inventoried VMs. The hypothetical vendor is not a deployed asset or inherited security provider.

Ubuntu evidence shows active UFW/default-deny inbound and Kali-source rules, with a broad NAT-side SSH exception still open. Read-only SEC-008 evidence supports historical authorized/denied access, UFW denial logging, server-certificate validation against the private lab CA and a remote CA-verified HTTPS 401 challenge. HTTPS trust evidence is not an authenticated-content or full crypto-assurance test.

Managed 8443 remains the HTTPS Basic app, Keycloak HTTPS uses 8444, and OIDC/RBAC was tested on manually launched 8445. Analyst authorized dashboard, viewer identity/role and Forbidden screenshots support the test behavior; ov-analyst/test port and the viewer's numeric 403 are operator-confirmed where not visible together. Keycloak 26.8.0/confidential authorization-code setup and token-validation implementation still require sanitized corroboration. No 8443 OIDC cutover or OIDC reboot persistence is claimed. See [traceability](../Control-Mapping/Evidence-Traceability.md).

## Validated AD Configuration Remediation

REM-01/02/03 substantiate length 7 to 14 and threshold 0 to 10. Complexity remains enabled; duration and observation window remain 30 minutes. PowerShell and `net accounts /domain` confirm configuration. The Administrator fine-grained-policy query has no displayed policy output. OV-DC01 reports baseline-export existence; content and restoration were not inspected. R-006/R-007 are not closed until enforcement/compatibility/recovery verification and acceptance. See [remediation report](AD-Password-Policy-Remediation.md).

## Windows Audit Update - R-008

### Final Validation Result

`gpupdate /force` completed successfully for both computer and user policies on OV-DC01 (command invocation operator-confirmed; success outputs and post-refresh settings observed in VAL-02). AD minimum length remained 14, threshold 10, and duration/observation window 30 minutes. Process Creation and Directory Service Changes remained Success; Credential Validation, Kerberos Authentication Service and Security Group Management remained Success and Failure. Event 4688 was successfully generated for `C:\Windows\System32\whoami.exe` (operator-confirmed generation; recorded path observed in VAL-01).

This is **successful configuration persistence through one Group Policy refresh**, not reboot persistence or full compliance validation. VAL-02 named Persistence in the update is already preserved as `VAL-02-Group-Policy-Refresh-Validation.png`; no new screenshot was invented or duplicated. The [audit report](Windows-Audit-Policy-Remediation.md) lists exact results and pending tests. R-006/R-007 enforcement and R-008 remaining operational audit validation are still pending; no risk is closed.

Selected Windows audit configuration has improved across five subcategories: Process Creation and Directory Service Changes changed from No Auditing to Success; Credential Validation, Kerberos Authentication Service and Security Group Management changed from Success to Success and Failure. Existing Security log was enabled with 104,488 records/128 MiB maximum, Logon Success and Failure, and a listed 4625 event. Event ID 4688 was successfully generated for whoami.exe (operator-confirmed generation; VAL-01 visually verifies the recorded process path). Settings were retained after one Group Policy refresh. These are useful narrow results, not complete detection coverage or all-category event tests.

R-008 carries proposed initial score 12/High and remains **Configuration remediated, validation pending**. Remaining event cases, directory SACL coverage, GPO provenance/reboot persistence, retention and centralized collection require validation. Proposed P-008 due date is 2026-10-24, not an approved deadline; appended order 8 is not a claim that audit assurance is lower urgency than every prior action. Coordinate it with R-006/R-007 immediately in the proposed plan. No residual reduction or closure is assigned. See [audit report](Windows-Audit-Policy-Remediation.md).

## Existing Remediation Sequence

| Order | Risk | Initial baseline score | Business concern and next action |
| --- | --- | --- | --- |
| 1 | R-007: AD attempt-limiting enforcement | 20 Critical | Configuration now threshold 10 with 30-minute timers; verify controlled limiting, recovery, alerts and account-specific behavior |
| 2 | R-006: AD password-strength enforcement | 16 High | Configuration now minimum 14; verify short-password rejection, representative-user policy and compatibility |
| 3 | R-002: CA signing key on app server | 15 High | A runtime-host compromise could expand to signing trust. Separate signing function and review lifecycle without exporting key contents |
| 4 | R-004: broad NAT-side SSH rule | 12 High | Reduce management exposure after confirming forwarding and an approved admin recovery path |
| 5 | R-005: development-file database | 12 High | Establish a supported database with backup/restore validation before OIDC promotion |
| 6 | R-001: incomplete OIDC cutover | 12 High | Promote only after database, token/session and service readiness; verify analyst/viewer behavior and rollback on 8443 |
| 7 | R-003: DNS inconsistency | 9 Moderate | Investigate domain-root versus locator behavior without calling this a complete AD/DNS outage |
| 8 (parallel verification) | R-008: Windows audit coverage | 12 High | Five settings remediated; validate remaining events/SACLs, full GPO persistence, retention/collection and acceptance alongside AD enforcement |

Order is a proposed planning choice based on scores and dependencies, not an emergency declaration. R-003 investigation can proceed in parallel. R-005 precedes R-001 despite equal scores because identity persistence is a promotion dependency. R-006/007 should be coordinated rather than treated as isolated fixes.

## Business and Resource Assumptions

Proposed responsible roles and calendar due dates are in the [POA&M](../POAM/Plan-of-Action-and-Milestones.csv); no staff assignments, funding or SLAs were approved. The [BIA](../BIA/Business-Impact-Analysis.md) proposes service targets and hypothetical financial arithmetic. Recovery targets are not verified, and host common-mode failure can prevent meeting proposed app/identity RTOs without additional infrastructure.

Phase 5 targets are AD/DNS 2-hour RTO/1-hour RPO, Keycloak 2-hour RTO/1-hour RPO and contractor portal 4-hour RTO/2-hour RPO. These supersede earlier draft values and require restoration testing, not simply active-service checks. Shared-host recovery is a prerequisite inside these deadlines.

The illustrative AD outage model assumes $200,000 modeled exposure, 25% exposure factor and 0.4 events/year: SLE $50,000 and ALE $20,000/year. With a hypothetical $6,000 annual control cost and assumed residual ALE $5,000/year, modeled reduction is $15,000/year and net benefit $9,000/year. Consider investment only after validating scope, efficacy and full costs. No actual loss, vendor quote, approved budget or achieved risk reduction was established. This financial residual input does not change R-006/R-007's pending enforcement status or unassessed residual ratings.

## Third-Party Decision

[Atlantic Defense Cloud Services](../Vendor-Assessment/Atlantic-Defense-Cloud-Services-Assessment.md) is fictional. Incident response, privileged MFA, encryption, backup/recovery and applicable CMMC evidence are all Unverified: no documentation was supplied. Defer approval pending scoped evidence. Do not treat unanswered questions as confirmed noncompliance or absent safeguards; no vendor certification, risk score, inherited controls or approval is represented. Service role/contract applicability and shared responsibilities must be established before any real supplier-assurance determination.

## Residual-Risk Limitations

The operator completed AD configuration remediation; the maintainer only updated documentation and evidence. Enforcement remains pending. Residual ratings remain unassessed, and no risk acceptance exists. Even completion of these eight actions would not establish full CMMC readiness: MFA, FIPS-validated cryptography, software baselines, backup restoration, logging, response, physical/media/personnel controls and other requirements remain outside assessed coverage. The [vendor assessment](../Vendor-Assessment/Simulated-Vendor-Assessment.md) contains hypothetical questions, not completed supplier assurance.

Positive RBAC behavior on 8445 is not proof of 8443 OIDC deployment. Active/enabled managed services do not prove test-app reboot persistence. NotConfigured Windows default actions require effective-policy verification. Broad NAT-side SSH does not by itself prove Internet reachability. CA placement and database type remain operator-confirmed pending sanitized corroboration.

## Acceptance and Next Review

The [v1.0 finalization review](Finalization-v1.0.md) checks the required package and lists missing evidence. Documentation is ready for portfolio review with explicit limitations; technical findings remain unclosed and publication approval is still required. No test, remediation or risk acceptance was created by finalizing these files.

The [detailed control matrix](../Control-Mapping/Control-Assessment-Matrix.md) separates SP 800-53 Rev. 5 references from SP 800-171 Rev. 2/CMMC identifiers, using evidence-limited local readiness statuses. No selected row establishes full Met coverage. The [traceability record](../Control-Mapping/Evidence-Traceability.md) preserves historical/current distinctions and credits REC-03 only for historical negative tests. The current owner-approved decision retains that screenshot as supporting evidence; it does not show a confirmed working password or authorize publication.

The [RMF lifecycle](../RMF/RMF-Lifecycle.md) documents all seven steps as a simulation. Its proposed categorization is hypothetical; its recommendation is to continue lab remediation and verification, not authorize production or real CUI. No actual authorizing official, risk acceptance or ATO exists.

Review the [control assessment](../Control-Mapping/NIST-CMMC-Control-Assessment.md), confirm real-world scope only if an actual engagement exists, approve organization-defined parameters, and assign owners. Reassess after approved changes using independently reviewable evidence. The framework distinction is documented against [official CMMC model requirements](https://www.govinfo.gov/link/cfr/32/170?link-type=pdf&year=mostrecent) and [NIST RMF](https://csrc.nist.gov/pubs/sp/800/37/r2/final); no authorization or certification is implied.
