# WMI Configuration Requirements for Event Log Collection

## Port Requirement

- Windows Server 2008 and later / Windows Vista and later


| Port        | Protocol | Name                                |
| ----------- |:--------:| ----------------------------------- |
| 135         | TCP      | RPC                                 |
| 445         | TCP      | SMB                                 |
| 49152-65535 | TCP      | High Port Range (Unrestricted DCOM) |
| 1025-1030   | TCP      | Low Port Range (Restricted DCOM)    |

- Windows NT4 / Windows 2000 / Windows Server 2003 / Windows XP

| Port      | Protocol | Name                    |
| --------- |:--------:| ----------------------- |
| 135       | TCP      | RPC                     |
| 139       | TCP      | NetBIOS Session Service |
| 1025-5000 | TCP      | RPC Dynamic Port Range  |


## User Privileges

| Member Groups             |
| ------------------------- |
| Distributed COM Users     |
| Performance Monitor Users |
| Event Log Reader          |

## Troublshooting

- WBEMTest - Windows
