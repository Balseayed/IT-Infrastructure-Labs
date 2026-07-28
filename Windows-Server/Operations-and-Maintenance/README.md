# Controlled Restart and Service Validation on FS01

## Lab Information

| Field | Value |
| --- | --- |
| Practical scenario | Controlled restart of FS01 followed by post-maintenance service validation |
| Lab owner | Basel Alseayed |
| Environment | Personal VMware Lab |
| Change status | Planned / In Progress |
| Results | Pending |

This lab must remain **In Progress** until the controlled restart is performed and real verification evidence is added.

No screenshots, commands, dates, snapshot availability, or successful outcomes are assumed.

---

## Purpose

The purpose of this lab is to practice a controlled Windows Server maintenance workflow by:

- Recording the state of `FS01` before maintenance.
- Performing a controlled restart of `FS01`.
- Confirming that the server returns normally.
- Validating the existing File Server services after the restart.
- Recording real evidence, issues, and any rollback decision.

This lab validates the existing environment. It does not recreate or reconfigure the File Server implementation.

Use:

- [Maintenance Checklist](./Maintenance-Checklist.md) for actionable checks.
- [Change Record](./Change-Record.md) for actual maintenance activity and results.

---

## Existing Environment

The existing [Advanced File Server Features](../File-Server/Advanced-File-Server-Features/) lab documents `FS01` as a dedicated File Server in the `Days.local` domain.

The documented implementation includes:

- The `\\FS01\Company` share
- Security-group-based NTFS permissions
- Group Policy drive mapping
- Access-Based Enumeration
- FSRM quotas
- File screening
- Shadow Copies
- File auditing

These services will be validated after the controlled restart. They will not be configured again in this lab.

---

## Maintenance Scope

### Approved maintenance action

**Controlled restart of FS01.**

### Included

- Pre-maintenance system and service checks
- Recording the current backup status
- Recording whether a VMware snapshot is created
- Controlled restart of FS01
- Server and service validation after restart
- Client access and security-boundary tests
- Evidence collection
- Issue and rollback recording

### Excluded

- Recreating the company share
- Reconfiguring NTFS permissions
- Reconfiguring Access-Based Enumeration
- Recreating FSRM quotas or file-screening rules
- Reconfiguring Shadow Copies
- Reconfiguring file auditing
- Modifying unrelated domain services

---

## Risk Assessment

| Risk | Possible effect | Control |
| --- | --- | --- |
| FS01 does not return normally | The company share remains unavailable | Stop further actions and begin rollback checks |
| Network configuration is unavailable or changed | Domain and client connectivity may fail | Record IP and DNS configuration before maintenance and verify it afterward |
| Critical services remain stopped | File Server features may be unavailable | Record service state before restart and validate it afterward |
| Permission behavior changes | Authorized access may fail or unauthorized access may become possible | Repeat authorized and unauthorized NTFS access tests |
| Existing File Server features fail validation | ABE, FSRM, Shadow Copies, or auditing may not operate as documented | Record the failure and stop unrelated changes |
| Recovery evidence is unavailable | Rollback options may be limited | Review backup status and record whether a VMware snapshot is created |

All risk controls and observed results remain **Pending** until the maintenance activity is performed.

---

## Pre-Maintenance Checks

Complete the pre-maintenance section in the [Maintenance Checklist](./Maintenance-Checklist.md).

The checks cover:

- Hostname, OS, and uptime
- IP and DNS configuration
- Disk free space and critical services
- Event Viewer and current backup status
- Client access to `\\FS01\Company`

Do not proceed if a pre-maintenance issue makes the controlled restart unsafe or prevents a reliable post-maintenance comparison.

---

## Maintenance Procedure

1. Complete and record all pre-maintenance checks.
2. Review and record the current backup status.
3. Decide whether to create a VMware snapshot before maintenance.
4. If a snapshot is created, record its real details in the Change Record.
5. Do not claim that a snapshot exists if one is not created.
6. Record the beginning of the maintenance activity.
7. Perform the approved controlled restart of `FS01`.
8. Capture the actual controlled restart evidence.
9. Wait for the VM and operating system to return normally.
10. If FS01 does not return normally, stop further actions and follow the rollback plan.
11. Complete all post-maintenance validation checks.
12. Record actual observations, evidence, issues, and the final outcome.

The actual restart method and observed behavior must be recorded only when the maintenance activity is performed.

---

## Post-Maintenance Validation

After FS01 returns, validate:

- Server availability
- IP and DNS configuration
- Critical service status
- Event Viewer
- Access to `\\FS01\Company`
- Authorized and unauthorized NTFS access
- Access-Based Enumeration
- Existing FSRM quota
- Existing file-screening behavior
- Shadow Copies
- File auditing
- Client access after maintenance

The validation must test the existing configuration without rebuilding it.

Failed or incomplete checks must remain marked **Not Verified** and be recorded in the Change Record.

---

## Rollback Criteria and Procedure

Begin rollback checks if `FS01` does not return normally or required services remain unavailable.

Rollback procedure:

1. Stop further actions if FS01 does not return normally.
2. Verify the VMware VM state.
3. Verify the VMware network adapter state.
4. Start required services if they remain stopped.
5. Recheck server availability, network configuration, and shared-folder access.
6. Restore the latest known-good VMware snapshot only if:
   - A snapshot was actually created before maintenance.
   - The snapshot details were recorded.
   - Rollback becomes necessary.
7. Do not claim that a snapshot exists until it is actually created.
8. Record every rollback action and observed result.

If no snapshot was created, the Change Record must state that snapshot rollback is unavailable rather than assuming otherwise.

---

## Required Screenshot Evidence

Do not add Markdown image links until the corresponding screenshot files exist.

| Evidence ID | Required capture | Status |
| --- | --- | --- |
| PRE-01 | Hostname, OS, and uptime | Pending |
| PRE-02 | IP and DNS configuration | Pending |
| PRE-03 | Disk space and critical services | Pending |
| PRE-04 | Event Viewer and backup status | Pending |
| PRE-05 | Client access to `\\FS01\Company` | Pending |
| MAINT-01 | Controlled restart evidence | Pending |
| POST-01 | Server availability, IP, and DNS | Pending |
| POST-02 | Critical services and Event Viewer | Pending |
| POST-03 | Shared-folder and NTFS access tests | Pending |
| POST-04 | ABE, FSRM quota, and file-screening validation | Pending |
| POST-05 | Shadow Copies and file-auditing validation | Pending |
| POST-06 | Client access after maintenance | Pending |

Store real evidence in `Screenshots/` and record each filename in the Maintenance Checklist or Change Record.

---

## Final Verification Summary

| Validation area | Status | Evidence |
| --- | --- | --- |
| Pre-maintenance baseline | Pending | Not added |
| Controlled restart | Pending | Not added |
| Server availability | Not Verified | Not added |
| IP and DNS configuration | Not Verified | Not added |
| Critical services and Event Viewer | Not Verified | Not added |
| Shared-folder and NTFS access | Not Verified | Not added |
| ABE, FSRM quota, and file screening | Not Verified | Not added |
| Shadow Copies and file auditing | Not Verified | Not added |
| Client access after maintenance | Not Verified | Not added |
| Rollback decision | Pending | Not recorded |

**Final result: Pending**

**Lab status: Planned / In Progress**

The lab must not be marked complete or Ready until real evidence supports every required validation.

---

## Production Considerations

In a production environment, a controlled server restart should also consider:

- A defined maintenance window
- Service ownership and user communication
- Current and tested recovery options
- Server and application dependencies
- Active user sessions
- Monitoring and alert review
- Redundancy and availability requirements
- Documented rollback criteria
- Evidence retention
- Review of unresolved post-maintenance issues
