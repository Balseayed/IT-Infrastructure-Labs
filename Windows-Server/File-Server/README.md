# File Server Labs

## Overview

This section focuses on Windows Server File Server administration.

The labs start with a basic department-based file share, then continue with advanced File Server features such as Access-Based Enumeration, FSRM, Shadow Copies, and File Auditing.

The goal is to build a file sharing environment that uses security groups, NTFS permissions, Group Policy, and File Server management features.

---

## Labs

### 1. Department File Share and NTFS Permissions

This lab covers the basic File Server setup.

It includes:

* Creating a shared company folder.
* Creating department folders.
* Using security groups for access control.
* Configuring NTFS permissions.
* Testing user access between departments.
* Mapping the shared folder using Group Policy.

[Open Lab](./Basic-Department-Share-and-NTFS)

---

### 2. Advanced File Server Features

This lab builds on the basic File Server setup.

The File Server role was moved to a dedicated server named `FS01`, and advanced File Server features were configured and tested.

It includes:

* FS01 dedicated File Server role separation.
* Access-Based Enumeration.
* FSRM Auto Apply Quota.
* File Screening.
* Shadow Copies / Previous Versions.
* File Auditing using Event Viewer.

[Open Lab](./Advanced-File-Server-Features)

---

## Final Structure

```text
File-Server/
├── Basic-Department-Share-and-NTFS/
└── Advanced-File-Server-Features/
```

---

## Technical Focus

This File Server section focuses on:

* Share permissions.
* NTFS permissions.
* Security groups.
* Group Policy drive mapping.
* Folder visibility control.
* Storage quota management.
* File type restrictions.
* File recovery using Previous Versions.
* File activity auditing.

These labs show both the basic and advanced sides of managing File Server services in a Windows Server domain environment.
