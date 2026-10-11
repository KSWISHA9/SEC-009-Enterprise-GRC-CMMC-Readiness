# Standalone Configuration Validator - Results and Import Status

SEC-009 v1.0 addendum, 2026-10-10. **Selected configuration baseline only**, not comprehensive NIST/CMMC compliance validation, a certification, formal assessment score or proof of enforcement. The operator reports creating and independently executing a standalone PowerShell validator on OV-DC01. The repository maintainer did not execute it or inspect its source.

## Available Evidence Versus VM-Only Artifacts

| Reference | Artifact and location | Current verification / host availability |
| --- | --- | --- |
| E-16 | [AUTO-02-Standalone-Compliance-Validation.png](../Evidence/Automation/AUTO-02-Standalone-Compliance-Validation.png) | Host project screenshot exists; visually reviewed. Shows standalone invocation, 12 PASS/0 REVIEW and output report path |
| VM-AUTO-01 | `C:\SECX-002\Scripts\Invoke-SECX002Compliance.ps1` on OV-DC01 | Operator-confirmed standalone script. Invocation visible; source and SHA-256 not supplied. **Pending host import** |
| VM-AUTO-02 | `C:\SECX-002\Reports\SECX-002-Compliance-20261010-192143.csv` on OV-DC01 | Operator-confirmed successful CSV. Path visible in output; actual CSV contents/hash not inspected. **Pending host import** |

The source image was named `SECX-002-Compliance-20261010-192143.csv.png`; it is a PNG screenshot, **not the CSV**. Copied unchanged under the requested AUTO-02 name; original retained and source/copy hashes match in the [manifest](../Evidence/Evidence-Manifest.csv). No visible password, token or private-key contents observed; account/path metadata approval remains pending. Guest report time and host file timestamps have not been reconciled.

The script is reported read-only with respect to assessed security configuration; writing a report CSV is an output operation. Source review is still needed to independently establish its behavior, dependencies and absence of configuration changes. Independent execution means the operator ran the saved script on OV-DC01; it is not an independent maintainer audit or host-side execution.

## Selected Baseline Results

| Check group | Number | Displayed actual values | Displayed result |
| --- | --- | --- | --- |
| AD password/lockout settings | 3 | Minimum length 14, complexity True, lockout threshold 10 | 3 PASS |
| Windows Firewall enabled flags | 3 | Domain True, Private True, Public True | 3 PASS |
| Advanced auditing subcategories | 5 | Process Creation/Directory Service Changes: Success; Credential Validation/Kerberos Authentication Service/Security Group Management: Success and Failure | 5 PASS |
| Security event log enabled | 1 | True | 1 PASS |
| Total selected checks | 12 | Screenshot summary | 12 PASS, 0 REVIEW |

The screenshot's expected values include minimum length 14 or more and threshold 1-10 attempts. These are script baseline criteria, not universal NIST/CMMC numeric requirements. This standalone result does not test lockout duration/window, password rejection, failed-logon enforcement, effective firewall actions/traffic, all audit events/SACLs, log retention/collection, reboot persistence, recovery or the full system boundary. Other evidence documents some configurations separately; do not attribute those tests to this run.

## Parser Correction and Rerun

The operator reports the original auditpol parser incorrectly classified five audit checks as REVIEW. The parser was corrected, assessment rerun, and the saved standalone script independently executed. AUTO-02 directly displays the standalone invocation and successful 12/0 output; AUTO-01 is an earlier corrected configuration spot-check screenshot, not proof of this saved script's contents.

The initial five REVIEW outputs and old/new parser source are not supplied. Record this as a reported parsing/validation defect, **not five confirmed security-control failures or remediations**. Source diff and representative parser fixtures for Success, Failure, Success and Failure, No Auditing, missing/error output and applicable localization would be useful future validation. No parser code is fabricated here.

## Import Instructions - No Transfer Performed

1. On OV-DC01, identify the two exact files above and record SHA-256 using `Get-FileHash -LiteralPath <exact path> -Algorithm SHA256`. Do not execute the validator again merely to transfer it. Keep originals intact.
2. Use an existing approved transfer channel to a temporary host review location. Do not change VirtualBox networking, service credentials, firewall rules or VM configurations for this documentation task. Nothing was transferred from the VM by the maintainer.
3. Review the script as text and the actual CSV as data for credentials, tokens, private-key material, sensitive records and unintended configuration-changing commands. Verify source/copy hashes and provenance. Do not execute an unreviewed import automatically.
4. After review, copy without overwriting any different existing file to these planned destinations:
   - `C:\Users\kalld\Documents\OmniVerse-SecurityX\SEC-009\Scripts\Invoke-SECX002Compliance.ps1`
   - `C:\Users\kalld\Documents\OmniVerse-SecurityX\SEC-009\Reports\SECX-002-Compliance-20261010-192143.csv`
5. Index the real imported artifacts with hashes, review status and evidence basis; reconcile CSV rows/totals with AUTO-02 and update pending-import labels only after successful verification. Recheck publication suitability and obtain approval before staging, committing or publishing.

Neither planned destination is currently claimed to exist. [Scripts import placeholder](../Scripts/README.md) is documentation only; no executable placeholder, dummy CSV or recreated validator is supplied. [Traceability](../Control-Mapping/Evidence-Traceability.md) separates the existing screenshot from both VM-only artifacts. Eight risk/POA&M statuses and broader control dispositions remain unchanged.
