# Assumptions and Missing Information

## Controlled ACL Exercise - Evidence Limits

[CMMC-AC-001](CMMC-AC-001-Controlled-Access-Control-Exercise.md) now includes E-23/24 Windows Effective Access evaluations alongside E-17 through E-22 configuration history. Read-only evaluated rights versus no evaluated grants are visible. Current reader membership/nonmembership and both test accounts staying disabled are operator-confirmed, not shown by these screenshots. Prior empty-group result is historical. No interactive login or actual file-read/denial attempt performed. OU setup, organizational scope, protection flag and persistence remain unverified. Printed automated PASS remains operator-confirmed; E-22 counters are visible. Current indexed count twenty-four; no visible secrets observed in either new capture; metadata approval pending.

## Confirmed Versus Observed

[CMMC-CM-001](CMMC-CM-001-Configuration-Drift-and-Recovery.md) adds operator-reported AuditLogging drift detection and restoration to Enabled. Final SHA-256 does not match the original trusted baseline: **exact byte-level recovery verification OPEN, not PASS**. Corresponding images, baseline/restored file bytes, hashes, validator code/output and approved change/acceptance evidence are missing. Cause of mismatch is not established; no ninth scored risk or closure is inferred.

[Standalone automation update](Automation-Validation-and-Import.md): E-16 visually shows saved-script invocation and 12 PASS/0 REVIEW for the selected baseline. Corrected parser history/read-only design are operator-confirmed; script source and actual CSV remain on OV-DC01, pending host import/review. Original five incorrect REVIEW outputs, parser diff/test fixtures and artifact hashes are unsupplied. This is not full compliance or enforcement evidence.

[SOC-001](SOC-001-Entra-Connect-Service-Account-Authentication-Investigation.md) adds observed same-second account-filtered 4624/4625 and ADSync Running/Auto identity output. Full failure fields and account enabled/PasswordLastSet are operator-confirmed where not shown. Event order, root cause, recurrence and sync health remain unconfirmed; successful authentication/service state is not sync-health proof. No reset or VM action performed.

v1.0 status and release gates are in [Finalization and Readiness](Finalization-v1.0.md). E-09 through E-14 substantiate selected Windows audit baseline/hardening, one 4688 for whoami.exe and one policy refresh. Generation of that test process event is operator-confirmed; full event coverage, SACLs, GPO provenance/reboot persistence, retention and centralized collection remain unverified. No AD enforcement test is inferred from 4625/4688.

The user confirms the VM allocations/IPs, NAT plus host-only networking, HTTPS ports, successful test-port RBAC, app/Keycloak active and enabled, incomplete cutover, unresolved DNS and CA key placement. E-01 through E-05 substantiate selected baseline subsets. New REM-01/02/03 (E-06/07/08) show AD before/after configuration and cross-command validation. Development-file database is a user-supplied assessment finding, not independently corroborated by these images. Kali 10.10.10.100 is supplied and appears in UFW allow rules, but a Kali interface capture is missing.

## Proposed Assumptions

- Fictional DoD subcontractor, simulated business mission/data and future CUI scenario.
- All likelihood/impact values, bands, impact narratives and remediation order.
- Owner roles, acceptance process and calendar due dates based on 2026-10-10.
- RTO/RPO, financial asset values, exposure factors and annual event frequencies.
- Phase 5 targets: AD/DNS 2h/1h, Keycloak 2h/1h and contractor portal 4h/2h. These supersede earlier values; no recovery target is demonstrated.
- Phase 5 AD outage inputs: modeled exposure $200,000, exposure factor 25%, ARO 0.4, annual control cost $6,000 and residual ALE $5,000. SLE $50,000, ALE $20,000, reduction $15,000 and net benefit $9,000 are arithmetic results, not verified company losses or control effectiveness.
- Monthly monitoring cadence and proposed policies, architectures and remediation approaches.

These are not agreed obligations. Risk scores retain the initial baseline and are not measured likelihoods or updated residual scores. Length 7/threshold 0 are historical observations; length 14/threshold 10 and 30-minute timers are new observed configuration facts, not candidate settings. Enforcement and compatibility still require testing. Baseline XML existence is shown on OV-DC01, not verified from this host or by opening/restoring the file.

## Missing Information and Evidence

| Needed input | Why it matters |
| --- | --- |
| VirtualBox host OS/build, CPU/RAM, disk encryption, patching, EDR and backup | Common-mode platform dependency not assessed |
| Current Kali guest version/interface output | VM type is Debian (64-bit), not evidence of exact guest version/IP |
| Sanitized Keycloak database/startup configuration | Confirm development-file finding without importing secrets |
| Sanitized CA storage architecture/permissions | Corroborate co-location and plan separation; never include key contents |
| Approved policy rationale; representative-user policy and enforcement tests | Configuration now verified; Administrator no-FGPP output is not all-user policy or lockout proof |
| Effective Windows Firewall policy and applicable-path tests | NotConfigured does not establish runtime permit/deny behavior |
| Sanitized NAT forwarding map and admin-path tests | Determine actual SSH exposure and avoid lockout during changes |
| DNS root/DC/GC/AD locator comparisons and intended record behavior | Preserve unresolved finding until cause and expectations verified |
| Route/identity/status/port-correlated OIDC evidence and source review | Confirm RBAC, token/session enforcement and eventual 8443 promotion |
| Backup/export/restore runbooks and timed restoration evidence | Evaluate proposed RTO/RPO; no successful backup restore shown |
| Data-change rates, backup consistency and recovered data timestamps | Determine whether 1-hour identity and 2-hour portal data-loss targets can be met |
| Control proposal, validated effectiveness and full lifecycle costs | Test the illustrative financial business case; no product selection or expenditure approval exists |
| Actual contract, data types, staff/policies, applicable baseline | Required only for a real assessment; absent in fictional scenario |
| Full requirement/objective coverage with interviews and tests | Needed before any formal CMMC determination |
| Five Atlantic Defense Cloud Services evidence packages and service/contract scope | Incident response, privileged MFA, encryption, backup/recovery and applicable CMMC assurance all Unverified; defer approval, not confirmed noncompliance |

## Publication Review

Previously held AC-008 is now visually reviewed with AC-007 and indexed in place as E-23/E-24. Both existed in the host project before edits; hashes match pre-edit snapshots. No external source originals located and no copy-from-Pictures provenance claimed. No visible credentials, tokens or private keys observed. Same-file association for AC-008 (header cropped), membership and both disabled states are operator-confirmed. Exact publication bundle/metadata approval is still required.

Twenty-four indexed images visually reviewed: earlier source copies plus two existing project captures. No visible passwords, tokens, client secrets or private-key contents observed. Domain/account names and paths remain visible, requiring approval. Original Pictures screenshots and both existing Evidence/CMMC images are preserved. No VM or SEC-008 changes; no commit/push/publication.

No Git initialization, stage, commit, push or publication is authorized by this assessment. Recheck the exact eventual release bundle and obtain approval before publishing.
