# Monitoring Evidence

- E-15: [SOC-001-ADSync-Authentication-Timeline.png](SOC-001-ADSync-Authentication-Timeline.png) shows account-filtered 4624/4625 at 2026-10-10 12:06:41 PM and ADSync Running/Auto under OMNIVERSE\ADSyncMSA7efbc$.
- Expected: correlated authentication records and service-account context. Actual: timestamp/event-ID listing and current service state; full event fields, record IDs, account properties, recurrence and synchronization health are not independently shown.
- Same-second events do not establish order or cause. See [investigation](../../Reports/SOC-001-Entra-Connect-Service-Account-Authentication-Investigation.md) for operator-confirmed details and follow-up.
- Double-extension original retained; source/copy hashes match in the [manifest](../Evidence-Manifest.csv). No visible secrets observed; account/host metadata approval pending.
