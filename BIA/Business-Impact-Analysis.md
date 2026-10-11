# Business Impact Analysis

Phase 5 analysis date: 2026-10-10. **All business functions, impacts, financial inputs, control-effectiveness estimates and recovery targets below are hypothetical proposals supplied for the fictional OmniVerse Defense Systems scenario.** No actual company financial data, customer loss, contract penalty, recovery capability or achieved RTO/RPO was verified. No real CUI is present.

## Proposed Critical Functions

| Business service | Proposed impact if unavailable | Proposed RTO | Proposed RPO | Capability status |
| --- | --- | --- | --- | --- |
| Active Directory / DNS | Employees cannot reliably authenticate or resolve internal services | 2 hours | 1 hour | Not demonstrated |
| Keycloak identity provider | Users cannot initiate new portal logins; existing-session behavior is unassessed | 2 hours | 1 hour | Not demonstrated |
| Internal contractor portal | Project work is interrupted | 4 hours | 2 hours | Not demonstrated |

RTO is the maximum targeted time to restore an acceptable service level. RPO is the maximum acceptable data-loss interval measured in time. The clock for a scenario must be defined consistently from the service disruption; dependency recovery, application restoration and end-to-end verification must fit inside that service's RTO. Meeting an RPO requires identifying the recovered data point, not merely showing that a service starts.

These values supersede the earlier draft targets and financial scenarios. Host and Kali are supporting dependencies, not additional business services with independently approved numeric targets. The earlier host 8-hour/24-hour and Kali 24-hour/24-hour suggestions are no longer current objectives. No backup schedule, replication or redundancy has been verified against the new targets.

## Business-Service Dependency Matrix

| Service | Technical dependency | Dependency basis | Failure consequence / recovery requirement |
| --- | --- | --- | --- |
| AD / DNS | OV-DC01 directory data, DNS zones/configuration and guest storage | VM identity observed; business reliance proposed | Restore consistent directory/DNS state and validate service-location/authentication; data point within 1 hour |
| AD / DNS | VirtualBox host, VM disks, networking and power | Shared local host observed; detailed resilience unassessed | Host/guest path must be available early enough for the 2-hour service deadline; alternate recovery platform may be needed |
| Keycloak | Ubuntu guest, realm/database state, service configuration and protected secrets | Runtime/IdP presence reported/observed; database mode operator-confirmed | Restore identities/roles/client configuration and service access within 2 hours using a data point within 1 hour |
| Keycloak | TLS certificate/trust and DNS where configured names are used | HTTPS operator-confirmed; CA configuration and named resolution unassessed | Restore valid trust/name resolution before login validation; no CA key publication |
| Keycloak | AD federation or synchronization, if later designed | Not established in this lab | Do not assume AD-to-Keycloak integration or require sequential AD restore on that basis |
| Contractor portal | Ubuntu app/code/configuration, stored content and virtualized storage | Current 8443 Basic and separate 8445 OIDC deployments documented | Define the recovery scope before testing; restore content/configuration within 2-hour data-loss tolerance |
| Contractor portal | Keycloak, role enforcement, tokens/sessions and TLS for intended OIDC path | Proposed business architecture; RBAC operator-confirmed on 8445 only | Verify new logins and authorized/denied roles after recovery; 8443 Basic restart is not OIDC portal restoration |
| Contractor portal | AD/DNS for employee workflows and named services where applicable | Fictional business dependency; actual application federation not confirmed | Validate applicable client resolution/authentication paths without inventing a direct AD integration |
| All three | Protected off-host backups, recovery credentials/runbooks and available operators | Proposed recovery design; capabilities unverified | Recover from loss of the runtime host and retain safe administrative access |
| All three | Kali or another approved validation client | Kali inventory observed; validation-client choice proposed | Use a working client for independent end-to-end checks; it is not assumed required for production service runtime |

The host is a common-mode failure dependency. A host outage that lasts beyond 2 hours prevents the two identity targets being met on that host alone. Proposed mitigations are an alternate restoration platform or greater availability, subject to design approval. Separate 2-hour objectives for AD and Keycloak cannot simply be added into a 4-hour allowance if the business requires both within 2 hours. Parallel recovery and prerequisite timing need a tested runbook.

## Illustrative AD Outage Financial Model (USD)

Modeled asset value is an assumed economic-exposure proxy, not a measured hardware value or actual company valuation. Exposure factor and ARO are illustrative inputs, not calibrated loss or incident-frequency estimates. ARO is independent of the risk register's 1-5 likelihood judgments; no conversion between them is used.

| Input / result | Value | Basis |
| --- | --- | --- |
| Modeled asset value / exposure | $200,000 | Hypothetical input |
| Exposure factor | 25% (0.25) | Hypothetical input |
| Single Loss Expectancy (SLE) | $50,000 per modeled event | 200000 x 0.25 |
| Annualized rate of occurrence (ARO) | 0.4 events/year | Hypothetical frequency; not a 40% breach probability |
| Annualized Loss Expectancy (ALE) | $20,000/year | 50000 x 0.4 |

```text
SLE = modeled asset value x exposure factor
    = $200,000 x 0.25 = $50,000
ALE = SLE x annualized rate of occurrence
    = $50,000 x 0.4 = $20,000/year
```

This is an AD outage scenario, not a demonstrated compromise or a separate scored risk. No actual losses or service downtime were measured. These documented inputs and reproducible formulas are the analysis evidence; no BIA screenshot is required.

## Proposed Security Investment

| Input / result | Annual value | Basis |
| --- | --- | --- |
| Baseline modeled ALE | $20,000 | Calculation above |
| Proposed control cost | $6,000 | Hypothetical input; no quote or approved expenditure |
| Hypothetical residual ALE | $5,000 | Assumed control effectiveness, not verified risk reduction |
| Expected modeled loss reduction | $15,000 | 20000 - 5000 |
| Expected modeled net annual benefit | $9,000 | 15000 - 6000 |

```text
Annual modeled reduction = baseline ALE - assumed residual ALE
                         = $20,000 - $5,000 = $15,000
Net modeled annual benefit = reduction - annual control cost
                           = $15,000 - $6,000 = $9,000
```

Proposed decision: consider the investment if feasibility, effectiveness and full lifecycle cost are independently substantiated. Under unchanged assumptions, break-even residual ALE is $14,000/year (20000 - 6000). At residual ALE $15,000/year the modeled net benefit becomes -$1,000/year. Doubling baseline ARO to 0.8 makes baseline ALE $40,000/year but does not justify retaining the same residual estimate without review.

This simplified annual model excludes one-time implementation/migration costs, additional staffing, discounting, taxes, outage during deployment and uncertainty ranges. No particular product or vendor was selected. The assumed residual ALE must not be entered as the verified residual rating for R-006/R-007 or attributed to the AD configuration change.

## Recovery Verification Required

| Service / objective | Proposed backup and restoration evidence | End-to-end acceptance evidence | Status |
| --- | --- | --- | --- |
| AD/DNS: RTO 2h, RPO 1h | Approved AD recovery approach; protected directory/DNS backups or recoverable data points; controlled restoration on a safe platform | Record disruption start and service-ready time; recover data timestamp within 1h; verify AD locator, DNS and test-user authentication within 2h | Not tested |
| Keycloak: RTO 2h, RPO 1h | Consistent realm/database backup, protected configuration/secrets and restore procedure; account for database-mode finding | Verify identities, role/client configuration, TLS and new login; record service-ready time within 2h and recovered state within 1h | Not tested |
| Contractor portal: RTO 4h, RPO 2h | Versioned code/configuration plus consistent content/data backup; define Basic or OIDC recovery scope explicitly | Verify content, legitimate access, denied roles and dependent login path within 4h; recovered data point within 2h | Not tested |
| Common host loss | Safe loss-of-host scenario, off-host backups and alternate-host recovery plan where needed | Test the three service deadlines from the same interruption clock, including network/trust and operator prerequisites | Not tested |

Backup cadence alone does not prove RPO: backup consistency, replication lag, backup failures, retention and restore integrity must be checked. Historical application stop/start, enabled services, a policy XML export or a snapshot listing does not demonstrate these recovery objectives. No backup/restore command or VM test was performed for this exercise.

AD policy remediation changes the configuration baseline, not these hypothetical recovery targets or financial inputs. REM-03 checks baseline-export existence on OV-DC01, not backup content, restore success or RPO achievement. Password/lockout enforcement testing should use approved dedicated accounts and preserve emergency access to avoid disrupting the identity function. The 30-minute lockout setting is a policy timer, not an RTO or measured outage.

Obtain stakeholder-approved service priorities, workload volumes, data-change rates, outage costs and actual dependency diagrams. Identify backup locations, retention, encryption, restore privileges and recovery runbooks. Conduct safe, approved restoration tests including authenticated access and content/role checks. Record elapsed recovery time and recovered data timestamps before claiming any RTO/RPO achieved.
