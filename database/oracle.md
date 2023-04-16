# Oracle Database Audit Configuration Guide
## Auditing Milestones
| Year | Version      | Milestone                         |
| :--- | :----------- | :-------------------------------- |
| 1992 | Oracle 7     | Introduced Traditional auditing.  |
| 2002 | Oracle 9iR2  | Introduced Fine-grained auditing. |
| 2013 | Oracle 12cR1 | Introduced Unified auditing.      |
| 2021 | Oracle 21c   | Traditional auditing deprecated.  |

## Traditional Auditing - 12.1 or lower (ex: 9i, 10g, 11g)
### Check the status of auditing
```sql
SQL> SHOW PARAMETER AUDIT
```
#### AUDIT_TRAIL
| Parameter     | Auditing Status    | Description                                                                                 |
| :------------ | :----------------: | :------------------------------------------------------------------------------------------ |
| NONE          | :x:                | Auditing is disabled.                                                                       |
| DB            | :heavy_check_mark: | Write the standard audit content to SYS.AUD$ table.                                         |
| DB, EXTENDED  | :heavy_check_mark: | Similar to DB, but the SQL_BIND and SQL_TEXT columns are also populated for SYS.AUD$ table. |
| XML           | :heavy_check_mark: | Write the standard audit content and FGA audit content to an XML formatted file.            |
| XML, EXTENDED | :heavy_check_mark: | Similar to XML, but the SQL_BIND and SQL_TEXT columns are also populated in XML file.       |
| OS            | :heavy_check_mark: | Write the standard audit content to text files.                                             |

#### AUDIT_SYS_OPERATIONS
| Parameter    | Auditing Status    | Description                                                                                 |
| :----------- | :----------------: | :------------------------------------------------------------------------------------------ |
| FALSE        | :x:                | Auditing is disabled.                                                                       |
| TRUE         | :heavy_check_mark: | Enables auditing of SQL statements directly issued by users with **SYS** authorization such as **SYSASM**, **SYSBACKUP**, **SYSDBA**, **SYSDG**, **SYSKM**, or **SYSOPER** privileges, as well as SQL statements that have been executed with **SYS** authorization using the _**PL/SQL**_ package _DBMS_SYS_SQL_. |

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

| Default Values                          | 
| :-------------------------------------- |
| _ORACLE_BASE_/admin/_ORACLE_SID_/adump  |
| _ORACLE_HOME_/rdbms/audit               |

#### Examples
```sql
# 'AUDIT_TRAIL' Configuration
SQL> ALTER SYSTEM SET AUDIT_TRAIL=DB SCOPE=SPFILE;
SQL> ALTER SYSTEM SET AUDIT_TRAIL=DB, EXTENDED SCOPE=SPFILE;
SQL> ALTER SYSTEM SET AUDIT_TRAIL=XML SCOPE=SPFILE;
SQL> ALTER SYSTEM SET AUDIT_TRAIL=XML, EXTENDED SCOPE=SPFILE;
SQL> ALTER SYSTEM SET AUDIT_TRAIL=OS SCOPE=SPFILE;
SQL> ALTER SYSTEM SET AUDIT_TRAIL=NONE SCOPE=SPFILE;

# 'AUDIT_SYS_OPERATIONS' Configuration
SQL> ALTER SYSTEM SET AUDIT_SYS_OPERATIONS=TRUE SCOPE=SPFILE;
SQL> ALTER SYSTEM SET AUDIT_SYS_OPERATIONS=FALSE SCOPE=SPFILE;

# 'AUDIT_SYSLOG_LEVEL' Configuration
SQL> ALTER SYSTEM SET AUDIT_SYSLOG_LEVEL='KERN.EMERG' SCOPE=SPFILE;
SQL> ALTER SYSTEM SET AUDIT_SYSLOG_LEVEL='LOCAL1.WARNING' SCOPE=SPFILE;

# 'AUDIT_FILE_DEST' Configuration
SQL> ALTER SYSTEM SET AUDIT_FILE_DEST='/opt/app/oracle/admin/db11/adump' SCOPE=SPFILE;
SQL> ALTER SYSTEM SET AUDIT_FILE_DEST='/var/log/oracle/audit' SCOPE=SPFILE;
```

### Levels of Auditing

| Level     | Description | Example |
| :-------- | :---------- | :--------- |
| Statement | Audit specific SQL statements, such as ```SELECT```, ```INSERT```, ```UPDATE```, and ```DELETE```. | ```AUDIT SELECT;```              |
| Object    | Audit actions on specific schema objects, such as tables, views, and procedures.                   | ```AUDIT SELECT ON employees;``` |
| Privilege | Audit the use of system privileges and object privileges.                                          | ```AUDIT DROP ANY TABLE;```      |

#### Security-relevant SQL Statements and Privileges audited by Default
| Level         | Audit                                                                                             |
| :------------ | :------------------------------------------------------------------------------------------------ |
| Privilege     | ALTER ANY PROCEDURE <br/> ALTER ANY TABLE <br/> ALTER DATABASE <br/> ALTER PROFILE <br/> ALTER SYSTEM <br/> ALTER USER <br/> AUDIT SYSTEM <br/> CREATE ANY JOB <br/> CREATE ANY LIBRARY <br/> CREATE ANY PROCEDURE <br/> CREATE ANY TABLE <br/> CREATE EXTERNAL JOB <br/> CREATE PUBLIC DATABASE LINK <br/> CREATE SESSION <br/> CREATE USER <br/> DROP ANY PROCEDURE <br/> DROP ANY TABLE <br/> DROP PROFILE <br/> DROP USER <br/> EXEMPT ACCESS POLICY <br/> GRANT ANY OBJECT PRIVILEGE <br/> GRANT ANY PRIVILEGE <br/> GRANT ANY ROLE |
| Statement     | ROLE <br/> SYSTEM AUDIT <br/> PUBLIC SYNONYM <br/> DATABASE LINK <br/> PROFILE <br/> SYSTEM GRANT |

### Audit Options

| Option              | Description                                                              |
| :------------------ | :----------------------------------------------------------------------- |
| ALL                 | Audit all statement options apart from the additional statement options. |
| ALL STATEMENTS      | Audit all executions of **top-level SQL statements** that are issued directly by a user. Does not audit the statements executed within PL/SQL procedures or functions.                                                                                                                                             |
| ALL PRIVILEGES      | Audit system privileges.                                                                                                                     |
| IN SESSION CURRENT  | Limit auditing to the current session. Auditing will persist until the end of the session and cannot be stopped using the NOAUDIT statement. |
| BY SESSION          | Audit system privileges.                                                |
| BY ACCESS           | Audit system privileges.                                                |
| WHENEVER SUCCESSFUL | Audit system privileges.                                                |
| NETWORK             | Audit internal failures in the network layer.                           |
| DIRECT_PATH LOAD    |   |


#### Examples
```sql
SQL> AUDIT ALL;
SQL> AUDIT ALL STATEMENTS;
SQL> AUDIT ALL PRIVILEGES;

SQL> AUDIT <OPERATION> IN SESSION CURRENT;

SQL> AUDIT <OPERATION> BY SESSION;
SQL> AUDIT <OPERATION> BY ACCESS;

SQL> AUDIT <OPERATION> WHENEVER SUCCESSFUL;
SQL> AUDIT <OPERATION> WHENEVER NOT SUCCESSFUL;

SQL> AUDIT <OPERATION> BY SESSION WHENEVER SUCCESSFUL;
SQL> AUDIT <OPERATION> BY ACCESS  WHENEVER NOT SUCCESSFUL;

SQL> AUDIT NETWORK;
```


## Unified Auditing - 12.2 or higher (ex: 12c, 19c, 21c)
