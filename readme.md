# Windows Profile Migration

Guides for migrating, repairing, and renaming Windows user profiles.

## Overview

This repository covers common profile migration scenarios, including creating a new profile, renaming profile folders, and correcting Windows Explorer folder mappings.

## Guides

* [Create a New User Account](create-user-account.md)
* [Profile Registry Configuration](profile-registry-configuration.md)
* [Rename a Windows Profile Folder](rename-profile-folder.md)

## Common Registry Locations

### Profile Mapping

```text
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList
```

### User Shell Folders

```text
HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders
```

### Shell Folders

```text
HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders
```
