# Windows Server Readiness Evidence Matrix

## Overview

This matrix summarizes the Windows Server capabilities already implemented and verified in this repository.

It provides a central index to the existing lab documentation and identifies completed work that should not be repeated. Each safe next upgrade extends the current environment without replacing or rewriting the documented labs.

---

## Status Definition

| Status | Meaning |
| --- | --- |
| Ready | The implementation and its verification evidence are documented in the linked lab. |

---

## Readiness Matrix

| Area | Already Implemented | Verification Evidence | Status | Do Not Repeat | Safe Next Upgrade |
| --- | --- | --- | --- | --- | --- |
| Active Directory | DC01 promotion; `Days.local` domain; department OUs; users and security groups; PowerShell bulk user creation; Windows client domain join | [Active Directory documentation and screenshots](../Active-Directory/) show installed roles, OU and group structure, created users, group membership, the client computer object, and successful domain membership. | Ready | Basic OUs, users, groups, bulk user creation, client domain join | AD health checks and troubleshooting scenarios |
| DNS | Forward and reverse lookup zones; A, PTR, CNAME, multiple A, and AD SRV records; internal DNS client configuration | [DNS documentation and screenshots](../DNS/) show forward and reverse records, PTR and CNAME records, multiple A records, SRV records, client DNS settings, and successful `ping` and `nslookup` tests. | Ready | Forward/reverse zones, A/PTR/CNAME/SRV records, basic `nslookup` | DNS troubleshooting, conditional forwarders, and scavenging |
| DC02 Replication | DC02 configured as an Additional Domain Controller and DNS server; DC01 and DC02 present in the Domain Controllers OU; AD object replication | [DC02 replication evidence](../DC02-Replication-and-DNS-Redundancy/#replication-verification) documents `repadmin /replsummary` with zero failures, `nltest` discovery of DC02, and a test user replicated from DC01 to DC02. | Ready | Additional Domain Controller promotion, Domain Controllers OU validation, basic `repadmin`, `nltest`, and AD object replication tests | `dcdiag` health checks, Active Directory Sites and Services, and controlled Domain Controller failure scenarios |
| DNS Redundancy | DC01 and DC02 configured as DNS servers; DHCP Option 006 supplies both DNS addresses; client receives both DNS servers | [DNS redundancy evidence](../DC02-Replication-and-DNS-Redundancy/#part-2-dns-redundancy) documents both DNS addresses on the client, resolution of the domain and both Domain Controllers, an isolated DC01 DNS-service interruption, and successful direct resolution through DC02. | Ready | Dual DNS configuration, DHCP Option 006 DNS entries, client DNS verification, direct DC02 lookup, and the isolated DNS-service test | Client resolver failover troubleshooting, DNS service monitoring, and documented DNS recovery procedures |
| DHCP | DHCP scope and address pool; router, DNS, and domain options; active leases; reservation; client release and renewal | [DHCP documentation and screenshots](../DHCP/) show the scope, address pool, options, leases, successful release/renew, and reservation verification. | Ready | Scope, options, leases, reservation, release/renew | DHCP failover, multiple scopes, and troubleshooting |
| Group Policy | OU-linked GPOs; USB storage restriction; clock removal; mapped drive; local administrator deployment test; client policy refresh and reporting | [Group Policy documentation and screenshots](../GPO/) show linked policies, successful restriction and mapping results, local Administrators group validation, and applied GPOs through `gpupdate` and `gpresult`. | Ready | GPO linking, USB restriction, mapped drive, local admin test, `gpresult` | Windows LAPS, security filtering, and WMI filtering |
| File Server | Department shares; security-group-based share and NTFS permissions; successful and denied access tests; mapped drives; dedicated FS01; ABE; FSRM quotas; file screening; shadow copies; file auditing | [Basic File Server evidence](../File-Server/Basic-Department-Share-and-NTFS/) verifies shares, permissions, access boundaries, and drive mapping. [Advanced File Server evidence](../File-Server/Advanced-File-Server-Features/) verifies FS01, ABE, FSRM, screening, previous-version recovery, and Event ID 4663 auditing. | Ready | Shares, NTFS, mapped drives, ABE, FSRM, file screening, shadow copies, and file auditing | No immediate standalone upgrade; use troubleshooting and backup integration |
| Backup and Recovery | Windows Server Backup; one-time volume backup; file recovery; ACL restoration; recovered-file verification | [Backup and Recovery documentation and screenshots](../Backup-Recovery/) show successful backup and recovery, restored files and permissions, and Event Viewer confirmation. | Ready | Backup Once, file restore, ACL restore, and Event Viewer validation | Scheduled backup, retention, off-server destination, and restore runbook |
| IT Delegation and Access Control | Separate daily and privileged accounts; role-based groups; RSAT administration; Helpdesk and IT Operator delegation; domain join delegation; workstation local administrator and RDP policies; allowed and denied tests | [IT Delegation and Access Control evidence](../IT-Delegation-and-Access-Control/) documents delegated permissions, RSAT administration, domain join, GPO application, RDP access, allowed and denied operations, and Event Viewer validation. | Ready | RSAT administration, Helpdesk delegation, domain join delegation, basic RDP and local admin GPO | Windows LAPS, restricted RDP firewall scope, privileged action auditing, and PowerShell onboarding |

---

## Readiness Rule

An area is marked **Ready** because its current implementation and verification results are documented in the linked lab.

Future work should follow the **Safe Next Upgrade** column and should not recreate items listed under **Do Not Repeat** unless troubleshooting requires a controlled retest.
