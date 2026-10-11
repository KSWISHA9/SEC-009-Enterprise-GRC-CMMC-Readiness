# SOC-001 - Entra Connect Service Account Authentication Investigation

Date: 2026-10-10. Host: OV-DC01. **Possible transient service-account credential issue; root cause unconfirmed. Low observed security concern; no demonstrated malicious activity.** This is an investigation addendum inside SEC-009, not a confirmed cyberattack or a new repository.

## Event and Account Context

| Item | Recorded or operator-confirmed detail |
| --- | --- |
| Failure | Security Event 4625, October 10, 2026, 12:06:41 PM |
| Account | ADSyncMSA7efbc$; AD account ADSyncMSA7efbc enabled |
| Logon Type | 5 (Service) |
| Status / SubStatus | 0xC000006D / 0xC000006A (incorrect password) |
| Process / workstation | `C:\Windows\System32\services.exe` / OV-DC01 |
| Source IP / authentication package | Not recorded / Negotiate |
| PasswordLastSet | October 10, 2026, 11:01:41 AM |
| Service | ADSync (Microsoft Azure AD Sync), `OMNIVERSE\ADSyncMSA7efbc$`, Running, Automatic |
| Successful authentication | Event 4624 for the same account at 12:06:41 PM |

Microsoft documents service logon type 5 and the bad-password meaning of 0xC000006A in [Event 4625 guidance](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-10/security/threat-protection/auditing/event-4625). The code describes the failed authentication result, not its root cause or an attacker. Negotiate alone does not establish the underlying protocol. Missing source IP is not proof of a particular origin.

## Evidence and Timeline Limits

[SOC-001-ADSync-Authentication-Timeline.png](../Evidence/Monitoring/SOC-001-ADSync-Authentication-Timeline.png), manifest E-15, shows a Security query filtered for this account, 4624 and 4625 at the same displayed second, and ADSync Running/Auto with the matching service identity. Full failure fields, AD enabled state and PasswordLastSet are operator-confirmed, not independently displayed here. The successful event's logon type, raw event XML and record IDs were not supplied.

Same-second timestamps do not establish failure-before-success, retry sequence or causality. PasswordLastSet precedes the reported events but does not prove a stale-credential cause. Guest timezone, clock alignment and observation time of current service status were not independently validated. Running now does not establish uninterrupted operation at the event time.

## Assessment and Follow-Up

A transient credential inconsistency is plausible, not a resolved cause. Supplied evidence does not demonstrate malicious activity, ongoing outage, recurrence rate or synchronization failure. A 4624 and running ADSync do **not** independently prove healthy Entra Connect synchronization or successful imports/exports. Low observed concern is a limited triage judgment, not a compliance finding or residual-risk reduction.

Monitor recurrence for this identity, verify synchronization health and recent connector/import/export results, and review relevant Application/System and ADSync service logs if failures continue. Preserve sanitized full records and correlate record IDs, times, service activity and account lifecycle before determining cause. [Microsoft synchronization operations guidance](https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-sync-staging-server) distinguishes operational sync verification from service status.

**Do not reset service credentials without further diagnosis.** No credential reset, service change, VM command or synchronization test was executed for this report. Root cause and sync health remain unconfirmed. This observation does not close R-006/R-007/R-008, create an unsupported R-009 or imply AD-to-Keycloak integration.

Screenshot copied unchanged from the double-extension source; SHA-256 matches and original is retained. No visible credential value, token or private-key contents observed; account/host metadata approval and release review remain pending. No commit, push or publication performed.
