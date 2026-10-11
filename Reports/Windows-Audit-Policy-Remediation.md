# Windows Security Audit Coverage - R-008

Review date: 2026-10-10. System: OV-DC01. **Configuration remediated, validation pending.** This is an evidence-limited lab review, not full event coverage, CMMC compliance or risk closure. Operator performed the changes; repository maintenance did not execute any VM commands.

v1.0 confirmation: the operator confirms successful generation of event ID 4688 for whoami.exe; VAL-01 visually verifies the recorded process path. This is one successful narrow test, not generation/coverage verification for every remediated subcategory. The initiating action and full record are not shown in that screenshot; no broader result is inferred.

## Baseline and Business Risk

The baseline shows Security log enabled, 104,488 records and maximum size 134,217,728 bytes (128 MiB). Logon auditing is Success and Failure; a 4625 failed-logon event is listed. This demonstrates an existing audit capability, not its absence. Record count is a point-in-time observation, not retention duration or detection quality. The event listing does not show full event fields or establish a real incident.

Incomplete selected subcategories could leave process, directory-change and identity-management activity insufficiently visible. R-008's proposed initial likelihood 3 x impact 4 = 12/High reflects that investigative uncertainty. It is not a measured probability, official compliance score or current residual rating. Owner roles, dates and business impacts remain proposed assumptions.

## Configuration Before and After

| Subcategory | Before | Verified after | Evidence |
| --- | --- | --- | --- |
| Process Creation | No Auditing | Success | Baseline supplemental, REM-04 and VAL-02 |
| Directory Service Changes | No Auditing | Success | Baseline, REM-04 and VAL-02 |
| Credential Validation | Success | Success and Failure | Baseline, REM-04 and VAL-02 |
| Kerberos Authentication Service | Success | Success and Failure | Baseline, REM-04 and VAL-02 |
| Security Group Management | Success | Success and Failure | Baseline, REM-04 and VAL-02 |

[REM-04](../Evidence/Controls/REM-04-Windows-Audit-Policy-Hardening.png) shows `auditpol /backup`, five selected `auditpol /set` operations and `auditpol /get` validation. Successful command messages and queried settings support the selected configuration changes. Backup target is `C:\SECX-002\Backups\Audit-Policy-Before.csv` **inside OV-DC01**. The operator reports the backup exists; the screenshot shows the operation, not independent file-content/hash/restore verification. No backup CSV or VM configuration was copied into the repository. [Microsoft auditpol backup documentation](https://learn.microsoft.com/en-gb/windows-server/administration/windows-commands/auditpol-backup) describes the export scope; it is not a system/data backup.

## Evidence Intake and Narrow Validation

Six unique SHA-256 source images were found in `C:\Users\kalld\Pictures\Screenshots`, visually reviewed, and copied unchanged into Evidence/Controls. No visible passwords, private-key contents, tokens or client/session secrets were observed. Metadata approval remains pending. Double extensions were normalized only on project copies; all originals and older evidence remain intact. The [manifest](../Evidence/Evidence-Manifest.csv) records provenance and matching source/copy hashes.

| Evidence | Verified result | Limit |
| --- | --- | --- |
| [CTRL-03-Windows-Audit-Logging-Baseline.png](../Evidence/Controls/CTRL-03-Windows-Audit-Logging-Baseline.png) | Security log state/count/size, 4625 listing and lower audit subcategories | Upper policy output is in supplemental image; no full 4625 event details |
| [CTRL-03-Windows-Audit-Policy-Baseline-Supplemental.png](../Evidence/Controls/CTRL-03-Windows-Audit-Policy-Baseline-Supplemental.png) | Logon Success and Failure; Process Creation No Auditing | Different image, not an exact duplicate; preserves other unassessed settings |
| [REM-04-Windows-Audit-Policy-Hardening.png](../Evidence/Controls/REM-04-Windows-Audit-Policy-Hardening.png) | Five selected after-state settings queried successfully | Does not prove all event generation or applicable SACL coverage |
| [VAL-01-Process-Creation-Audit-Event.png](../Evidence/Controls/VAL-01-Process-Creation-Audit-Event.png) | Security event 4688 lists `C:\Windows\System32\whoami.exe` | One process event observed; initiating action/full record/command-line capture and other categories not demonstrated |
| [VAL-02-Group-Policy-Refresh-Validation.png](../Evidence/Controls/VAL-02-Group-Policy-Refresh-Validation.png) | Computer/user policy refresh completed; five audit settings and AD length 14/threshold 10/30-minute timers still displayed | One refresh observation only. Original filename said Persistence; new name avoids implying reboot, repeated refresh or verified GPO source |
| [AUTO-01-Configuration-Spot-Checks.png](../Evidence/Controls/AUTO-01-Configuration-Spot-Checks.png) | Script displays 12 configuration PASS checks and REVIEW 0 | Not 12 framework controls Met; full script and generated CSV not supplied. Original Compliance label was narrowed to actual observed scope |

File timestamps and displayed guest event/report times differ; clocks/timezone alignment was not validated. Do not derive elapsed remediation/recovery time or a precise event chronology from these captures alone.

## Final Configuration Persistence Validation

The operator confirms `gpupdate /force` completed successfully on OV-DC01. VAL-02 visibly shows successful computer and user policy updates, followed by the settings below. The command's `/force` switch is operator-confirmed; the screenshot begins at the refresh output and does not display the invocation. **Successful configuration persistence through one Group Policy refresh is demonstrated.** This is not reboot persistence, repeated-refresh assurance, approved GPO provenance, password/lockout enforcement or full compliance validation.

| Post-refresh item | Confirmed result |
| --- | --- |
| Computer policy update | Completed successfully |
| User policy update | Completed successfully |
| AD minimum password length | 14 |
| Account lockout threshold | 10 |
| Lockout duration | 30 minutes |
| Lockout observation window | 30 minutes |
| Process Creation auditing | Success |
| Directory Service Changes auditing | Success |
| Credential Validation auditing | Success and Failure |
| Kerberos Authentication Service auditing | Success and Failure |
| Security Group Management auditing | Success and Failure |

Evidence named `VAL-02-Group-Policy-Persistence.png` in the update corresponds to the original `VAL-02-Group-Policy-Persistence.png.png` and its existing unchanged project copy [VAL-02-Group-Policy-Refresh-Validation.png](../Evidence/Controls/VAL-02-Group-Policy-Refresh-Validation.png), manifest E-13. No duplicate copy or source rename was needed. [VAL-01](../Evidence/Controls/VAL-01-Process-Creation-Audit-Event.png), E-12, records event ID 4688 with process `C:\Windows\System32\whoami.exe`; successful generation is operator-confirmed. It is a successful process-event test, not all-category coverage or AD lockout enforcement.

R-006/R-007 retain configuration-remediated/enforcement-pending status. R-008 retains configuration-remediated/validation-pending status. One refresh and the process-event test are completed narrow milestones; remaining evidence requirements below are not marked complete.

## Remaining Verification and Closure Criteria

1. Correlate approved safe test actions to full events for each selected subcategory, including remaining credential, Kerberos, group and directory-change cases. The observed 4625/4688 do not cover all five changes or prove AD account-lockout enforcement.
2. Review the approved directory objects/attributes/operations and applicable SACLs, then confirm representative directory-change events. Enabling Directory Service Changes alone is insufficient; [Microsoft documents its SACL-dependent coverage](https://learn.microsoft.com/en-us/windows/security/threat-protection/auditing/audit-directory-service-changes).
3. Verify authoritative GPO configuration, precedence and relevant advanced-audit override settings with sanitized resultant-policy evidence. Validate repeated refresh and approved reboot persistence; one successful refresh is only partial evidence.
4. Approve retention duration, size/volume planning, overwrite/archive behavior, access protection and audit-failure handling. 128 MiB maximum size does not establish any number of retained days.
5. Validate centralized forwarding/collection, protected storage, time synchronization, full-event receipt, source identity, correlation, alerts and investigation ownership. Nothing in these images proves central collection is operational.
6. Verify backup existence/content/integrity and controlled rollback without publishing sensitive artifacts. Obtain independent review and fictional risk-owner acceptance before closure.

The [POA&M P-008](../POAM/Plan-of-Action-and-Milestones.csv) retains these remaining milestones. R-006/R-007 enforcement statuses are unchanged. All other unresolved findings remain open, including DNS, CA signing-key separation and OIDC production cutover. Use the [control matrix](../Control-Mapping/Control-Assessment-Matrix.md) for framework associations; all relevant broader audit controls remain Partially Demonstrated or Not Assessed, not formally MET.
