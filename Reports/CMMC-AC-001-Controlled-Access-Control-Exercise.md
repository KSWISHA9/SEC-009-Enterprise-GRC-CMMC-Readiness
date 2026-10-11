# CMMC-AC-001 - Controlled Access-Control Exercise

Assessment date: 2026-10-10. Environment: OV-DC01, Windows Server 2022, corp.omniverse.com (operator-confirmed environment). Fictional defense-contractor scenario; disposable training data only, no real CUI. This is configuration validation, not certification or a full compliance assessment.

## Finding and Remediation Record

Record: CMMC-AC-001-F01. **Lab ACL remediated and validated; positive/negative Windows Effective Access evaluations completed. Actual login/file-read tests remain unperformed.** This controlled exercise is separate from the existing eight assessed risks; it does not close R-001 through R-008 or create an unapproved ninth scored risk.

The operator created OU SECX002-Lab and account SECX002-TestUser, and reports that the account remained disabled throughout. E-21/E-22 now show Enabled False at final validation; continuously disabled state and OU creation remain operator-confirmed. No successful unauthorized access, exploitation, data loss or confirmed cyberattack was demonstrated.

The disposable VM file was `C:\SECX-002\CMMC-AC-001\Contractor-Test-Data.txt`. E-18 shows creation with the training-only string and intentional grant to OMNIVERSE\SECX002-TestUser. The file itself was not imported into the host project.

| Stage | Expected result | Observed result / evidence | Limit |
| --- | --- | --- | --- |
| Inventory and privileged groups | Record current population and selected memberships | E-17: 2,607 users = 2,594 enabled + 13 disabled; Domain Admins and Enterprise Admins each list Administrator and count 1 | Baseline snapshot before test setup, not a current post-creation census, authorization approval, all privileged groups or complete effective privilege review |
| Controlled excessive grant | Disposable file has an explicit test-account Full Control entry | E-18: `icacls` lists OMNIVERSE\SECX002-TestUser:(F); processing succeeds | Disabled-account state is operator-confirmed; ACL inspection is not execution of access under that identity |
| Remove explicit grant | Test-account grant absent from resulting ACL | E-19 shows `icacls /remove:g`, successful processing, and subsequent ACL without that explicit entry | Narrow grant removal, not proof of no effective access through other groups or deny/allow interactions |
| Interim administrative entries | SYSTEM and Administrators retain inherited Full Control | E-19: NT AUTHORITY\SYSTEM:(I)(F), BUILTIN\Administrators:(I)(F) | No broader administrator entitlement approval or access test |
| Historical residual inherited access | Assess inherited Users rights against intended policy | E-18 and E-19 both show BUILTIN\Users:(I)(RX) | Historical ACL superseded by E-20/21; actual user access testing still pending |

The request describes `icacls /remove`; the captured command is specifically `/remove:g`, removing grants for the named identity. Documentation preserves the observed command. No commands were executed on OV-DC01 by the repository maintainer.

## Historical Residual Finding and Final Remediation

Full Control exceeds the intended training scenario's least-privilege grant and could allow inappropriate file changes if effective access were possible. The disabled account and absence of an access test limit conclusions: no actual misuse or interactive file access is established. Later E-23/E-24 demonstrate evaluated permissions only.

Historical observation CMMC-AC-001-OBS01: E-18/E-19 retained inherited BUILTIN\Users RX after the first grant-removal step. **Superseded for this disposable file by E-20/E-21:** Users is absent and all three displayed final Allow ACEs have IsInherited False. Inheritance was disabled (operator-confirmed; protection flag itself not displayed), and the global security group SECX002-Contractor-Readers was granted Read. This is configuration remediation, not proof of effective access or enterprise-wide least privilege.

Remaining steps: approve real organizational readership and membership governance if extending beyond the lab; enroll a dedicated authorized identity through an approved test process and perform a read test, then perform a separate unauthorized-user denial test. Review effective permissions, group changes and persistence. E-21's group-empty snapshot is historical; the operator now confirms SECX002-Authorized membership and SECX002-Unauthorized nonmembership. Both remain disabled; no usable authenticated end-user access path was tested. Do not enable SECX002-TestUser or change VM permissions as part of documentation work. No test account or file was deleted here.

## Final RBAC Configuration and Automated Checks

The operator completed group-based NTFS remediation on the same disposable file. E-20 shows SECX002-Contractor-Readers as a Global Security group and icacls output containing only that group (R), SYSTEM (F) and Administrators (F), without inherited markers. E-21 shows these Allow ACEs:

| Identity | Final rights | IsInherited |
| --- | --- | --- |
| NT AUTHORITY\SYSTEM | FullControl | False |
| BUILTIN\Administrators | FullControl | False |
| OMNIVERSE\SECX002-Contractor-Readers | Read, Synchronize | False |

E-21 shows SECX002-TestUser Enabled False and MemberOf {}; the authorized group-members query displays no entries. At that earlier stage the operator confirmed an empty group; subsequent SECX002-Authorized membership is operator-confirmed for E-23. The capture's heading "RBAC NEGATIVE TEST" labels configuration queries, **not an actual denial test under an unauthorized identity**.

E-22 visibly shows automated counters: Unexpected Allow ACEs 0, Authorized Reader ACEs 1, Test Account Enabled False. The displayed code selects a PASS branch for those values. The final printed PASS line is outside the screenshot; **PASS - configured ACL matches the lab authorization policy is operator-confirmed**, with the counters and matching branch visually corroborated.

The visible validator rejects Allow ACE identities outside its three-identity list and requires one reader ACE containing the Read rights bitmask and a disabled test account. It does not independently assert exact rights equality, inheritance protection, populated group membership, or effective authorized/unauthorized access. E-21 separately documents exact displayed rights and no inherited ACEs. PASS is a narrow lab configuration result, not comprehensive ACL-validator coverage or CMMC compliance.

No actual authorized-user file read or unauthorized-user denial test was performed. Current role membership is operator-confirmed; Effective Access evaluations below do not demonstrate interactive end-user access. Retain Partially Demonstrated framework dispositions and pending enforcement tests.

### Final Evidence

- E-20: [CMMC-AC-004-RBAC-Restricted-ACL.png](../Evidence/Controls/CMMC-AC-004-RBAC-Restricted-ACL.png).
- E-21: [CMMC-AC-005-RBAC-Membership-And-ACL-Validation.png](../Evidence/Controls/CMMC-AC-005-RBAC-Membership-And-ACL-Validation.png).
- E-22: [CMMC-AC-006-Automated-Access-Policy-PASS.png](../Evidence/Controls/CMMC-AC-006-Automated-Access-Policy-PASS.png).

## Windows Effective Access Authorization Evaluation

The operator completed two Windows Effective Access evaluations on OV-DC01 for the disposable training file. Both SECX002-Authorized and SECX002-Unauthorized remained disabled throughout (operator-confirmed). SECX002-Authorized is now a member of SECX002-Contractor-Readers; SECX002-Unauthorized is not (operator-confirmed; direct membership queries are not present in these two images). This supersedes the earlier empty-group snapshot in E-21, which remains as historical evidence.

| Evaluation | Expected result | Screenshot-observed actual result | Limits |
| --- | --- | --- | --- |
| Positive, SECX002-Authorized, E-23 | Reader permissions without modification or ownership rights | Read data, Read attributes, Read extended attributes and Read permissions allowed; Write data, Delete and Full Control not allowed. Other displayed modification/ownership permissions also not allowed | Evaluated Windows permissions, not successful login, token/session activation or a file read. Membership/disabled-state assertions are operator-confirmed |
| Negative, SECX002-Unauthorized, E-24 | No evaluated file permissions for the nonmember | Every displayed permission has a red not-allowed indicator; no evaluated permission granted | Not an actual access-denied read attempt or proof across other files/interfaces. Top file-path header is outside this capture; association with the same file is operator-confirmed |

- E-23: [CMMC-AC-007-Authorized-Effective-Access.png](../Evidence/CMMC/CMMC-AC-007-Authorized-Effective-Access.png).
- E-24: [CMMC-AC-008-Unauthorized-Effective-Access.png](../Evidence/CMMC/CMMC-AC-008-Unauthorized-Effective-Access.png).

These are positive and negative **authorization evaluations**, not interactive login or file-read tests. A disabled identity can be evaluated without proving it can authenticate. No accounts were enabled and no VM operations were performed by the repository maintainer. Actual read/denial behavior with approved enabled identities, persistence, membership lifecycle and complete system-wide control coverage remain untested.

The earlier automated ACL result remains PASS (operator-confirmed, with 0 unexpected Allow ACEs, 1 reader ACE and the original test account disabled visually corroborated in E-22). No rerun of that automation is evidenced by E-23/E-24. Do not interpret a prior configuration PASS as a test of these accounts' interactive access.

Both images already existed in Evidence/CMMC and were indexed in place, not renamed or duplicated. SHA-256 hashes match the pre-edit review snapshot. External source originals were not located; no external-copy provenance is claimed. No visible credentials, private keys or tokens observed; identity, domain and local-path metadata approval remains pending.

## Selected Framework Assessment

Identifiers verified against [NIST SP 800-171 Rev. 2](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-171r2.pdf) and the [DoD CMMC Level 2 Assessment Guide](https://dodcio.defense.gov/Portals/0/Documents/CMMC/AssessmentGuideL2v2.pdf). Rev. 2 requirement identifiers and CMMC Level 2 practice identifiers are separate from SP 800-53 Rev. 5 control identifiers.

| Framework / identifier | Locally scoped review objective | Evidence and safeguard | Local readiness status | Gap |
| --- | --- | --- | --- | --- |
| SP 800-171 Rev. 2 3.1.1 / AC.L2-3.1.1 | Review identification of authorized identities and restrictions on access | E-17 inventory; E-18/19 historical ACL; E-20/21/22 restricted ACL; E-23/24 evaluated permissions | Partially Demonstrated | E-23/24 provide positive/negative evaluated permissions; membership/both disabled states operator-confirmed; full user/process/device scope and actual login/read/denial tests absent |
| SP 800-171 Rev. 2 3.1.2 / AC.L2-3.1.2 | Review permissions for intended user actions | E-18/19 grant removal; E-20/21 group Read grant; E-23/24 positive/negative Effective Access | Partially Demonstrated | Lab ACL and evaluated permissions demonstrated; actual user read/denial tests absent; existing OIDC tests distinct |
| SP 800-171 Rev. 2 3.1.5 / AC.L2-3.1.5 | Review least-privilege decisions, including privileged accounts and security functions | E-17 selected privileged groups; E-20/21 least-privilege file ACL; E-22 configuration counters; E-23/24 evaluated permissions | Partially Demonstrated | Single-member groups do not prove approved privileged access; security-function inventory/authorization and wider least-privilege review absent |
| SP 800-53 Rev. 5 AC-3 | Examine access enforcement against approved permissions | E-18/19 historical change; E-20/21/22 final lab ACL configuration | Partially Demonstrated | Lab ACL policy checked; organizational authorization approval and actual positive/negative enforcement tests absent |

These are local learning/readiness dispositions, not official CMMC MET/NOT MET/NOT APPLICABLE findings. The file exercise illustrates least-privilege practice; it does not test every 3.1.5 privileged-account/security-function objective. No score, certification, complete access-control assessment or satisfaction of all 110 requirements is asserted.

## Evidence and Publication Review

- E-17: [CMMC-AC-001-Privileged-Access-Baseline.png](../Evidence/Controls/CMMC-AC-001-Privileged-Access-Baseline.png).
- E-18: [CMMC-AC-002-Excessive-Permissions-Detected.png](../Evidence/Controls/CMMC-AC-002-Excessive-Permissions-Detected.png).
- E-19: [CMMC-AC-003-Least-Privilege-Remediation.png](../Evidence/Controls/CMMC-AC-003-Least-Privilege-Remediation.png).

Six double-extension originals remain unchanged in Pictures/Screenshots. Copies use a single .png extension and matching SHA-256 hashes in the manifest. No visible password, token, secret or private-key contents observed; usernames and local paths remain visible and require publication approval. Guest/host clocks are not reconciled.

CMMC-AC-004/005/006 are now visually reviewed and incorporated as E-20/21/22. Earlier captures remain as history. No visible secrets observed in the three added images; local metadata approval pending. No VM change, commit, push or publication was performed.
