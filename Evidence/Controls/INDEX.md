# Control Evidence

- [CMMC-AC-004 restricted ACL](CMMC-AC-004-RBAC-Restricted-ACL.png): Global Security reader group, final icacls three-identity ACL; Users absent.
- [CMMC-AC-005 configuration validation](CMMC-AC-005-RBAC-Membership-And-ACL-Validation.png): disabled test account, empty group-members output, SYSTEM/Administrators FullControl and reader Read/Synchronize, all Allow/IsInherited False. Heading "negative test" is not an actual denial test.
- [CMMC-AC-006 automated counters](CMMC-AC-006-Automated-Access-Policy-PASS.png): 0 unexpected Allow ACEs, 1 reader ACE, Enabled False; PASS branch logic visible, printed outcome operator-confirmed/cropped out. No real user access test.

- [CMMC-AC-001 baseline](CMMC-AC-001-Privileged-Access-Baseline.png): baseline 2,607 users, 2,594 enabled, 13 disabled; two privileged groups each list Administrator.
- [CMMC-AC-002 intentional finding](CMMC-AC-002-Excessive-Permissions-Detected.png): training file with explicit test-user Full Control and inherited administrative/Users entries.
- [CMMC-AC-003 remediation](CMMC-AC-003-Least-Privilege-Remediation.png): historical interim explicit grant removal retained inherited administrative rights and Users RX; later AC-004/005 supersede that ACL. [Finding report](../../Reports/CMMC-AC-001-Controlled-Access-Control-Exercise.md) distinguishes ACL inspection from effective-access/compliance validation.

- [CTRL-01 Ubuntu](CTRL-01-Ubuntu-Security-Baseline.png): runtime UFW, interfaces, listeners and unlabeled service-state output.
- [CTRL-02 AD baseline](CTRL-02-Active-Directory-Security-Baseline.png): enabled profiles, NotConfigured default actions, password/lockout settings and displayed admin membership.
- [CTRL-03 AD supplemental](CTRL-03-Active-Directory-Baseline-Supplemental.png): different capture of the same settings, retained rather than overwritten.
- [CTRL-04 domain summary](CTRL-04-AD-Domain-Summary.png): domain/function/PDC output; empty sections are not proof of other controls.
- [REM-01 before](REM-01-AD-Password-Policy-Before.png): length 7, threshold 0, complexity enabled, duration/window 30 minutes, baseline-export message.
- [REM-02 after](REM-02-AD-Password-Policy-After.png): length 14, threshold 10, complexity enabled, duration/window 30 minutes.
- [REM-03 validation](REM-03-AD-Policy-Validation.png): corroborating PowerShell/net accounts, no displayed Administrator fine-grained policy, backup existence True on OV-DC01.

- [CTRL-03 Windows audit baseline](CTRL-03-Windows-Audit-Logging-Baseline.png): enabled Security log, 104,488 records, 128 MiB maximum, 4625 listing and selected baseline settings. Separate filename from existing CTRL-03 AD supplemental; neither overwritten.
- [CTRL-03 audit supplemental](CTRL-03-Windows-Audit-Policy-Baseline-Supplemental.png): upper policy output, including Logon Success and Failure and Process Creation No Auditing.
- [REM-04 audit hardening](REM-04-Windows-Audit-Policy-Hardening.png): backup command and five selected after-state audit settings.
- [VAL-01 process event](VAL-01-Process-Creation-Audit-Event.png): event 4688 for whoami.exe; one event, not all audit coverage.
- [VAL-02 refresh validation](VAL-02-Group-Policy-Refresh-Validation.png): settings observed after one successful Group Policy refresh, not full persistence proof.
- Final operator update confirms `gpupdate /force`; computer/user success outputs and AD/audit values establish configuration persistence through one refresh only. The supplied `VAL-02-Group-Policy-Persistence.png` maps to this same preserved image (E-13), not an additional capture. No reboot or full GPO provenance is established. VAL-01/E-12 records 4688 for `C:\Windows\System32\whoami.exe` with generation operator-confirmed.
- [AUTO-01 spot-checks](AUTO-01-Configuration-Spot-Checks.png): 12 script configuration PASS results, not compliance/control-assessment outcomes.

CTRL captures remain historical baseline observations. REM captures verify configuration remediation but not risk closure. VAL captures support only the specific observed process event/refresh results. [Main index](../INDEX.md) defines actual results, security review and missing evidence; [R-008 report](../../Reports/Windows-Audit-Policy-Remediation.md) documents outstanding event/SACL/persistence/retention/collection validation.
