# FS01 Controlled Restart Maintenance Checklist

| Field | Value |
| --- | --- |
| Lab owner | Basel Alseayed |
| Environment | Personal VMware Lab |
| Approved maintenance action | Controlled restart of FS01 |
| Change status | Planned / In Progress |

## Pre-Maintenance Checks

| Complete | Evidence ID | Actionable check | Actual observation | Evidence filename | Result |
| --- | --- | --- | --- | --- | --- |
| [ ] | PRE-01 | Record FS01 hostname, OS information, and uptime | Pending | Pending | Pending |
| [ ] | PRE-02 | Record IP and DNS configuration | Pending | Pending | Pending |
| [ ] | PRE-03 | Record disk free space and critical service status | Pending | Pending | Pending |
| [ ] | PRE-04 | Review Event Viewer and record current backup status | Pending | Pending | Pending |
| [ ] | PRE-05 | Test client access to `\\FS01\Company` | Pending | Pending | Pending |

## Maintenance Execution

| Complete | Evidence ID | Actionable step | Actual observation | Evidence filename | Result |
| --- | --- | --- | --- | --- | --- |
| [ ] | — | Confirm all required pre-maintenance checks are complete | Pending | Pending | Pending |
| [ ] | — | Record whether a VMware snapshot was created | Pending | Pending | Pending |
| [ ] | MAINT-01 | Perform and capture the controlled restart of FS01 | Pending | Pending | Pending |
| [ ] | — | Confirm whether FS01 returned normally | Pending | Pending | Pending |
| [ ] | — | Stop further actions and begin rollback checks if FS01 did not return normally | Pending | Pending | Pending |

## Post-Maintenance Checks

| Complete | Evidence ID | Actionable check | Actual observation | Evidence filename | Result |
| --- | --- | --- | --- | --- | --- |
| [ ] | POST-01 | Verify server availability, IP configuration, and DNS configuration | Pending | Pending | Not Verified |
| [ ] | POST-02 | Verify critical services and review Event Viewer | Pending | Pending | Not Verified |
| [ ] | POST-03 | Test shared-folder access and authorized and unauthorized NTFS access | Pending | Pending | Not Verified |
| [ ] | POST-04 | Validate Access-Based Enumeration, the existing FSRM quota, and file screening | Pending | Pending | Not Verified |
| [ ] | POST-05 | Validate Shadow Copies and file auditing | Pending | Pending | Not Verified |
| [ ] | POST-06 | Verify client access after maintenance | Pending | Pending | Not Verified |
