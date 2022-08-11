# Nessus Credential Based Scanning (Windows)
## Domain/Local Administrator Account

| Checklist                                                             | Status             |
|:----------------------------------------------------------------------|:------------------:|
| Remote Registry Service                                               | :heavy_check_mark: |
| Windows Management Instrumentation (WMI) Service                      | :heavy_check_mark: |
| Administrative Shares<ul><li>IPC$</li><li>ADMIN$</li><li>C$</li></ul> | :heavy_check_mark: |
| Network Access<ul><li>139/TCP</li><li>445/TCP</li></ul>               | :heavy_check_mark: |

## Local Account with Admin Privileges

| Checklist                                                             | Status             |
|:----------------------------------------------------------------------|:------------------:|
| Remote Registry Service                                               | :heavy_check_mark: |
| Windows Management Instrumentation (WMI) Service                      | :heavy_check_mark: |
| Administrative Shares<ul><li>IPC$</li><li>ADMIN$</li><li>C$</li></ul> | :heavy_check_mark: |
| Network Access<ul><li>139/TCP</li><li>445/TCP</li></ul>               | :heavy_check_mark: |
| Windows User Account Control (UAC)                                    | :x:                |

### Disabling Windows User Account Control (UAC)

  - Method 1: Open the **Control Panel**, select **User Accounts** and then set **Turn User Account Control** to **Off**
  - Method 2: Change the registry DWORD named **EnableLUA** to "**0**" at the following location:
    ```
    HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\EnableLUA
    ```
  - Method 3: Add a new registry DWORD named **LocalAccountTokenFilterPolicy** and set the value to "**1**" at the following location:
    ```
    HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\LocalAccountTokenFilterPolicy
    ```

## Domain Account with Admin Privileges 


  - - Verify the following,
  ```
  Administrative Tools
    > Local Security Policy
      > Security Settings
        > Local Policies
          > Security Options
            > Network access: Sharing and security model for local accounts
              # Classic - local users authenticate as themselves
  ```

