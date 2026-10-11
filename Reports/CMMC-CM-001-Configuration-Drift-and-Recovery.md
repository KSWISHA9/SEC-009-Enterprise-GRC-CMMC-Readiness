# CMMC-CM-001 - Configuration Drift and Recovery Verification

Status: **Exact byte-level recovery verification OPEN.** This controlled simulated exercise is recorded from the operator's latest update; no corresponding screenshot, script, configuration file, trusted-baseline hash or recovered-file hash was located in the current project. No test was repeated by the maintainer.

## Reported Sequence

| Stage | Expected | Operator-reported actual | Disposition |
| --- | --- | --- | --- |
| Trusted baseline | AuditLogging Enabled; retain trusted file/hash | Original trusted baseline existed; actual bytes/hash not supplied | Baseline artifact pending import |
| Controlled drift | Detect change from the trusted configuration | AuditLogging intentionally changed Enabled to Disabled; drift detected | Operator-confirmed detection, not independently reproduced |
| Setting restoration | Return AuditLogging to Enabled | Setting restored to Enabled | Semantic setting restoration reported |
| Exact recovery | Restored file SHA-256 equals trusted baseline SHA-256 | Final SHA-256 did not match the original trusted baseline | **OPEN; not PASS** |

A restored setting and identical file bytes are different acceptance criteria. Whitespace, encoding, line endings, serialization or another change could cause a hash difference, but none is established as the cause. Do not dismiss the mismatch, substitute a new baseline or claim byte-level recovery without approved comparison and verification.

## Finding and Acceptance Criteria

Record CM-001-F01: drift detection and reported setting restoration are complete within the operator's narrow exercise; exact trusted-baseline recovery is unverified and open. This is an additional exercise record, not an automatically scored ninth risk or a closure of R-001 through R-008.

Next approved review needs the trusted baseline and its recorded SHA-256, drifted/restored copies and hashes, exact comparison targets, safe validator source and output, change chronology and an explanation of any remaining difference. Preserve originals. Confirm semantic and byte-level outcomes separately; if byte-identical recovery is required, obtain a matching verified hash before acceptance.

If a changed baseline is legitimately desired, approve and document that new baseline separately rather than treating it as restoration of the original. Do not transfer secrets or execute changes during documentation cleanup.

## Selected Control Associations

| Existing requirement | Partial technical association | Remaining gap |
| --- | --- | --- |
| SP 800-171 Rev. 2 3.4.2 / CM.L2-3.4.2 | Reported comparison/restoration of one lab security setting | Source artifacts, approved baseline, independent validation and exact recovery missing |
| SP 800-171 Rev. 2 3.4.3 / CM.L2-3.4.3 | Reported intentional change and restoration sequence | Formal approval, complete change record and verified recovery missing |
| SP 800-53 Rev. 5 CM-3 / CM-6 | Contextual change/configuration-setting associations | No complete control assessment or system-wide drift assurance |

These identifiers already occur in the selected project matrix. This operator-reported exercise is contextual supplemental evidence; their local Partially Demonstrated dispositions are not upgraded. No new control test, screenshot, CMMC certification, complete assessment, backup restoration or PASS recovery outcome is invented.

## Publication and Next Phase

Hands-on work remains paused until Monday, October 12, 2026. Obtain source evidence and review it before claiming independently verified drift detection or baseline recovery. The [SSP](../SSP/System-Security-Plan.md), [control matrix](../Control-Mapping/Control-Assessment-Matrix.md) and [missing information](Assumptions-and-Missing-Information.md) reference this open result. No VM changes, commit, push or publication performed.
