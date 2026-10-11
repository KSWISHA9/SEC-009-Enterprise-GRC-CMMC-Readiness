# System Security Plan - Draft Lab Assessment

System: OmniVerse Defense Systems Engineering Workspace (fictional). Version: 1.0. Assessment baseline: 2026-10-10. Approval: not provided. All owner roles below are proposed. No real CUI is stored, processed or transmitted.

## Purpose and Boundary

### Configuration-Drift Addendum

[CMMC-CM-001](../Reports/CMMC-CM-001-Configuration-Drift-and-Recovery.md) records operator-reported simulated drift: AuditLogging Enabled changed to Disabled, then restored to Enabled. The final SHA-256 did not match the original trusted baseline. **Exact byte-level recovery verification remains OPEN, not PASS.** No source file/hash, script or corresponding capture is imported; semantic restoration is not byte-identical recovery or backup-restore evidence. This exercise does not close the eight existing risks or establish full configuration-management compliance.

### Controlled File-Permission Exercise

[CMMC-AC-001](../Reports/CMMC-AC-001-Controlled-Access-Control-Exercise.md) is a disposable simulated-data exercise on OV-DC01, not a new production asset or real CUI store. The operator reports OU SECX002-Lab and a continuously disabled SECX002-TestUser. Baseline E-17 shows 2,607 users (2,594 enabled, 13 disabled), and Administrator as the sole listed member of Domain Admins and Enterprise Admins. This pre-setup snapshot is not the current post-creation inventory or full privilege approval.

E-18/19 preserve the intentional Full Control grant and first removal with residual inherited Users RX. E-20/21 supersede that interim ACL: inheritance disabled (operator-confirmed), Users removed, SYSTEM/Administrators Full Control and Contractor-Readers Read, Synchronize; all displayed ACEs are Allow and not inherited. E-22 shows 0 unexpected Allow ACEs, 1 reader ACE and disabled account; PASS is operator-confirmed. E-23/24 now document positive/negative Windows Effective Access evaluations: SECX002-Authorized has evaluated Read data/attributes/permissions, not Write/Delete/Full Control; SECX002-Unauthorized has no displayed evaluated permissions. Membership/nonmembership and both accounts remaining disabled are operator-confirmed. E-21 group-empty output is historical. These are permission evaluations, not interactive login or actual read/denial attempts, full least privilege or a change to the eight risk statuses.

The simulated mission is to give engineering analysts role-limited access to dummy internal information while supporting workforce identity, DNS and security validation. The boundary includes OV-DC01, Ubuntu-Server, Kali, and the Windows VirtualBox host. The host is a security-relevant dependency because it controls VM storage, networking, execution and snapshots; it must not be ignored as out of scope.

NAT and the host-only adapter connect to host-controlled virtual networks. NAT permits outbound paths subject to configuration and may permit inbound forwarding if configured; actual forwarding was not exported. Host-only is not a physical isolation boundary. Physical host, storage, power, host security and Internet/update paths are supporting dependencies whose protections are unassessed.

Data classification: simulated internal engineering data only. A hypothetical future CUI categorization would require actual data types, contract requirements and an approved scope. No FIPS 199 category, formal RMF authorization, CUI enclave determination or actual defense contract is established.

## Architecture and Flows

```text
Windows VirtualBox host (hypervisor, VM disks, administrative access)
  |-- OV-DC01 10.10.10.10: AD DS / DNS
  |-- Ubuntu-Server 10.10.10.101:
  |     8443 managed HTTPS Basic application
  |     8444 Keycloak HTTPS identity provider
  |     8445 manually launched OIDC/RBAC test application
  |-- Kali 10.10.10.100: authorized validation client

Each VM: adapter 1 NAT; adapter 2 host-only
Kali --> Ubuntu 8443/8444/8445: source-specific UFW permits captured
Host/admin path --> Ubuntu 22 via NAT side: broad rule; forwarding unknown
Clients --> OV-DC01: AD/DNS dependency; exact effective port policy unassessed
```

OIDC conceptual flow: browser reaches test app, redirects to Keycloak, authenticates, returns an authorization code to the configured callback, and the confidential client exchanges it for tokens before enforcing roles. Operator-confirmed analyst allow/viewer deny was on test port 8445. Sanitized callback, token/session review and application implementation proof are missing. No AD-to-Keycloak federation, LDAP synchronization or shared credential store was confirmed; diagram proximity does not establish integration.

Trust boundaries include guest versus host, application versus IdP, approved client versus other sources, administrative management versus user access, and CA signing trust versus application runtime. App and IdP share an Ubuntu host, limiting separation. RBAC is local application authorization, not full enterprise Zero Trust or device assurance.

## Existing Safeguards and Evidence

| Safeguard | Evidence basis | Limits |
| --- | --- | --- |
| NAT/host-only VM adapters; allocated RAM/CPU | E-01 | Not complete isolation, hardware inventory or availability redundancy |
| Ubuntu 24.04.3 LTS; interfaces and UFW policy | E-02 | Runtime capture, not approved persistent config export |
| Application-source restrictions | E-02 | New-port Windows and IPv6 path denial tests missing |
| HTTPS and Keycloak services | Operator-confirmed; E-02 listeners/status lines | Unlabeled service lines; comprehensive TLS/service config not captured |
| Application/Keycloak active and enabled | Operator-confirmed | Does not imply OIDC test app is managed or reboot-persistent |
| Analyst/viewer OIDC RBAC | Operator-confirmed; SEC-008 contextual documentation | 8445 test only; 8443 remains Basic |
| Windows Firewall enabled for three profiles | E-03/04 | Default actions NotConfigured; effective actions unverified |
| AD password and lockout policy | E-06 before; E-07/08 after and validation | Length 14, complexity enabled, threshold 10, duration/window 30 minutes; max age 42 days. Configuration verified; enforcement pending |
| Displayed Domain Admins membership | E-03/04 | Administrator shown; nested groups, service accounts and effective privilege not assessed |

Evidence references resolve through [Evidence Index](../Evidence/INDEX.md). No secret material was imported.

## Proposed Responsibilities

The [Atlantic Defense Cloud Services assessment](../Vendor-Assessment/Atlantic-Defense-Cloud-Services-Assessment.md) evaluates a fictional future supplier only. No service/access/data scope is established, no external administrative connection is verified, and no vendor control is inherited. All five safeguards are Unverified; defer approval pending evidence. The existing four-asset boundary is unchanged.

| Role | Proposed responsibility |
| --- | --- |
| Fictional business sponsor / risk owner | Approve scope, recovery targets, resources and residual-risk decisions |
| GRC lead | Maintain SSP, control assessment, risks and evidence traceability |
| IAM engineer | OIDC promotion, Keycloak database, roles and session/token review |
| PKI administrator | Separate/protect CA signing function and validate trust lifecycle |
| AD administrator | DNS, password policy, attempt limiting and privilege review |
| Platform/security engineer | Hypervisor, host, UFW management boundary, service/backup operations |
| Assessment reviewer | Verify closure evidence without accepting planned actions as completed |

These are planning roles, not assigned employees. No segregation-of-duties implementation is established.

## Findings and Operational Plan

### Final Group Policy Refresh Validation

OV-DC01 successfully completed `gpupdate /force` for computer and user policies (invocation operator-confirmed; successful outputs observed). E-13 verifies AD length 14, lockout threshold 10, duration/window 30 minutes; Process Creation and Directory Service Changes Success; Credential Validation, Kerberos Authentication Service and Security Group Management Success and Failure. E-12 records event 4688 for `C:\Windows\System32\whoami.exe`, whose successful generation is operator-confirmed.

This establishes **configuration persistence through one Group Policy refresh**, not reboot persistence, full policy provenance, password/lockout enforcement or full compliance. The supplied VAL-02 Persistence name is mapped to the preserved project copy `VAL-02-Group-Policy-Refresh-Validation.png`; [final validation details](../Reports/Windows-Audit-Policy-Remediation.md) explain provenance and exact results. No risk is closed or residual score reduced by this update.

### Windows Audit Remediation and Remaining Assurance

R-008, Incomplete Windows Security Audit Coverage, is **Configuration remediated, validation pending**. Baseline E-09/10 shows Security log enabled with 104,488 records, max size 128 MiB, Logon Success and Failure and one listed 4625. REM-04 verifies Process Creation and Directory Service Changes changed from No Auditing to Success; Credential Validation, Kerberos Authentication Service and Security Group Management changed from Success to Success and Failure. [Audit report](../Reports/Windows-Audit-Policy-Remediation.md) preserves the evidence and limits.

VAL-01 shows one 4688 for whoami.exe; VAL-02 shows expected settings after one successful policy refresh. This narrows, but does not close, validation gaps. Remaining event-generation cases, relevant directory SACLs, approved GPO source/reboot/repeated-refresh persistence, retention/overwrite/archiving, protected centralized collection and correlation require validation. AUTO-01's 12 PASS checks are configuration spot-checks only. No complete audit program, CMMC compliance or AD lockout enforcement is established.

Operator reports the original audit policy backed up on OV-DC01 at `C:\SECX-002\Backups\Audit-Policy-Before.csv`; export command/success is visible, but file contents/hash/restoration were not inspected or imported. This is configuration preservation, not full system/data backup. Proposed AD/security-monitoring roles own P-008; responsibility and dates await approval. All eight findings remain unclosed.

R-001 through R-005 remain Open in the [risk register](../Risk-Assessment/Risk-Register.csv). R-006/R-007 are configuration remediated, enforcement testing pending. Proposed treatments and dates are in the [POA&M](../POAM/Plan-of-Action-and-Milestones.csv). DNS discrepancy is unresolved; CA signing key remains co-located per operator statement. OIDC promotion, database replacement and SSH policy changes remain planned. AD changes were performed by the operator and are documented in the [remediation report](../Reports/AD-Password-Policy-Remediation.md); the maintainer did not change the VMs.

REM-03 shows no fine-grained policy output for Administrator and corroborating domain values through `net accounts /domain`. Scope is that account/query only, not all users. Baseline export `C:\SECX-002\Backups\AD-Password-Policy-Before.xml` is reported by the operator and existence-checked in the OV-DC01 capture. It was not imported or restored. Configuration preservation is not an AD system-state backup.

Proposed monitoring: monthly risk/evidence review and review after material changes; review admin membership, failed logons, firewall denials, IdP events and certificate expiry. No central collection, retention policy, reviewer accountability or incident-response program was verified.

Proposed recovery: protect VM/app/IdP/AD backups outside the runtime host, document dependencies and conduct controlled restore tests. Historical stop/start does not prove backup recovery or BIA targets. Proposed change management requires approved work, rollback, sanitized evidence and post-change tests. No changes were performed by this assessment.

Phase 5 proposed recovery objectives are AD/DNS RTO 2 hours/RPO 1 hour, Keycloak RTO 2 hours/RPO 1 hour and contractor portal RTO 4 hours/RPO 2 hours. None has been demonstrated. The [BIA dependency matrix](../BIA/Business-Impact-Analysis.md) distinguishes confirmed shared hosting from assumed business-service relationships, including unverified AD federation. Host/network/trust recovery must fit within each service deadline; independent target values are not sequential extra allowances.

The [recovery validation plan](../POAM/Recovery-Validation-Plan.md) describes proposed evidence needed. It is not an approved backup architecture or scheduled VM test. The BIA's assumed residual ALE is a financial scenario input, not a residual security-risk rating or an authorization decision.

## Coverage Limits

The [selected six-field control matrix](../Control-Mapping/Control-Assessment-Matrix.md) and [evidence traceability](../Control-Mapping/Evidence-Traceability.md) now distinguish current configurations, historical 8080 tests and operator-confirmed OIDC details. Read-only SEC-008 references do not imply current-port recovery or full assessment-objective coverage. The [RMF lifecycle](../RMF/RMF-Lifecycle.md) proposes a hypothetical Moderate/Moderate/Moderate scenario only; the statement above that no formal category is established remains unchanged. Its authorization section recommends continued lab verification, not production approval or an actual ATO.

This is a selected-control SSP draft, not a complete description of all 110 Level 2 requirements. Physical/media/personnel security, training, incident response, vulnerability management, patching, endpoint protection, encryption at rest, MFA, centralized logs and external providers need assessment. Dependencies and policies remain missing, not presumed absent. A real SSP would require approved parameters, all applicable implementation narratives and independent review.
