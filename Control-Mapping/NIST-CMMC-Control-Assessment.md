# Selected NIST and CMMC Readiness Assessment

Verification date: 2026-10-10. **Partial lab readiness review only.** No complete baseline, assessment-objective coverage, CMMC status or certification is asserted.

## Framework Distinctions

NIST SP 800-53 Rev. 5 is a broad control catalog. Its identifiers are used below as thematic references, not a selected federal baseline. RMF is the risk-management process in SP 800-37 Rev. 2; using its steps does not grant an authorization.

CMMC Level 2 uses SP 800-171 Revision 2 under 32 CFR 170.14. Revision 3 supersedes Revision 2 as a NIST publication, but this does not silently replace the incorporated CMMC basis. All 3.x requirement numbers below are explicitly Revision 2. For an actual engagement, verify the contract, rule, assessment type, scope and applicable edition. See [32 CFR Part 170, official CFR](https://www.govinfo.gov/link/cfr/32/170?link-type=pdf&year=mostrecent), [NIST Revision 2 publication status](https://csrc.nist.gov/pubs/sp/800/171/r2/upd1/final) and [current NIST CUI publications](https://csrc.nist.gov/Projects/protecting-controlled-unclassified-information/publications).

Mappings between frameworks are analytical associations, not one-to-one equivalence or evidence of compliance. SP 800-171 Rev. 2 Appendix D references an earlier 800-53 revision; the Rev. 5 associations below are separately identified, not presented as that appendix verbatim.

## Selected Assessment

The authoritative six-field row assessment is now the [Control Assessment Matrix](Control-Assessment-Matrix.md), supported by [Evidence Traceability](Evidence-Traceability.md) and the [RMF lifecycle](../RMF/RMF-Lifecycle.md). The summary below preserves earlier assessment context; its descriptive dispositions are not official findings. Use the matrix's defined local status vocabulary for the selected rows it covers. Themes here that are outside that matrix remain contextual, not additional full assessments.

E-01 through E-08 are defined in the [evidence index](../Evidence/INDEX.md); E-06/07/08 correspond to REM-01/02/03. Prior SEC-008 references are contextual and not copied into this project's release bundle. All row dispositions are limited to the described evidence.

| Topic | SP 800-53 Rev. 5 reference | SP 800-171 Rev. 2 / CMMC Level 2 | Evidence / disposition | Gap and follow-up |
| --- | --- | --- | --- | --- |
| Inventory and baseline | CM-8; CM-2 | 3.4.1 / CM.L2-3.4.1 | E-01 verifies three VM allocations/adapters; Partial | Host specs, software inventory, versions, update history and baseline approvals missing |
| Access enforcement | AC-3 | 3.1.2 / AC.L2-3.1.2 | Operator-confirmed RBAC on 8445; Partial | R-001; safe route/status/role correlation and managed-port tests required |
| Least privilege | AC-6 | 3.1.5 / AC.L2-3.1.5 | E-17 selected privileged groups; E-18/19 historical grant removal; E-20/21 final group-based noninherited ACL; E-22 counters; E-23/24 Effective Access; Partial | Historical Users RX removed from test file; current reader membership operator-confirmed; both identities disabled, no actual login/read attempts; full privilege/security-function authorization/lifecycle absent |
| Failed logons | AC-7 | 3.1.8 / AC.L2-3.1.8 | E-06 baseline 0; E-07/08 threshold 10, duration/window 30 minutes; Configuration remediated | R-007; controlled enforcement, recovery/DoS and audit tests pending; not a full MET determination |
| Remote access control | AC-17 | 3.1.12 / AC.L2-3.1.12 | E-02 permits SSH Anywhere on NAT interface; Partial | R-004; forwarding, approved sources and monitoring not fully assessed |
| Authenticator policy | IA-5(1) | 3.5.7 / IA.L2-3.5.7 | E-06 length 7; E-07/08 length 14 and complexity true; Configuration remediated | R-006; password-rejection, representative-user policy and compatibility tests pending; full requirement not established |
| Configuration settings | CM-6 | 3.4.2 / CM.L2-3.4.2 | E-02 and E-03 show current baseline settings; Partial | R-005 and broader hardening need approved baseline and sanitized config review |
| Risk assessment | RA-3 | 3.11.1 / RA.L2-3.11.1 | Eight documented proposed ratings; Draft assessment | Real threats, impacts, scope and stakeholder review absent |
| Control assessment | CA-2 | 3.12.1 / CA.L2-3.12.1 | Limited screenshot review; Partial | Not all requirements/objectives tested; periodic independent review undefined |
| Remediation planning | CA-5 | 3.12.2 / CA.L2-3.12.2 | Eight proposed POA&M rows; Draft plan | Approval, resources, owners and closure verification pending |
| System security plan | PL-2 | 3.12.4 / CA.L2-3.12.4 | Draft lab SSP; Draft plan | Complete requirement-level implementation descriptions and real approval missing |
| Boundary protection | SC-7 | 3.13.1 / SC.L2-3.13.1 | E-02 UFW active/default deny; E-03 firewall enabled; Partial | Multi-interface paths, IPv6, effective Windows policy and egress need testing |
| Transport protection | SC-8 | 3.13.8 / SC.L2-3.13.8 | HTTPS operator-confirmed with prior TLS context; Partial | Current TLS configuration and all sensitive flows not assessed |
| Key management | SC-12 | 3.13.10 / SC.L2-3.13.10 | CA key co-location operator-confirmed; Gap | R-002; key lifecycle/separation and rotation evidence missing |
| Cryptographic assurance | SC-13 | 3.13.11 / SC.L2-3.13.11 | Not assessed | Ordinary TLS and a private CA do not prove FIPS-validated cryptography |

Paraphrased topic labels are short summaries, not full requirement text. Identifiers checked against [SP 800-171 Rev. 2](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-171r2.pdf) and [SP 800-53 Rev. 5](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf). CMMC identifier structure follows the official Part 170 model.

## Important Interpretation Limits

- Seven-character minimum length is the historical assessed risk. REM-02/03 show it changed to 14. Revision 2 requirement 3.5.7 does not prescribe a universal numeric minimum; neither the earlier value alone nor the new value alone determines full compliance.
- Threshold 0 was the historical disabled policy. REM-02/03 show threshold 10 with 30-minute timers. A configuration query is not a failed-logon enforcement test. Lockout design still needs denial-of-service, recovery and account-specific review.
- NotConfigured is not proof of Allow, Block or firewall inactivity. Effective profiles, policy inheritance and positive/negative traffic tests are missing.
- R-003 is primarily a DNS availability/configuration issue. SC-22 (Architecture and Provisioning for Name/Address Resolution Service) is a contextual Rev. 5 reference, not proof of an SC-20 data-origin authenticity failure or a direct 800-171 requirement failure.
- R-005 is an operational database/baseline concern; no SQL injection, data loss or confirmed exploitation is inferred from database type.
- Backups and proposed BIA recovery targets relate conceptually to CP-9/CP-10, but no successful restoration was assessed. Do not invent a direct CMMC requirement equivalence.

No official MET/NOT MET determinations, aggregate score, percent compliant, conditional CMMC eligibility or regulated POA&M treatment is issued. This lab POA&M is a planning artifact, not a claim that any failed requirement may be deferred under CMMC rules.

## Assessor Evidence and Next Review

Final E-13 review confirms configuration persistence through one successful computer/user Group Policy refresh (`gpupdate /force` invocation operator-confirmed); E-12 confirms recorded 4688 for whoami.exe with generation operator-confirmed. See [final result details](../Reports/Windows-Audit-Policy-Remediation.md). These are completed narrow validation milestones, not reboot persistence, AD enforcement, full audit coverage or official compliance findings. Broader matrix dispositions and all eight risk statuses remain unchanged.

The later [R-008 audit review](../Reports/Windows-Audit-Policy-Remediation.md) adds Windows audit baseline/hardening and narrow process-event/policy-refresh evidence. The [matrix](Control-Assessment-Matrix.md) now includes Rev. 5 AU-2/AU-12 alongside audit/configuration associations. R-008 remains configuration remediated, validation pending; all eight risks remain unclosed. No official CMMC findings or complete operational logging coverage follow from these settings.

These local dispositions describe specific safeguards, not full requirement determinations. A configuration capture proves a setting, not all assessment objectives. Examine, interview and test methods require real scope/approval if used beyond this simulation.

| Safeguard / assessment area | Current disposition | Evidence an assessor would still need |
| --- | --- | --- |
| UFW default-deny and source/port restrictions | Implemented setting observed; boundary coverage partial | Approved rules/baseline, persistent configuration, applicable IPv4/IPv6/interface positive/negative tests and review records |
| HTTPS on the current application/IdP | Reported and supported by prior context; scope partial | Current chain/identity/protocol configuration, all sensitive-flow validation, safe trust lifecycle and applicable cryptographic assurance |
| Analyst/viewer OIDC RBAC | Test behavior operator-confirmed; deployment gap | Port/route/identity/status correlation, source review, token/session negative tests and managed-port promotion evidence |
| AD length 14 and threshold 10 | Configuration remediated; enforcement pending | Dedicated-account password rejection, attempt-limiting/recovery and representative-user applicability tests without credentials |
| CA signing-key separation | Gap remains open | Safe key-custody/permission/lifecycle evidence, separation design and trust validation without key contents |
| Keycloak database operations | Finding operator-confirmed; operational assurance gap | Sanitized database-mode configuration, supported architecture and verified persistence/restore |
| BIA and financial model | Documented hypothetical analysis | Business-owner approval and validated inputs; no screenshot required for arithmetic |
| Backup restoration and service recovery targets | Not demonstrated | Protected backup/restore runbooks, recovered-state timestamps and timed end-to-end tests against BIA objectives |
| Wider CMMC scope | Not assessed | Full applicable requirement/objective coverage, policies, interviews and tests across the defined boundary |

The BIA recovery plan is conceptually associated with SP 800-53 CP-2 (Contingency Plan), CP-9 (System Backup) and CP-10 (System Recovery and Reconstitution), checked against the [Rev. 5 catalog](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf). Proposed RTO/RPO are planning inputs, not proof these controls are implemented. No direct Level 2 requirement equivalence or additional CMMC compliance score is asserted. SP 800-171 Rev. 2 risk/assessment/SSP themes remain mapped separately above.
