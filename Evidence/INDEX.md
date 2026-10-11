# Evidence Index

For the selected NIST/CMMC review, see [Control Evidence Traceability](../Control-Mapping/Evidence-Traceability.md) and the [Control Assessment Matrix](../Control-Mapping/Control-Assessment-Matrix.md). These reference SEC-008 read-only and distinguish historical HTTP recovery from later HTTPS/OIDC. No new screenshots were created or copied for that review. REC-03 in SEC-008 remains supporting historical evidence under the [current owner-approved decision](https://github.com/KSWISHA9/SEC-008-Enterprise-Security-Architecture/blob/main/Reports/Publication-Review.md). No confirmed working password is visible; publication approval remains pending.

Capture selection window: 2026-10-10 21:29:22 through 21:59:22 America/New_York (EDT), equivalent to 2026-10-11 01:29:22 through 01:59:22 UTC. Files were selected by creation or modification timestamp, not presumed capture time alone. Five source files were found in Pictures/Screenshots; their visible content was inspected individually before copying. [Manifest](Evidence-Manifest.csv) records original/copy hashes and timestamps.

No exact SHA-256 duplicates occurred among the five. E-03 and E-04 show substantively repeated results but have different pixels; both are preserved. Double/incorrect extensions were normalized only on copies. Nothing was renamed or deleted at the source.

Remediation intake window: 2026-10-10 21:56:15 through 22:06:15 America/New_York (EDT), or 2026-10-11 01:56:15 through 02:06:15 UTC. Pictures, Downloads, Desktop, OneDrive and the project tree were searched. Three new source captures were found; five recently created project copies matched earlier hashes and were not reimported. The three REM labels match their actual contents. Eight unique images were indexed at that stage; originals remain unchanged.

| ID | Screenshot | What it demonstrates | Expected assessment evidence | Actual result and limits |
| --- | --- | --- | --- | --- |
| E-01 | [VM inventory](Inventory/INV-01-VirtualBox-Asset-Inventory.png) | Running VM list and allocation/adapter output | Three VMs, resource allocation and interface types | DC 8192 MiB/4 CPUs, Ubuntu and Kali 4096 MiB/2 CPUs; each NAT plus host-only. Guest type is not full guest-version proof; host specs missing |
| E-02 | [Ubuntu baseline](Controls/CTRL-01-Ubuntu-Security-Baseline.png) | OS, IPs, UFW policy, rules and listeners | Runtime policy and service/network evidence | Ubuntu 24.04.3 LTS; 10.10.10.101 and NAT 10.0.2.15; active/default deny inbound, allowed outgoing/routed disabled; Kali-source 8443/8444/8445 rules; SSH Anywhere on NAT including IPv6. Unlabeled active/enabled lines do not independently identify units or prove OIDC persistence |
| E-03 | [AD baseline](Controls/CTRL-02-Active-Directory-Security-Baseline.png) | DC identity, firewall flags and AD policy | Current directory/security settings | OV-DC01 10.10.10.10 Server 2022 Standard Evaluation; all three firewall profiles True/default actions NotConfigured; length 7, complexity True, threshold 0, max age 42 days; Administrator displayed in Domain Admins |
| E-04 | [AD supplemental capture](Controls/CTRL-03-Active-Directory-Baseline-Supplemental.png) | Same AD settings in a different capture | Corroboration without overwriting different pixels | Same settings as E-03; redundant content, not independent test or exact duplicate |
| E-05 | [Domain summary](Controls/CTRL-04-AD-Domain-Summary.png) | Domain output amid mostly empty sections | Domain identity/function-level evidence | corp.omniverse.com, Windows2016Domain and OV-DC01 PDC shown. Firewall/password/member section headings are empty, so this frame does not demonstrate those controls |
| E-06 | [REM-01 before](Controls/REM-01-AD-Password-Policy-Before.png) | Default-domain configuration and baseline-export command/message | Pre-change settings and preservation step | Length 7, complexity True, threshold 0, duration/window 30 minutes, max age 42 days; export message visible. XML contents/restoration not verified |
| E-07 | [REM-02 after](Controls/REM-02-AD-Password-Policy-After.png) | Set command followed by configuration query | New configured values | Length 14, complexity True, threshold 10, duration/window 30 minutes, max age 42 days. No short-password rejection or failed-logon enforcement shown |
| E-08 | [REM-03 validation](Controls/REM-03-AD-Policy-Validation.png) | Default policy, Administrator resultant query, net accounts and file existence | Cross-command settings and preservation check | PowerShell/net accounts agree; no displayed Administrator FGPP; Test-Path True on OV-DC01. No all-user policy, enforcement or restore proof |

## Windows Audit Evidence Update

Six further source captures were found in Pictures/Screenshots during a search of accessible Pictures, Downloads, Desktop, Documents, OneDrive and project folders. Sources have file modification times 2026-10-10 22:07:54 through 22:18:03 EDT. Fourteen unique project images were indexed at that intake stage. No exact hash duplicates occurred in this intake; baseline frames are complementary. Filename fixes were applied only to copies, with original source names and matching hashes preserved.

| ID | Screenshot | Expected evidence | Actual result and limit |
| --- | --- | --- | --- |
| E-09 | [Windows audit baseline](Controls/CTRL-03-Windows-Audit-Logging-Baseline.png) | Existing log state and audit gaps | Enabled Security, 104,488 records, maximum 134,217,728 bytes; 4625 listed; selected baseline categories incomplete. Not a retention guarantee |
| E-10 | [Audit baseline supplemental](Controls/CTRL-03-Windows-Audit-Policy-Baseline-Supplemental.png) | Remaining baseline settings | Logon Success and Failure; Process Creation No Auditing; different pixels from E-09 |
| E-11 | [Audit hardening](Controls/REM-04-Windows-Audit-Policy-Hardening.png) | Five remediated settings and backup operation | Process Creation/Directory Service Changes Success; Credential Validation/Kerberos Authentication Service/Security Group Management Success and Failure; export operation shown, file integrity/restore unverified |
| E-12 | [Process event](Controls/VAL-01-Process-Creation-Audit-Event.png) | Narrow event-generation evidence | 4688 for whoami.exe observed; not full event coverage or command-line capture |
| E-13 | [Policy refresh](Controls/VAL-02-Group-Policy-Refresh-Validation.png) | Configuration after policy refresh | One successful refresh and expected settings; GPO provenance/reboot/repeated refresh validation pending |
| E-14 | [Configuration spot-checks](Controls/AUTO-01-Configuration-Spot-Checks.png) | Narrow automated configuration review | 12 displayed PASS checks; no full script/CSV supplied and no formal compliance outcome |

No visible secrets were observed in these six captures. Guest/host times were not reconciled. See [R-008 report](../Reports/Windows-Audit-Policy-Remediation.md) for exact before/after settings, scope and missing evidence.

## SOC-001 Investigation Evidence

E-15: [SOC-001 ADSync authentication timeline](Monitoring/SOC-001-ADSync-Authentication-Timeline.png). Expected: authentication correlation and service identity/state. Actual: 4624/4625 listed at 2026-10-10 12:06:41 PM, ADSync Running/Auto with OMNIVERSE\ADSyncMSA7efbc$. Full event fields and AD properties are operator-confirmed; root cause, event order, recurrence and sync health remain unconfirmed. See [investigation report](../Reports/SOC-001-Entra-Connect-Service-Account-Authentication-Investigation.md). Double-extension original retained; matching hashes recorded in the manifest. No visible secret value observed; account/host metadata approval pending. Evidence count at the SOC-001 intake was fifteen; AUTO-02 below increases the current total to sixteen.

## Controlled Access-Control Evidence

E-23/E-24: [CMMC Effective Access index](CMMC/INDEX.md) records read-only evaluated permissions for SECX002-Authorized and no granted displayed permissions for SECX002-Unauthorized. Membership/nonmembership and both disabled states are operator-confirmed. These are evaluations, not actual login or file-read attempts. Both images already existed in the project and remain unchanged; pre-edit snapshot hashes match. No visible secrets observed; metadata approval pending.

Final follow-up E-20/21/22 adds [restricted group ACL, membership/account queries and automated counters](../Reports/CMMC-AC-001-Controlled-Access-Control-Exercise.md). Users RX from E-18/19 is historical: final three Allow ACEs are SYSTEM/Administrators FullControl and Contractor-Readers Read/Synchronize, all not inherited. Historical group-empty output superseded by reported SECX002-Authorized membership; current E-23/24 evaluated permissions are not actual login/read/denial attempts. Counters 0/1/False are visible; printed PASS is operator-confirmed outside the frame. Six configuration captures preserved; two later Effective Access captures bring the project total to twenty-four indexed images.

Historical E-17 through E-19 document privileged-group/user baseline, intentional Full Control grant and initial explicit grant removal. [Exercise report](../Reports/CMMC-AC-001-Controlled-Access-Control-Exercise.md) provides screenshot links, expected/actual results, findings and missing tests. Those interim captures retain inherited administrative rights and Users RX; final E-20/21 supersede that ACL. Actual user access validation remains pending. Account continuously disabled is operator-confirmed. Three original .png.png captures were copied unchanged with single extensions; no secrets visibly observed. Count at that first intake: nineteen; final follow-up brings the total to twenty-two.

## Standalone Automation Evidence

E-16: [AUTO-02 standalone validation](Automation/AUTO-02-Standalone-Compliance-Validation.png). Expected: saved-script execution and selected baseline output. Actual: invocation of `C:\SECX-002\Scripts\Invoke-SECX002Compliance.ps1`, 12 PASS/0 REVIEW across 3 AD settings, 3 firewall flags, 5 audit settings and Security log enabled state; guest CSV path displayed. Script and actual CSV remain VM-only and are not imported. The source `.csv.png` file is a screenshot, not report data. Source/copy hashes match; original retained; no visible secrets observed. See [results/import instructions](../Reports/Automation-Validation-and-Import.md). Capture count at the automation intake was sixteen; initial CMMC-AC evidence raised it to nineteen, followed by twenty-two after final RBAC captures.

## Visual Review Limits

No visible credential values, tokens, client/session secrets or private-key contents were observed. Prompts/variable names are not secret values. Metadata such as internal domain/IPs, local username, boot/machine IDs and VM UUIDs remains visible. Public metadata approval is outstanding. This review is visual and cannot guarantee hidden/steganographic content absence.

## Evidence Not Supplied Here

CMMC-CM-001 drift and semantic restoration are operator-reported. [Recovery record](../Reports/CMMC-CM-001-Configuration-Drift-and-Recovery.md) retains the final SHA-256 mismatch as **exact byte-level recovery OPEN**. No screenshot, trusted baseline, restored file, hash values, source script or report is imported. The indexed image count remains 24; no picture was fabricated.

The Phase 5 [BIA](../BIA/Business-Impact-Analysis.md) is a documented analytical exercise. Its inputs, formulas, dependency matrix and arithmetic are the analysis evidence; no screenshot is needed or added for BIA. These documents do not establish actual financial losses, control effectiveness or recovery capability. Current indexed screenshot count is twenty-four including audit intake, SOC-001, AUTO-02 and CMMC-AC-001 through CMMC-AC-008.

No new screenshot establishes CA key placement, Keycloak database type, DNS closure, 8443 OIDC cutover, test-app reboot persistence, FIPS validation or backup restoration. Prior SEC-008 work is contextual only. Operator-confirmed HTTPS/RBAC/service descriptions remain identified as such, rather than relabeling these frames as those tests.
