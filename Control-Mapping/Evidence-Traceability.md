# Control Evidence Traceability

Review date: 2026-10-10. References below resolve to existing files; none was invented, copied from a VM or newly fabricated. SEC-008 was inspected read-only. Screenshots establish a captured state, not a continuous guarantee. Operator statements are labeled separately. Hash/provenance for the SEC-009 captures remains in the [evidence manifest](../Evidence/Evidence-Manifest.csv).

## SEC-009 Configuration Evidence

| Reference / existing file | Observed result and command | Assessment limit |
| --- | --- | --- |
| E-02: [CTRL-01-Ubuntu-Security-Baseline.png](../Evidence/Controls/CTRL-01-Ubuntu-Security-Baseline.png) | Ubuntu host-only 10.10.10.101; UFW active, medium logging, deny incoming/allow outgoing/routed disabled; source 10.10.10.100 permits 8443/8444/8445; NAT SSH Anywhere including IPv6; listeners visible | Runtime setting capture; unlabeled active/enabled lines do not prove OIDC service management. Does not prove TLS, current-port denial, reboot persistence or approved baseline |
| E-03: [CTRL-02-Active-Directory-Security-Baseline.png](../Evidence/Controls/CTRL-02-Active-Directory-Security-Baseline.png) | Historical AD baseline; firewall profiles enabled, default actions NotConfigured; displayed Domain Admins member Administrator | Effective firewall actions and nested/effective privilege are unverified; later REM evidence supersedes historic password settings |
| REM-01: [REM-01-AD-Password-Policy-Before.png](../Evidence/Controls/REM-01-AD-Password-Policy-Before.png) | `Get-ADDefaultDomainPasswordPolicy`: length 7, complexity True, threshold 0, duration/window 30 minutes, maximum age 42 days; `Export-Clixml` command and completion message | Baseline configuration and export operation shown; XML contents/hash/restoration not inspected |
| REM-02: [REM-02-AD-Password-Policy-After.png](../Evidence/Controls/REM-02-AD-Password-Policy-After.png) | `Set-ADDefaultDomainPasswordPolicy` followed by query: length 14, complexity True, threshold 10, duration/window 30 minutes, maximum age 42 days | Configuration change, not password/lockout enforcement testing |
| REM-03: [REM-03-AD-Policy-Validation.png](../Evidence/Controls/REM-03-AD-Policy-Validation.png) | PowerShell and `net accounts /domain` corroborate length 14, threshold 10 and 30-minute timers. `Get-ADUserResultantPasswordPolicy -Identity Administrator` has no displayed FGPP. `Test-Path` baseline XML returns True | File path is on OV-DC01, not this maintainer host. Existence is not backup integrity or restore. Resultant policy query is not all-user scope or Administrator lockout behavior |

Baseline export reference: `C:\SECX-002\Backups\AD-Password-Policy-Before.xml` on OV-DC01. No XML, secrets or VM files were imported. Commands above are observed records, not instructions executed by the maintainer.

## SEC-008 Read-Only Implementation Evidence

| Reference / existing file | Observed result | Assessment limit |
| --- | --- | --- |
| S-01: [SEG-05-Least-Privilege-Application-Access.png](https://github.com/KSWISHA9/SEC-008-Enterprise-Security-Architecture/blob/main/Evidence/Segmentation/SEG-05-Least-Privilege-Application-Access.png) | Kali shows 22 filtered, 8080 open and HTTP 200/application content | Historical 8080 path; source address not visible in this capture; not current HTTPS/OIDC proof |
| S-02: [SEG-07-Unauthorized-Client-Blocked.png](https://github.com/KSWISHA9/SEC-008-Enterprise-Security-Architecture/blob/main/Evidence/Segmentation/SEG-07-Unauthorized-Client-Blocked.png) | Windows source 10.10.10.1 to 10.10.10.101:8080: ping True, TCP False | Specific historical source/port denial, not universal or current-port exclusion |
| S-03: [SEG-11-Firewall-Blocked-Traffic-Logs.png](https://github.com/KSWISHA9/SEC-008-Enterprise-Security-Architecture/blob/main/Evidence/Segmentation/SEG-11-Firewall-Blocked-Traffic-Logs.png) | Kernel journal UFW blocks correlate source 10.10.10.1, destination 10.10.10.101, TCP 8080, interface and time | Packet logging does not identify an authenticated person or demonstrate all audit events/retention |
| S-04: [SEG-12-Security-Incident-Investigation.png](https://github.com/KSWISHA9/SEC-008-Enterprise-Security-Architecture/blob/main/Evidence/Segmentation/SEG-12-Security-Incident-Investigation.png) | UFW policy and matching denied traffic inspected manually | Lab investigation of test traffic, not evidence of real compromise or enterprise monitoring program |
| T-01: [TLS-02-Lab-CA-and-Server-Certificate-Validation.png](https://github.com/KSWISHA9/SEC-008-Enterprise-Security-Architecture/blob/main/Evidence/TLS/TLS-02-Lab-CA-and-Server-Certificate-Validation.png) | Server certificate validates OK against lab CA; issuer and IP SAN 10.10.10.101 visible | Does not prove key custody, revocation, approved algorithms or validated module |
| T-02: [TLS-03-Remote-HTTPS-Authentication-Challenge.png](https://github.com/KSWISHA9/SEC-008-Enterprise-Security-Architecture/blob/main/Evidence/TLS/TLS-03-Remote-HTTPS-Authentication-Challenge.png) | Kali `curl --cacert` to 8443 produces HTTP 401/Basic challenge and exit 0 | CA-verified HTTPS challenge, not valid-credential HTTP 200 or OIDC login |
| I-01: [IAM-11-Analyst-Dashboard-Authorized.png](https://github.com/KSWISHA9/SEC-008-Enterprise-Security-Architecture/blob/main/Evidence/IAM/IAM-11-Analyst-Dashboard-Authorized.png) | Authorized dashboard visible | Identity ov-analyst and port 8445 are operator-confirmed; this image alone lacks identity/port/status correlation |
| I-02: [IAM-12-Viewer-Identity-and-Realm-Roles.png](https://github.com/KSWISHA9/SEC-008-Enterprise-Security-Architecture/blob/main/Evidence/IAM/IAM-12-Viewer-Identity-and-Realm-Roles.png) | Signed-in ov-viewer and viewer realm role displayed | Does not show token validation implementation or complete identity lifecycle |
| I-03: [IAM-13-Analyst-Dashboard-Forbidden.png](https://github.com/KSWISHA9/SEC-008-Enterprise-Security-Architecture/blob/main/Evidence/IAM/IAM-13-Analyst-Dashboard-Forbidden.png) | Forbidden page visible | Viewer association and numeric HTTP 403 are operator-confirmed, not visible response-header evidence |
| C-01: [REC-01-Controlled-Application-Outage.png](https://github.com/KSWISHA9/SEC-008-Enterprise-Security-Architecture/blob/main/Evidence/Recovery/REC-01-Controlled-Application-Outage.png) | Historic `secx001-app.service` inactive; no 8080 listener; curl HTTP 000/exit 7 | HTTP 000 is curl's no-response value, not an HTTP response status. No production HTTPS/IdP recovery demonstrated |
| C-02: [REC-02-Service-Restored-Authentication-Enforced.png](https://github.com/KSWISHA9/SEC-008-Enterprise-Security-Architecture/blob/main/Evidence/Recovery/REC-02-Service-Restored-Authentication-Enforced.png) | Service active; 10.10.10.101:8080 listening; unauthenticated HTTP 401 | Restart and challenge only; no backup restoration, valid login, reboot persistence or elapsed recovery measurement |
| C-03: REC-03-Remote-Post-Recovery-Validation.png, existing SEC-008 Recovery folder; supporting historical evidence; publication approval pending | Kali no-credential 401, invalid-credential 401, ping 2/2 successful | Rejected test string visible; owner approved retaining as supporting evidence. Valid credentials were NOT retested; exact-release approval pending |

Screenshots in this review other than C-03 did not visibly expose a password, token, client/session secret or private-key contents. This is a visual review, not a guarantee of absence of metadata or secrets elsewhere in either repository. C-03 remains unchanged and is retained as supporting negative-test evidence under the [current owner-approved decision](https://github.com/KSWISHA9/SEC-008-Enterprise-Security-Architecture/blob/main/Reports/Publication-Review.md); no confirmed working credential is visible. Publication approval remains pending.

## Windows Audit Evidence - R-008

| Reference / existing file | Observed result | Limit |
| --- | --- | --- |
| E-09: [CTRL-03-Windows-Audit-Logging-Baseline.png](../Evidence/Controls/CTRL-03-Windows-Audit-Logging-Baseline.png) | Security log enabled; 104,488 records; max 128 MiB; 4625 listing; baseline lower categories | Full event details and retention duration not shown |
| E-10: [CTRL-03-Windows-Audit-Policy-Baseline-Supplemental.png](../Evidence/Controls/CTRL-03-Windows-Audit-Policy-Baseline-Supplemental.png) | Logon Success and Failure; Process Creation No Auditing | Complementary baseline, not exact duplicate or proof all missing categories are required |
| E-11: [REM-04-Windows-Audit-Policy-Hardening.png](../Evidence/Controls/REM-04-Windows-Audit-Policy-Hardening.png) | Five settings queried after change; audit-policy export operation | File contents/hash/restore, SACLs and complete event coverage not verified |
| E-12: [VAL-01-Process-Creation-Audit-Event.png](../Evidence/Controls/VAL-01-Process-Creation-Audit-Event.png) | Event 4688 with whoami.exe path | One process event, not all audit objectives or initiating-action/full-record proof |
| E-13: [VAL-02-Group-Policy-Refresh-Validation.png](../Evidence/Controls/VAL-02-Group-Policy-Refresh-Validation.png) | One successful policy refresh; desired settings displayed | Not authoritative GPO, repeated refresh or reboot persistence proof |
| E-14: [AUTO-01-Configuration-Spot-Checks.png](../Evidence/Controls/AUTO-01-Configuration-Spot-Checks.png) | Script shows 12 configuration PASS checks | Not compliance; full script and generated CSV unavailable |

See [audit report](../Reports/Windows-Audit-Policy-Remediation.md) for exact transitions, pending criteria, private VM backup path and clock uncertainty. All six source originals remain unchanged and copy hashes match. No visible secrets observed; public metadata approval remains pending.

## Controlled Access-Control Traceability

### Effective Access Follow-Up

| Reference | Screenshot | Observed actual result | Provenance / limits |
| --- | --- | --- | --- |
| E-23 | [CMMC-AC-007-Authorized-Effective-Access.png](../Evidence/CMMC/CMMC-AC-007-Authorized-Effective-Access.png) | SECX002-Authorized evaluated with read data/attributes/permissions allowed; write, delete and Full Control not allowed | Readers-group membership and disabled state operator-confirmed; evaluation only, not file read |
| E-24 | [CMMC-AC-008-Unauthorized-Effective-Access.png](../Evidence/CMMC/CMMC-AC-008-Unauthorized-Effective-Access.png) | SECX002-Unauthorized shows no evaluated permissions granted | Nonmembership and disabled state operator-confirmed; file header cropped, same-file association confirmed by operator; not an actual denial attempt |

The group-empty output in E-21 is historical, superseded by reported addition of SECX002-Authorized. Both test accounts remained disabled; current membership/state command evidence is not supplied. Existing project images are indexed in place with hashes matching the pre-edit snapshot, not represented as copies from Pictures. No visible secrets observed; account/path metadata approval remains pending. AC.L2-3.1.1/3.1.5 stay Partially Demonstrated; the earlier ACL PASS is not a new authentication/access attempt or full compliance result.

Final RBAC follow-up supersedes the interim Users RX residual below, without removing historical evidence:

| Reference | Screenshot | Observed result | Limits |
| --- | --- | --- | --- |
| E-20 | [CMMC-AC-004-RBAC-Restricted-ACL.png](../Evidence/Controls/CMMC-AC-004-RBAC-Restricted-ACL.png) | Global Security group; reader R, SYSTEM/Administrators F, Users absent | Inheritance-disable operation operator-confirmed; no actual access test |
| E-21 | [CMMC-AC-005-RBAC-Membership-And-ACL-Validation.png](../Evidence/Controls/CMMC-AC-005-RBAC-Membership-And-ACL-Validation.png) | Enabled False; group query empty; final three Allow ACEs, no inherited ACEs, reader Read/Synchronize | Historical empty-group snapshot, later membership operator-confirmed; heading "negative test" is not an actual denial attempt |
| E-22 | [CMMC-AC-006-Automated-Access-Policy-PASS.png](../Evidence/Controls/CMMC-AC-006-Automated-Access-Policy-PASS.png) | 0 unexpected Allow ACEs, 1 reader ACE, Enabled False and matching PASS branch | Printed PASS line outside frame/operator-confirmed; checks do not test effective access, exact rights equality or inheritance protection |

No authorized-user read or unauthorized-user denial test was performed. All eight CMMC-AC captures are reviewed; source originals retained, matching hashes indexed. Selected CMMC mappings remain partial evidence.

| Reference | Screenshot | Observed result | Limits |
| --- | --- | --- | --- |
| E-17 | [CMMC-AC-001-Privileged-Access-Baseline.png](../Evidence/Controls/CMMC-AC-001-Privileged-Access-Baseline.png) | 2,607 users, 2,594 enabled, 13 disabled; two selected privileged groups each list Administrator | Snapshot only; not all privileged access or approved authorization |
| E-18 | [CMMC-AC-002-Excessive-Permissions-Detected.png](../Evidence/Controls/CMMC-AC-002-Excessive-Permissions-Detected.png) | Disposable training file created; explicit test-user (F), inherited administrative (F) and Users (RX) | Disabled account throughout is operator-confirmed, not visibly validated |
| E-19 | [CMMC-AC-003-Least-Privilege-Remediation.png](../Evidence/Controls/CMMC-AC-003-Least-Privilege-Remediation.png) | /remove:g succeeds; explicit test-user entry absent; inherited SYSTEM/Administrators (F) and Users (RX) retained | Effective access and intended readership remain untested; not approved-users-only proof |

See [finding/remediation and framework mapping](../Reports/CMMC-AC-001-Controlled-Access-Control-Exercise.md). Account/OU setup and no-exploitation statement are operator-confirmed. Originals preserved; three source/copy hashes match; no visible secrets observed. E-20/21/22 above now provide visually reviewed final ACL and counters; historical residuals below are not current-file findings.

## Automation Artifact Traceability

| Reference | Artifact / exact location | Evidence basis and availability | Limits |
| --- | --- | --- | --- |
| E-16 | [AUTO-02-Standalone-Compliance-Validation.png](../Evidence/Automation/AUTO-02-Standalone-Compliance-Validation.png) | Host screenshot observed: standalone invocation, 12 PASS/0 REVIEW and guest report path | Selected configuration baseline only; not comprehensive compliance or enforcement validation |
| VM-AUTO-01 | `C:\SECX-002\Scripts\Invoke-SECX002Compliance.ps1` on OV-DC01 | Operator-confirmed saved script; invocation visible; **pending host import** | Source/hash/read-only behavior not independently reviewed; no host source file claimed |
| VM-AUTO-02 | `C:\SECX-002\Reports\SECX-002-Compliance-20261010-192143.csv` on OV-DC01 | Operator-confirmed successful CSV; path visible; **pending host import** | Actual CSV rows/hash not inspected; `.csv.png` screenshot is not the report data |

The five original REVIEW classifications and parser correction are operator-reported history, not five confirmed control failures. Current standalone output is visually evidenced. [Results and import instructions](../Reports/Automation-Validation-and-Import.md) explain 3 AD + 3 firewall + 5 audit + 1 log checks and remaining source/CSV review. No test of effective firewall actions, AD enforcement, full event/SACL/retention coverage, reboot, recovery or all framework objectives is inferred. E-14/AUTO-01 remains earlier spot-check evidence, not this script's source.

## Assessment Documents

### Configuration Drift - No Host Artifact Yet

CMMC-CM-001 is [documented from the operator update](../Reports/CMMC-CM-001-Configuration-Drift-and-Recovery.md), not from a fabricated evidence filename. Reported AuditLogging Enabled-to-Disabled drift was detected; Enabled restored, final hash different from original baseline. Exact byte-level recovery is OPEN. Baseline/restored bytes and SHA-256 values, validator, output and screenshots remain unsupplied. No manifest screenshot row or recovery PASS is created for this exercise.

Final confirmation: E-13 corresponds to supplied `VAL-02-Group-Policy-Persistence.png` and existing project `VAL-02-Group-Policy-Refresh-Validation.png`. Computer/user refresh success and all expected AD/audit values are visually observed; `gpupdate /force` invocation is operator-confirmed. This proves configuration persistence through one refresh, not reboot/repeated-refresh assurance or full compliance. E-12 records 4688 for `C:\Windows\System32\whoami.exe`; its generation is operator-confirmed. Hashes and original filenames are unchanged in the manifest; no duplicate was created. See [exact results](../Reports/Windows-Audit-Policy-Remediation.md).

| Reference | Existing artifact / provenance | Limit |
| --- | --- | --- |
| D-01 | [Risk Register](../Risk-Assessment/Risk-Register.csv) and [Methodology](../Risk-Assessment/Methodology.md) | Eight preliminary risk judgments; original scores, proposed owners/dates, no residual acceptance |
| D-02 | [BIA](../BIA/Business-Impact-Analysis.md) | Proposed recovery targets and hypothetical SLE/ALE calculations; analysis evidence only, no measured recovery or real financial data |
| D-03 | [Recovery Validation Plan](../POAM/Recovery-Validation-Plan.md) | Proposed tests, not approved/executed restoration evidence |
| D-04 | [AD Remediation Report](../Reports/AD-Password-Policy-Remediation.md) | Describes observed configuration and remaining enforcement tests; no closure claim |
| D-05 | [POA&M](../POAM/Plan-of-Action-and-Milestones.csv) | Proposed planning actions; five Open, two AD configuration remediated/enforcement pending, one Windows audit configuration remediated/validation pending |
| D-06 | [SSP](../SSP/System-Security-Plan.md) | Draft selected-control system description, not full 110-requirement implementation record |

Operator-confirmed details not fully demonstrated by these images include OIDC authorization-code/confidential-client setup, token validation implementation, managed app/Keycloak service identities, CA signing-key co-location, development-file database and incomplete cutover. Preserve these as reported facts pending sanitized configuration/source corroboration. DNS remains an unresolved domain-root response discrepancy, not an established complete outage.

## Missing Evidence and Publication Gate

- Approved access/flow/configuration baselines; current-port unauthorized-client and IPv6/NAT/egress tests.
- Sanitized OIDC route, identity, role and response-status correlation; negative token/session tests; managed-port cutover and reboot/recovery evidence.
- AD representative-account password rejection, attempt limiting, recovery and auditing evidence; reviewed baseline export integrity/rollback.
- CA key separation/custody, certificate lifecycle, full TLS flow coverage and applicable cryptographic module assurance.
- Repeatable audit review, retention, protection and wider AD/IdP/application event coverage.
- Protected backup restoration and timed end-to-end tests against proposed BIA objectives; formal owner approval and risk acceptance.
- Safe replacement/redaction of C-03 before any release that includes SEC-008 evidence.

Sibling links are valid in the current OmniVerse workspace but not necessarily in an independently published SEC-009 repository. Before approved publication, choose reviewed immutable repository links or an approved sanitized evidence bundle. Apply the current supporting/archive dispositions and do not assume this local review is publication approval.
