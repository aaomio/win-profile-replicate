# Rename a Windows Profile Folder

## Overview

This procedure can be used when the account name and profile folder name do not match.

Example:

```text
Account Name: Neo
Profile Folder: C:\Users\User_
```

Desired result:

```text
Account Name: Neo
Profile Folder: C:\Users\Neo
```

## Step 1 - Rename the User Account

### PowerShell

Open PowerShell as Administrator:

```powershell
Rename-LocalUser -Name "User_" -NewName "Neo"
```

Verify:

```powershell
Get-LocalUser
```

### Alternative: Local Users and Groups

1. Press **Windows + R**
2. Type:

```text
lusrmgr.msc
```

3. Press **Enter**
4. Select **Users**
5. Right-click the user account
6. Select **Rename**
7. Enter the new account name

## Step 2 - Create a Temporary Administrator

The profile folder cannot be renamed while logged into the account that owns it.

Open Command Prompt as Administrator:

```cmd
net user TempAdmin Password123 /add
net localgroup Administrators TempAdmin /add
```

Sign out and log in as **TempAdmin**.

## Step 3 - Rename the Profile Folder

Navigate to:

```text
C:\Users
```

Rename:

```text
User_
```

to:

```text
Neo
```

Alternatively:

```cmd
ren "C:\Users\User_" Neo
```

> Important: Rename the folder before modifying any registry paths.

## Step 4 - Update ProfileList

Open Registry Editor.

Press **Windows + R**, type:

```text
regedit
```

and press **Enter**.

Navigate to:

```text
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList
```

Locate the SID associated with the user.

Update:

```text
ProfileImagePath
```

from:

```text
C:\Users\User_
```

to:

```text
C:\Users\Neo
```

## Step 5 - Verify User Shell Folders

Log in as the renamed user.

Navigate to:

```text
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders
```

Check for any hardcoded references to:

```text
C:\Users\User_
```

Update them to:

```text
C:\Users\Neo
```

if necessary.

### Important

Leave entries that use:

```text
%USERPROFILE%
```

unchanged.

Example:

```text
%USERPROFILE%\Desktop
%USERPROFILE%\Documents
%USERPROFILE%\Downloads
```

Windows automatically resolves these paths based on the active profile.

## Step 6 - Verify

Open Command Prompt:

```cmd
echo %USERPROFILE%
```

Expected:

```text
C:\Users\Neo
```

Verify the account:

```cmd
whoami
```

Expected:

```text
COMPUTERNAME\neo
```

## Step 7 - Remove Temporary Administrator

After confirming everything works:

```cmd
net user TempAdmin /delete
```

