# Proposed Recovery Validation Plan

Phase 5 planning date: 2026-10-10. **Planning artifact only. No test is scheduled, authorized, executed or passed.** Owner roles, acceptance process and resources are proposed assumptions. This complements the eight-risk [POA&M](Plan-of-Action-and-Milestones.csv) without adding a fabricated risk or closing an action.

## Objectives and Traceability

| Proposed test | Business objective | Existing risk relationship | Proposed owner | Required verification |
| --- | --- | --- | --- | --- |
| RV-01 AD/DNS restore | RTO 2 hours; RPO 1 hour | R-003 DNS; R-006/007 policy preservation/enforcement pending | AD administrator | Safe restore, recovered-state timestamp, locator/DNS/authentication checks, elapsed service-ready time |
| RV-02 Keycloak restore | RTO 2 hours; RPO 1 hour | R-005 database; R-002 trust; R-001 promotion prerequisites | IAM/database engineer | Consistent DB/config restore, identities/roles/clients and new-login checks, trusted HTTPS, elapsed time/data point |
| RV-03 contractor portal restore | RTO 4 hours; RPO 2 hours | R-001 intended OIDC deployment and dependencies | Application/platform engineer | Restore scoped content/config, successful approved access, denied viewer access and dependency validation with timing/data point |
| RV-04 shared-host recovery | Meet all applicable service targets from one interruption clock | Shared dependency in SSP/BIA, not itself a separately confirmed finding | Platform engineer | Off-host recoverability or approved alternate platform, networking/trust/admin access and all three end-to-end results |

The [BIA](../BIA/Business-Impact-Analysis.md) owns current target values. Recovery-validation dates are not assigned; first approve architecture, safe test conditions and resources. Existing eight-risk due dates remain proposals and do not authorize destructive recovery exercises or establish a recovery SLA.

## Proposed Milestones

1. Confirm business-owner acceptance of targets and required recovered data; distinguish the current Basic app from intended OIDC service.
2. Inventory backup type, protected location, successful restore points, encryption/key custody and recovery privileges without copying secrets.
3. Define a consistent interruption clock, dependency order/parallelism, isolated restoration environment, rollback and emergency access.
4. Obtain explicit operator approval before any VM, backup or network change.
5. Perform approved tests and capture safe logs, elapsed times, recovered timestamps and functional results.
6. Compare results with each objective, record unmet targets and obtain independent review before making achievement or residual-risk claims.

AD policy XML existence is not a system-state restore. A service restart is not a database/data restore. Backup frequency is not proof of recovered data age. The hypothetical $5,000 residual ALE is not a test result and does not verify recovery effectiveness.
