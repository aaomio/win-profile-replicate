# Profile Registry Configuration

## Overview

After creating and signing in to the new account, verify that Windows is using the correct profile path and Explorer folder locations.

## Profile Mapping

Open Registry Editor:

```cmd
regedit
```

Navigate to:

```text
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList
```

Locate the SID associated with the user account and verify:

```text
ProfileImagePath
```

Example:

```text
C:\Users\Neo
```

If the path references an old profile directory, update it accordingly.

---

## User Shell Folders

Navigate to:

```text
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders
```

Review the following entries:

* Desktop
* Personal (Documents)
* Downloads
* My Pictures
* My Music
* My Video

Ensure they point to the correct profile location.

Example:

```text
C:\Users\Neo\Desktop
```

Incorrect:

```text
C:\Users\User_\Desktop
```

Correct:

```text
C:\Users\Neo\Desktop
```

---

## Shell Folders

Navigate to:

```text
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders
```

Verify that folder paths match the values configured in:

```text
User Shell Folders
```

---

## Verification

Confirm the active profile:

```cmd
echo %USERPROFILE%
```

Expected:

```text
C:\Users\Neo
```

Review configured folder locations:

```cmd
reg query "HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders"
```

Check for any remaining references to previous profile paths.

---

## Common Symptoms

Incorrect profile mappings may result in:

* Missing Desktop files
* Empty Documents folder
* Downloads folder unavailable
* "Location is unavailable" messages
* Broken Quick Access links
* Explorer opening invalid paths

## Notes

* Sign in to the new account before making changes.
* Back up registry keys before editing them.
* Ensure all profile paths reference existing directories.
* Restart Explorer or sign out and back in after making changes.
