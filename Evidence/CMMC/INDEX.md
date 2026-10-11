# CMMC Effective Access Evidence

| Evidence | Expected | Observed | Limits |
| --- | --- | --- | --- |
| E-23 / [AC-007 Authorized Effective Access](CMMC-AC-007-Authorized-Effective-Access.png) | Read-only permissions for the reader-group member | Read data, attributes and permissions allowed; Write data, Delete and Full Control not allowed | Windows permission evaluation, not login/file-read attempt; membership and disabled state operator-confirmed |
| E-24 / [AC-008 Unauthorized Effective Access](CMMC-AC-008-Unauthorized-Effective-Access.png) | No evaluated file permissions for the nonmember | No displayed permission granted | Not an actual denial attempt; same-file association/membership/disabled state operator-confirmed |

Existing project images preserved and indexed in place, with pre-edit snapshot/hash verification in the manifest. No external source originals located. No visible secrets observed; metadata approval pending. [Remediation record](../../Reports/CMMC-AC-001-Controlled-Access-Control-Exercise.md) explains historical ACL steps, final configuration, automated PASS scope and partial AC.L2-3.1.1/3.1.5 mapping. Both evaluated accounts remained disabled; no actual interactive login or file-read testing was performed.
