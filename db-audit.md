# Database Auditing Configuration Guide
## Oracle Database - 9i, 10g, 11g
### Check the status of auditing
```sql
SQL> SHOW PARAMETER AUDIT
```
#### AUDIT_TRAIL
| Parameter     | Auditing Status    | Description                                                                                 |
| :------------ | :----------------: | :------------------------------------------------------------------------------------------ |
| NONE          | :x:                | Auditing is disabled.                                                                       |
| DB            | :heavy_check_mark: | Write the standard audit content to SYS.AUD$ table                                          |
| DB, EXTENDED  | :heavy_check_mark: | Similar to DB, but the SQL_BIND and SQL_TEXT columns are also populated for SYS.AUD$ table. |
| XML           | :heavy_check_mark: | Write the standard audit content and FGA audit content to an XML formatted file.            |
| XML, EXTENDED | :heavy_check_mark: | Similar to XML, but the SQL_BIND and SQL_TEXT columns are also populated in XML file.       |
| OS            | :heavy_check_mark: | Write the standard audit content to text files.                                             |

#### AUDIT_SYS_OPERATIONS
| Parameter    | Auditing Status    | Description                                                                                 |
| :----------- | :----------------: | :------------------------------------------------------------------------------------------ |
| FALSE        | :x:                | Auditing is disabled.                                                                       |
| TRUE         | :heavy_check_mark: | Enables auditing of directly issued user SQL statements with **SYS** authorization. These include SQL statements directly issued by users when connected with the **SYSASM**, **SYSBACKUP**, **SYSDBA**, **SYSDG**, **SYSKM**, or **SYSOPER** privileges, as well as SQL statements that have been executed with **SYS** authorization using the _**PL/SQL**_ package _DBMS_SYS_SQL_. |

#### AUDIT_SYSLOG_LEVEL
> **Note**  
> 
> _AUDIT_SYSLOG_LEVEL allows SYS and standard OS audit records to be written to the system audit log using the SYSLOG utility._

| Parameter | Description                                                                                                          |
| :-------- | :------------------------------------------------------------------------------------------------------------------- |
| facility  | USER / LOCAL[0 \| 1 \| 2 \| 3 \| 4 \| 5 \| 6 \| 7] / SYSLOG / DAEMON / KERN / MAIL / AUTH / LPR / NEWS / UUCP / CRON |
| priority  | NOTICE / INFO / DEBUG / WARNING / ERR / CRIT / ALERT / EMERG                                                         |

#### AUDIT_FILE_DEST
> **Note**  
> 
> _AUDIT_FILE_DEST specifies the operating system directory into which the audit trail is written when the AUDIT_TRAIL initialization parameter is set to **OS**, **XML**, or **XML, EXTENDED**._



### Enable/Disable auditing
#### - Enable -
```sql
SQL> ALTER SYSTEM SET AUDIT_TRAIL=TRUE SCOPE=SPFILE;
```
OR one of the below commands
```sql
SQL> ALTER SYSTEM SET AUDIT_TRAIL=DB SCOPE=SPFILE;
SQL> ALTER SYSTEM SET AUDIT_TRAIL=DB, EXTENDED SCOPE=SPFILE;
SQL> ALTER SYSTEM SET AUDIT_TRAIL=XML SCOPE=SPFILE;
SQL> ALTER SYSTEM SET AUDIT_TRAIL=XML, EXTENDED SCOPE=SPFILE;
SQL> ALTER SYSTEM SET AUDIT_TRAIL=OS SCOPE=SPFILE;
```
#### - Disable -
```sql
SQL> ALTER SYSTEM SET AUDIT_TRAIL=NONE SCOPE=SPFILE;
```

### Enable/Disable SYS operations auditing
#### - Enable -
```sql
SQL> ALTER SYSTEM SET AUDIT_SYS_OPERATIONS=TRUE SCOPE=SPFILE;
```
#### - Disable -
```sql
SQL> ALTER SYSTEM SET AUDIT_SYS_OPERATIONS=FALSE SCOPE=SPFILE;
```

### Examples of configuring audit syslog levels
```sql
SQL> ALTER SYSTEM SET AUDIT_SYSLOG_LEVEL='KERN.EMERG' SCOPE=SPFILE;
SQL> ALTER SYSTEM SET AUDIT_SYSLOG_LEVEL='LOCAL1.WARNING' SCOPE=SPFILE;
```





## Oracle Database - 12c, 19c, 21c
