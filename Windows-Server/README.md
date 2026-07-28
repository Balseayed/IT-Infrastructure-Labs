# Windows Server Infrastructure Lab

This project documents my hands-on Windows Server infrastructure lab using VMware.

The lab covers core Windows Server administration tasks such as Active Directory, Domain Controller replication, DNS redundancy, DHCP, Group Policy, File Server permissions, Backup and Recovery, and role-based IT access control.

---

## Lab Sections

| Lab                              | Description                                                                                                                                |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ | 
| [Active Directory](./Active-Directory/)                 | Domain Controller setup, OU structure, users, groups, and client domain join                                        |
| [DNS](./DNS/)                              | Forward lookup zones, reverse lookup zones, A records, PTR records, CNAME records, and DNS validation                            |
| [DC02 Replication and DNS Redundancy](./DC02-Replication-and-DNS-Redundancy/) | Additional Domain Controller deployment, Active Directory replication, redundant DNS configuration, and validation |
| [DHCP](./DHCP/)                             | DHCP scope configuration, address pool, scope options, leases, reservation, and client IP renewal testing                       |
| [Group Policy](./GPO/)                      | GPO configuration, workstation policies, restrictions, and client-side validation                                               |
| [File Server](./File-Server/)                      | Shared folders, NTFS permissions, security groups, and mapped drives                                                     |
| [Backup and Recovery](./Backup-Recovery/)               | Windows Server Backup, restore testing, and recovery validation                                                     |
| [IT Delegation and Access Control](./IT-Delegation-and-Access-Control/) | Role-based IT access model using privileged accounts, AD delegation, GPO, RSAT, and audit validation|
| [Operations and Maintenance](./Operations-and-Maintenance/) | Controlled restart of FS01 followed by post-maintenance service validation |
| [Readiness Evidence](./Readiness-Evidence/Evidence-Matrix.md) | Implementation status, verification evidence, completed scope, and safe next upgrades |

---

## What This Project Covers

* Domain Controller setup
* Active Directory users, OUs, and groups
* PowerShell bulk user creation
* DNS records and name resolution testing
* Additional Domain Controller deployment
* Active Directory replication validation
* DNS redundancy testing
* DHCP scope, leases, reservations, and client renewal
* Group Policy management
* File Server shared folders
* NTFS permissions
* Mapped network drives
* Backup and Recovery testing
* IT account separation
* Helpdesk delegation
* Workstation support delegation
* IT Admin / AD Operator delegation
* Client-side verification
* Event Viewer validation
* Readiness evidence tracking

---

## Main Skills Practiced

* Windows Server Administration
* Active Directory
* DNS Administration
* Domain Controller Replication
* DNS Redundancy
* DHCP Administration
* Group Policy
* File Server Administration
* NTFS Permissions
* Windows Server Backup
* RSAT / ADUC Remote Administration
* Role-Based Access Control
* Least Privilege Design
* Troubleshooting and Documentation
