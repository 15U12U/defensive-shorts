|  #  | Logon Type        | Authenticators                          |
| :-: | :---------------- | :-------------------------------------- |
|  2  | Interactive       | Password, SmartCard                     |
|  3  | Network           | Password, Kerberos ticket, NT Hash      |
|  4  | Batch             | Password (usually stored as LSA secret) |
|  5  | Service           | Password (usually stored as LSA secret) |
|  7  | Unlock            | Password                                |
|  8  | NetworkCleartext  | Password                                |
|  9  | NewCredentials    | Password                                |
| 10  | RemoteInteractive | Password                                |
---

### Logon Type 2 - Interactive
This is just logging on a local computer, typing user name and password. User logs on with a local or a domain account. This logon tvpe will appear only when a user really authenticated in the domain (by a domain controller). In case the DC is not available, but the user provided valid domain credentials cached in the local PC, Windows will log an event with logon type = 11 (Cached Interactive).
- A local logon grants a user permission to access Windows resources on the local computer.
- A local loaon requires that the user has a user account in The Security Accounts Manager (SAM) on the local computer.

### Logon Type 3 - Network
A computer was accessed from the Network. Mostly connecting to shared resources (like shared folders) and printers. A network logon grants a user permission to access Windows resources on the local computer in addition to any resources on networked computers, as defined by the credential's access token. Only after local authentication.  

Most logons to **Internet Information Services (IIS)** are Type 3, the exception is basic authentication which is explained in Logon Type 8.  

\[Because IIS is a service for hosting a website, hat can be put on a Windows machine, it's like accessing a machine from Network\]

### Logon Type 4 - Batch
This concerns Scheduled Tasks. When Windows executes a scheduled task, the Scheduled Task service first creates a new logon session for the task so that it can run under the authority of the User account specified, when the task was created.  

Logon type 4 events are usually benign, but a malicious user could try to guess the password of an account through scheduled tasks. Such attempts would generate a logon failure event where logon type is 4.  

But logon failures associated with scheduled tasks can also result trom an administrator entering the wrong password for the account at the time of task creation or from the password of an account being changed without modifying the scheduled task to use the new password.  

It is recommended to monitor schtasks.exe and at.exe (old) and their parent processes.


