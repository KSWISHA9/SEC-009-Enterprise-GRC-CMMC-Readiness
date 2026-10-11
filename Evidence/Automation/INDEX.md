# Automation Evidence

- E-16: [AUTO-02-Standalone-Compliance-Validation.png](AUTO-02-Standalone-Compliance-Validation.png) shows OV-DC01 invoking the saved PowerShell validator, 12 selected configuration PASS checks, 0 REVIEW and the VM CSV output path.
- Original is `SECX-002-Compliance-20261010-192143.csv.png`, a screenshot rather than actual CSV. It remains unchanged; matching source/copy hashes are recorded in the [manifest](../Evidence-Manifest.csv).
- The `.ps1` and actual `.csv` remain VM-only, pending host import. Screenshot does not establish source behavior, CSV contents or full compliance. [Result and import documentation](../../Reports/Automation-Validation-and-Import.md) records provenance and limitations.
- No visible secrets observed; account/path metadata and exact publication bundle review remain pending. No VM commands, transfer, commit or publication performed.
