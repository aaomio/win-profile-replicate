# Create a New User Account

## Overview

Create a new local Windows user account and generate a new profile.

This procedure is commonly used when:

* Migrating to a new profile
* Recovering from profile corruption
* Correcting profile path issues
* Creating a replacement user profile

## Create the User

Open Command Prompt as Administrator.

```cmd
net user Neo Password123 /add
```

## Add Local Administrator Rights (Optional)

```cmd
net localgroup Administrators Neo /add
```

## Verify the Account

```cmd
net user Neo
```

## Generate the Profile

1. Sign out of the current account.
2. Sign in as the new user.
3. Allow Windows to complete profile creation.

## Verify Profile Creation

Open Command Prompt and run:

```cmd
echo %USERPROFILE%
```

Expected output:

```text
C:\Users\Neo
```

