# IT Delegation and Access Control Lab

## Overview

In this lab, I designed a simple IT delegation model in Active Directory.

The goal was not to give all IT users full Domain Admin permissions.
Instead, I separated IT accounts by role, created security groups, delegated only the required permissions, and verified the results with real tests.

The lab focuses on:

* Separating daily IT accounts from privileged IT accounts
* Creating IT role-based security groups
* Managing AD from an IT workstation using RSAT / ADUC
* Delegating domain join permissions
* Delegating Helpdesk permissions
* Delegating IT Admin / AD Operator permissions
* Applying workstation access using Group Policy
* Testing allowed and denied actions
* Validating changes using Event Viewer and `gpresult`

---

## Tools Used

| Tool                                 | Purpose                                                                                                     |
| ------------------------------------ | ----------------------------------------------------------------------------------------------------------- |
| Active Directory Users and Computers | Create OUs, users, groups, delegated permissions, and move AD objects                                       |
| Group Policy Management              | Create and link GPOs for local admin access, Remote Desktop, firewall rules, and workstation access control |
| RSAT / ADUC on IT Workstation        | Manage AD from an IT workstation without logging directly into the Domain Controller                        |
| Event Viewer                         | Validate domain join, user account changes, and AD object movement                                          |
| CMD / PowerShell                     | Run commands such as `runas`, `gpresult`, and event validation commands                                     |
| Remote Desktop                       | Test remote support access after applying GPO settings                                                      |
| VMware Workstation                   | Run the Windows Server lab environment                                                                      |

---

## Lab Idea

In many environments, IT users need different levels of access.

For example:

* Helpdesk may need to reset user passwords.
* Workstation support may need to join computers to the domain.
* IT Admin may need to create or disable normal users.
* Not everyone should have Domain Admin access.

So I built this lab to test a more controlled access model.

The main idea is:

```text
Give each IT role only the permissions it needs.
```

---

## IT Account Model

### What I did

For IT staff, I created two types of accounts:

| Account Type       | Example        | Usage                   |
| ------------------ | -------------- | ----------------------- |
| Daily account      | `jaffar.sheik` | Normal daily work       |
| Privileged account | `pa-it.jaffar` | IT administrative tasks |

I used the same idea for different IT roles:

| Role                | Example Account |
| ------------------- | --------------- |
| Helpdesk            | `pa-hd.almousa` |
| IT Admin            | `pa-it.jaffar`  |
| Workstation Support | `pa-ws.danish`  |

### Why I did it

The daily account is used for normal work such as email, browsing, Teams, and opening links or attachments.

This account is more exposed to risks like:

* Phishing emails
* Malicious links
* Unsafe attachments
* Browser-based attacks
* User mistakes

Because of that, I did not assign admin permissions to daily accounts.

If a daily account gets compromised, the attacker should not automatically get IT admin permissions.

### Result

Administrative permissions were assigned only to privileged IT accounts and security groups.

![IT OU Structure](./Screenshots/01-it-ou-structure.png)

---

## AD OU and Security Group Design

### What I did

I created a clear OU structure for users, computers, and IT access groups.

The IT accounts were separated into:

* Standard accounts
* Admin accounts

Computers were separated into:

* Regular computers
* Management computers

![Regular Computer OU Structure](./Screenshots/03-regular-ou-computer-objects.png)

I also created IT security groups to control access by role.

![IT Access Security Groups](./Screenshots/02-it-access-security-groups.png)

### Why I did it

Using groups is better than assigning permissions directly to users.

It makes access easier to manage because:

* Users can be added or removed from groups.
* Permissions stay organized.
* Each group has a clear purpose.
* It is easier to audit who has access.

### Main Groups

| Group                           | Purpose                                                               |
| ------------------------------- | --------------------------------------------------------------------- |
| `GG_Helpdesk_AD_Delegation`     | Helpdesk AD tasks such as password reset and computer object movement |
| `GG_IT_AD_Operators_Delegation` | IT Admin / AD Operator tasks for normal users                         |
| `GG_IT_Workstation_LocalAdmins` | Local admin access on regular workstations                            |
| `GG_IT_Workstation_RDP`         | Used to separate Remote Desktop access for workstation support        |

---

## RSAT / ADUC Management from IT Workstation

### What I did

I used RSAT / Active Directory Users and Computers from an IT workstation instead of logging directly into the Domain Controller.

The IT workstation used in this lab was:

```text
DYS-IT-HD01
```

I opened ADUC using a delegated Helpdesk account:

```cmd
runas /user:pa-hd.almousa@days.local "mmc dsa.msc"
```

![ADUC Run As Helpdesk User](./Screenshots/15-aduc-run-as-helpdesk-user-cmd.png)

### Why I did it

Normal Helpdesk or IT support tasks should not require logging into the Domain Controller.

Using RSAT from an IT workstation is cleaner and safer because:

* The Domain Controller is not used for daily admin work.
* Helpdesk can work with delegated permissions only.
* The admin task is separated from normal daily user access.

### Result

Helpdesk was able to open ADUC from the IT workstation using a delegated privileged account.

---

## Workstation Support Delegation for Domain Join

### What I did

I delegated limited permissions to allow the workstation support group to join new computers to the domain.

The permission was applied on the default `Computers` container.

The delegated group was:

```text
GG_IT_Workstation_LocalAdmins
```

The important permission was:

```text
Create Computer objects
```

![Computers Container Domain Join Permission](./Screenshots/20-computers-container-domain-join-permissions.png)

### Why I did it

In a real IT environment, support staff may need to join new computers to the domain.

But they should not use Domain Admin accounts for this task.

The goal was to allow domain join without giving full domain privileges.

### Result

The workstation support account successfully joined a new computer to the domain.

The account used for the test was:

```text
pa-ws.danish
```

The computer joined to the domain was:

```text
DYS-HR-03
```

![Domain Join Success](./Screenshots/18-domain-join-success-using-ws-account.png)

### Validation

The domain join action was validated in Event Viewer using Event ID `4741`.

```text
Event ID 4741 = A computer account was created
```

The event showed that `pa-ws.danish` created the computer account.

![Event 4741 Computer Account Created](./Screenshots/19-event-4741-computer-account-created.png)

---

## Helpdesk Computer Object Movement

### What I did

After the computer was joined to the domain, I delegated permissions for Helpdesk to move computer objects from the default `Computers` container to the `Regular` OU.

The delegated group was:

```text
GG_Helpdesk_AD_Delegation
```

![Helpdesk Computer Move Permission](./Screenshots/21-computers-container-helpdesk-move-permissions.png)

### Why I did it

When a new workstation is joined to the domain, it may appear first in the default `Computers` container.

Helpdesk should be able to organize normal workstations and move them to the correct OU.

But Helpdesk should not be able to manage Management computers.

### Result

Helpdesk successfully moved the computer object:

```text
DYS-HR-03
```

from:

```text
CN=Computers
```

to:

```text
OU=Regular
```

### Validation

The move action was verified using Event ID `5139`.

```text
Event ID 5139 = A directory service object was moved
```

![Event 5139 Computer Object Moved](./Screenshots/22-event-5139-computer-object-moved.png)

### Denied Test

I also tested moving the same computer object to the `Management` OU.

The action was denied.

![Helpdesk Denied Moving to Management](./Screenshots/23-helpdesk-denied-moving-to-management.png)

This confirms that Helpdesk can manage regular workstation objects but cannot manage Management computers.

---

## Workstation Access Using Group Policy

### What I did

I created a GPO for regular workstations.

The GPO was linked to the `Regular` computers OU.

The GPO configured:

* Local admin access for the IT workstation support group
* Remote Desktop access
* Firewall rules for Remote Desktop

![Workstation Access GPO Settings](./Screenshots/04-gpo-workstation-it-admin-rd-access.png)

### Why I did it

IT support may need local admin access on regular workstations to troubleshoot issues.

But this access should be controlled by GPO and applied only to the correct OU.

I linked the GPO to the `Regular` OU so the policy does not apply to Management computers or servers.

### Local Admin Result

The group `GG_IT_Workstation_LocalAdmins` was added to the local Administrators group on the workstation.

![Local Admin Group Added by GPO](./Screenshots/05-workstation-local-admin-group-added-by-gpo.png)

### GPO Validation

I verified that the GPO was applied using `gpresult`.

![GPO Applied Using gpresult](./Screenshots/07-gpresult-workstation-gpo-applied.png)

### Remote Desktop Test

After the policy was applied, I tested Remote Desktop access to the workstation.

![Remote Desktop Test Success](./Screenshots/08-rdp-to-workstation-success.png)

### Result

The workstation received the policy successfully.

The IT workstation support group had local admin access on the regular workstation, and Remote Desktop access worked after the GPO was applied.

---

## Helpdesk User Delegation

### What I did

I delegated password reset permissions to the Helpdesk group on the HR OU.

The delegated group was:

```text
GG_Helpdesk_AD_Delegation
```

The delegated task was:

```text
Reset user passwords and force password change at next logon
```

![Helpdesk Reset Password Delegation](./Screenshots/11-helpdesk-reset-password-delegation.png)

The permission was also verified from Advanced Security settings.

![Helpdesk Reset Password Permission](./Screenshots/12-hr-ou-helpdesk-delegation-entry.png)

### Why I did it

Helpdesk usually needs to reset passwords for normal users.

But Helpdesk should not have full control over all users or privileged IT accounts.

So I delegated only the required task.

### Result

The Helpdesk account successfully reset a password for a normal HR user.

![Helpdesk Reset Password Success](./Screenshots/16-helpdesk-reset-password-success.png)

### Denied Test

The same Helpdesk account was denied when trying to perform a privileged action on an IT account.

![Helpdesk Denied Privileged Action](./Screenshots/17-helpdesk-denied-privileged-action.png)

This confirms that Helpdesk has limited access only.

---

## IT Admin / AD Operator Delegation

### What I did

I created a higher IT role for AD Operator tasks.

The delegated group was:

```text
GG_IT_AD_Operators_Delegation
```

This role was allowed to perform normal user administration tasks such as:

* Create normal users
* Modify normal users
* Disable users
* Reset passwords

The permissions were delegated on normal user OUs such as HR.

![IT Operator Delegation Entry](./Screenshots/13-hr-ou-it-operator-delegation-entry.png)

### Why I did it

IT Admin / AD Operator needs more access than Helpdesk.

But that still does not mean the account should be Domain Admin.

The goal was to give this role enough access to manage normal users, but still block high-risk actions.

### Result

The IT Admin account was able to perform normal user management tasks.

### Validation

User account changes were validated from Event Viewer.

![IT Admin Create User Validation Event](./Screenshots/24-it-admin-create-user-validation-event.png)

A disabled user action was also validated.

![IT Admin Disable User Validation Event](./Screenshots/25-it-admin-disable-user-validation-event.png)

### Denied Test

The IT Admin account was denied when trying to delete a user.

![IT Admin Denied Delete User](./Screenshots/26-it-admin-denied-delete-user.png)

This confirms that the IT Admin role has more access than Helpdesk, but still does not have full control.

---

## Access Control Summary

| Role                   | Allowed                                                           | Denied                                              |
| ---------------------- | ----------------------------------------------------------------- | --------------------------------------------------- |
| Helpdesk               | Reset HR user passwords, move regular computer objects            | Privileged IT accounts, Management computers        |
| Workstation Support    | Join computers to the domain, local admin on regular workstations | Domain Admin access, Management / server access     |
| IT Admin / AD Operator | Create, modify, disable, and reset normal users                   | Delete users, privileged areas, full domain control |

---

## Main Security Points

This lab follows a least privilege approach.

The main security decisions were:

* Daily IT accounts do not have admin permissions.
* Privileged IT accounts are separated from daily accounts.
* IT permissions are assigned through groups.
* Helpdesk has limited delegated access.
* Workstation support can support regular PCs without Domain Admin.
* IT Admin has more permissions than Helpdesk, but still limited.
* Management computers and privileged accounts are protected.
* Allowed and denied tests were performed to confirm the access boundaries.

---

## Troubleshooting Notes

During the lab, I faced some issues and fixed them:

* RSAT installation failed at first because the workstation DNS was not resolving Microsoft update sources correctly.
* Remote Desktop did not work at first because it was disabled on the target workstation.
* Moving computer objects required specific permissions on the source and destination locations.
* Event Viewer validation required checking the correct security events.

---

## Future Improvements

Possible improvements for a more production-like setup:

* Add a dedicated Staging OU for newly joined computers.
* Redirect new computer objects to the Staging OU.
* Restrict RDP firewall scope to IT workstations only.
* Add Windows LAPS for local administrator password management.
* Add more detailed auditing for privileged AD actions.
* Automate some onboarding tasks with PowerShell.
