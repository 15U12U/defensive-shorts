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
### Basic Audit Configuration Options
#### AUDIT_TRAIL
| Parameter     | Auditing Status    | Description                                                                                               |
| :------------ | :----------------: | :-------------------------------------------------------------------------------------------------------- |
| NONE          | :x:                | Auditing is disabled.                                                                                     |
| DB            | :heavy_check_mark: | Write the standard audit content to _**SYS.AUD$**_ table.                                                 |
| DB, EXTENDED  | :heavy_check_mark: | Similar to **DB**, but the _SQL_BIND_ and _SQL_TEXT_ columns are also populated for _**SYS.AUD$**_ table. |
| XML           | :heavy_check_mark: | Write the standard audit content and FGA audit content to an XML formatted file.                          |
| XML, EXTENDED | :heavy_check_mark: | Similar to **XML**, but the _SQL_BIND_ and _SQL_TEXT_ columns are also populated in XML file.             |
| OS            | :heavy_check_mark: | Write the standard audit content to text files.                                                           |

#### AUDIT_SYS_OPERATIONS
| Parameter    | Auditing Status    | Description                                                                                 |
| :----------- | :----------------: | :------------------------------------------------------------------------------------------ |
| FALSE        | :x:                | Auditing is disabled.                                                                       |
| TRUE         | :heavy_check_mark: | Enables auditing of SQL statements directly issued by users with **SYS** authorization such as **SYSASM**, **SYSBACKUP**, **SYSDBA**, **SYSDG**, **SYSKM**, or **SYSOPER** privileges, as well as SQL statements that have been executed with **SYS** authorization using the _**PL/SQL**_ package _DBMS_SYS_SQL_. |

#### AUDIT_SYSLOG_LEVEL
> **Note**  
> 
> _AUDIT_SYSLOG_LEVEL allows SYS and standard OS audit records to be written to the system audit log using the SYSLOG utility._

| Type      | Available Parameters                                                                              |
| :-------- | :------------------------------------------------------------------------------------------------ |
| facility  | `USER` <br> `LOCAL0` \| `LOCAL1` \| `LOCAL2` \| `LOCAL3` \| `LOCAL4` \| `LOCAL5` \| `LOCAL6` \| `LOCAL7` <br> `SYSLOG` <br> `DAEMON` <br> `KERN` <br> `MAIL` <br> `AUTH` <br> `LPR` <br> `NEWS` <br> `UUCP` <br> `CRON` |
| priority  | `NOTICE` <br> `INFO` <br> `DEBUG` <br> `WARNING` <br> `ERR` <br> `CRIT` <br> `ALERT` <br> `EMERG` |

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

| Level     | Description                                                                                        | Example                          |
| :-------- | :------------------------------------------------------------------------------------------------- | :------------------------------- |
| Statement | Audit specific SQL statements, such as ```SELECT```, ```INSERT```, ```UPDATE```, and ```DELETE```. | ```AUDIT SELECT;```              |
| Object    | Audit actions on specific schema objects, such as tables, views, and procedures.                   | ```AUDIT SELECT ON employees;``` |
| Privilege | Audit the use of system privileges and object privileges.                                          | ```AUDIT DROP ANY TABLE;```      |

#### SQL Statement Types

| Statement Type                     | Description                                                                         | Example                               |
| :--------------------------------- | :---------------------------------------------------------------------------------- | :------------------------------------ |
| DDL (Data Definition Language)     | Define the structure of a database and objects, such as tables, views, and indexes. | ```CREATE```, ```ALTER```, ```DROP```, ```TRUNCATE```, ```RENAME``` |
| DML (Data Manipulation Language)   | Manipulate data stored in a database.                                               | ```SELECT```, ```INSERT```, ```UPDATE```, ```DELETE```, ```MERGE```    |
| DCL (Data Control Language)        | Control access to data stored in a database.                                        | ```GRANT```, ```REVOKE```                                              |
| TCL (Transaction Control Language) | Manage transactions in a database.                                                  | ```COMMIT```, ```ROLLBACK```, ```SAVEPOINT```              |

#### Security-relevant SQL Statements and Privileges audited by Default
| Level         | Audit                                                                                                                                               |
| :------------ | :-------------------------------------------------------------------------------------------------------------------------------------------------- |
| Privilege     | ```ALTER ANY PROCEDURE``` <br/> ```ALTER ANY TABLE``` <br/> ```ALTER DATABASE``` <br/> ```ALTER PROFILE``` <br/> ```ALTER SYSTEM``` <br/> ```ALTER USER``` <br/> ```AUDIT SYSTEM``` <br/> ```CREATE ANY JOB``` <br/> ```CREATE ANY LIBRARY``` <br/> ```CREATE ANY PROCEDURE``` <br/> ```CREATE ANY TABLE``` <br/> ```CREATE EXTERNAL JOB``` <br/> ```CREATE PUBLIC DATABASE LINK``` <br/> ```CREATE SESSION``` <br/> ```CREATE USER``` <br/> ```DROP ANY PROCEDURE``` <br/> ```DROP ANY TABLE``` <br/> ```DROP PROFILE``` <br/> ```DROP USER``` <br/> ```EXEMPT ACCESS POLICY``` <br/> ```GRANT ANY OBJECT PRIVILEGE``` <br/> ```GRANT ANY PRIVILEGE``` <br/> ```GRANT ANY ROLE```                                                                                                                                                  |
| Statement     | ```ROLE``` <br/> ```SYSTEM AUDIT``` <br/> ```PUBLIC SYNONYM``` <br/> ```DATABASE LINK``` <br/> ```PROFILE``` <br/> ```SYSTEM GRANT```               |

### 'AUDIT' Options

| Option                  | Description                                                                                                                               |
| :---------------------- | :---------------------------------------------------------------------------------------------------------------------------------------- |
| ALL                     | Audit \*all statement options apart from the \*additional statement options.                                                              |
| ALL STATEMENTS          | Audit all executions of **top-level SQL statements** that are issued directly by a user. Does not audit the statements executed within PL/SQL procedures or functions.                                                                                                                                       |
| ALL PRIVILEGES          | Audit system privileges.                                                                                                                  |
| IN SESSION CURRENT      | Limit auditing to the current session. Auditing will persist until the end of the session and cannot be stopped using the ```NOAUDIT``` statement.                                                                                                                                                            |
| ON DEFAULT              | Establish a default auditing options for subsequently created objects.                                                                    |
| BY SESSION              | Write a single record for all SQL statements or operations of the same type executed on the same schema objects in the same session. Recommended to include the ```BY ACCESS``` clause for all ```AUDIT``` statements and if not explicitly specified, included by default.                                |
| BY ACCESS               | Write one record for each audited statement and operation.                                                                                |
| WHENEVER SUCCESSFUL     | Audit only SQL statements and operations that succeed.                                                                                    |
| WHENEVER NOT SUCCESSFUL | Audit only SQL statements and operations that fail or result in errors.                                                                   |
| NETWORK                 | Audit internal failures in the network layer.                                                                                             |
| DIRECT_PATH LOAD        | Audit **SQL\*Loader** direct path loads.                                                                                                  |

#### Audit Statement Options

| Shortcut             | SQL Statements and Operations Audited                                                                                                        |
| :------------------- | :------------------------------------------------------------------------------------------------------------------------------------------- |
| ALTER SYSTEM         | ```ALTER SYSTEM```                                                                                                                           |
| CLUSTER              | ```CREATE CLUSTER``` <br> ```ALTER CLUSTER``` <br> ```DROP CLUSTER``` <br> ```TRUNCATE CLUSTER```                                            |
| CONTEXT              | ```CREATE CONTEXT``` <br> ```DROP CONTEXT```                                                                                                 |
| DATABASE LINK        | ```CREATE DATABASE LINK``` <br> ```ALTER DATABASE LINK``` <br> ```DROP DATABASE LINK```                                                      |
| DIMENSION            | ```CREATE DIMENSION``` <br> ```ALTER DIMENSION``` <br> ```DROP DIMENSION```                                                                  |
| DIRECTORY            | ```CREATE DIRECTORY``` <br> ```DROP DIRECTORY```                                                                                             |
| INDEX                | ```CREATE INDEX``` <br> ```ALTER INDEX``` <br> ```ANALYZE INDEX``` <br> ```DROP INDEX```                                                     |
| MATERIALIZED VIEW    | ```CREATE MATERIALIZED VIEW``` <br> ```ALTER MATERIALIZED VIEW``` <br> ```DROP MATERIALIZED VIEW```                                          |
| NOT EXISTS           | _All SQL statements that fail because a specified object does not exist._                                                                    |
| OUTLINE              | ```CREATE OUTLINE``` <br> ```ALTER OUTLINE``` <br> ```DROP OUTLINE```                                                                        |
| PLUGGABLE DATABASE   | ```CREATE PLUGGABLE DATABASE``` <br> ```ALTER PLUGGABLE DATABASE``` <br> ```DROP PLUGGABLE DATABASE```                                       |
| PROCEDURE            | ```CREATE FUNCTION``` <br> ```CREATE LIBRARY``` <br> ```CREATE PACKAGE``` <br> ```CREATE PACKAGE BODY``` <br> ```CREATE PROCEDURE``` <br> ```DROP FUNCTION``` <br> ```DROP LIBRARY``` <br> ```DROP PACKAGE``` <br> ```DROP PROCEDURE```                                                                         |
| PROFILE              | ```CREATE PROFILE``` <br> ```ALTER PROFILE``` <br> ```DROP PROFILE```                                                                        |
| PUBLIC DATABASE LINK | ```CREATE PUBLIC DATABASE LINK``` <br> ```ALTER PUBLIC DATABASE LINK``` <br> ```DROP PUBLIC DATABASE LINK```                                 |
| PUBLIC SYNONYM       | ```CREATE PUBLIC SYNONYM``` <br> ```DROP PUBLIC SYNONYM```                                                                                   |
| ROLE                 | ```CREATE ROLE``` <br> ```ALTER ROLE``` <br> ```DROP ROLE``` <br> ```SET ROLE```                                                             |
| ROLLBACK SEGMENT     | ```CREATE ROLLBACK SEGMENT``` <br> ```ALTER ROLLBACK SEGMENT``` <br> ```DROP ROLLBACK SEGMENT```                                             |
| SEQUENCE             | ```CREATE SEQUENCE``` <br> ```DROP SEQUENCE```                                                                                               |
| SESSION              | _Logons_                                                                                                                                     |
| SYNONYM              | ```CREATE SYNONYM``` <br> ```DROP SYNONYM```                                                                                                 |
| SYSTEM AUDIT         | ```AUDIT _sql_statements_``` <br> ```NOAUDIT _sql_statements_```                                                                             |
| SYSTEM GRANT         | ```GRANT _system_privileges_and_roles_``` <br> ```REVOKE _system_privileges_and_roles_```                                                    |
| TABLE                | ```CREATE TABLE``` <br> ```DROP TABLE``` <br> ```TRUNCATE TABLE```                                                                           |
| TABLESPACE           | ```CREATE TABLESPACE``` <br> ```ALTER TABLESPACE``` <br> ```DROP TABLESPACE```                                                               |
| TRIGGER              | ```CREATE TRIGGER``` <br> ```ALTER TRIGGER``` <br> - with **ENABLE** and **DISABLE** clauses <br> ```DROP TRIGGER``` <br> ```ALTER TABLE``` <br> - with **ENABLE ALL TRIGGERS** clause <br> - and **DISABLE ALL TRIGGERS** clause                                                                                 |
| TYPE                 | ```CREATE TYPE``` <br> ```CREATE TYPE BODY``` <br> ```ALTER TYPE``` <br> ```DROP TYPE``` <br> ```DROP TYPE BODY```                           |
| USER                 | ```CREATE USER``` <br> ```ALTER USER``` <br> ```DROP USER``` <br> Notes: <br> - ```AUDIT USER``` audits these three SQL statements. Use ```AUDIT ALTER USER``` to audit statements that require the ```ALTER USER``` system privilege. <br> - An ```AUDIT ALTER USER``` statement does not audit a user changing his or her own password, as this activity does not require the ```ALTER USER``` system privilege.                                                            |
| VIEW                 | ```CREATE VIEW``` <br> ```DROP VIEW```                                                                                                       |

#### Additional Audit Statement Options

| Shortcut          | SQL Statements and Operations Audited                                                                                                      |
| :---------------- | :----------------------------------------------------------------------------------------------------------------------------------------- |
| ALTER SEQUENCE    | ```ALTER SEQUENCE```                                                                                                                       |
| ALTER TABLE       | ```ALTER TABLE```                                                                                                                          |
| COMMENT TABLE     | ```COMMENT ON TABLE _table, view, materialized view_``` <br> ```COMMENT ON COLUMN _table.column, view.column, materialized view.column_``` |
| DELETE TABLE      | ```DELETE FROM _table, view_```                                                                                                            |
| EXECUTE DIRECTORY | _Execution of any program in a directory_                                                                                                  |
| EXECUTE PROCEDURE | ```CALL``` <br> _Execution of any procedure or function or access to any variable, library, or cursor inside a package_                    |
| GRANT DIRECTORY   | ```GRANT privilege ON directory``` <br> ```REVOKE privilege ON directory```                                                                |
| GRANT PROCEDURE   | ```GRANT privilege ON procedure, function, package``` <br> ```REVOKE privilege ON procedure, function, package```                          |
| GRANT SEQUENCE    | ```GRANT privilege ON sequence``` <br> ```REVOKE privilege ON sequence```                                                                  |
| GRANT TABLE       | ```GRANT privilege ON table, view, materialized view``` <br> ```REVOKE privilege ON table, view, materialized view```                      |
| GRANT TYPE        | ```GRANT privilege ON TYPE``` <br> ```REVOKE privilege ON TYPE```                                                                          |
| INSERT TABLE      | ```INSERT INTO _table, view_```                                                                                                            |
| LOCK TABLE        | ```LOCK TABLE _table, view_```                                                                                                             |
| READ DIRECTORY    | _Read operations on a directory_                                                                                                           |
| SELECT SEQUENCE   | _Any statement containing_ ```_sequence_.CURRVAL``` _or_ ```_sequence_.NEXTVAL```                                                          |
| SELECT TABLE      | ```SELECT FROM _table, view, materialized view_```                                                                                         |
| UPDATE TABLE      | ```UPDATE _table, view_```                                                                                                                 |
| WRITE DIRECTORY   | _Write operations on a directory_                                                                                                          |


#### Examples
```sql
SQL> AUDIT ALL;
SQL> AUDIT ALL STATEMENTS;
SQL> AUDIT ALL PRIVILEGES;

SQL> AUDIT <OPERATION> IN SESSION CURRENT;
SQL> AUDIT SELECT IN SESSION CURRENT;                                  --Example

SQL> AUDIT <OPERATION> ON DEFAULT;
SQL> AUDIT ALTER, GRANT, INSERT, UPDATE, DELETE ON DEFAULT;            --Example

SQL> AUDIT <OPERATION> BY SESSION;
SQL> AUDIT <OPERATION> BY ACCESS;
SQL> AUDIT DELETE BY SESSION;                                          --Example
SQL> AUDIT UPDATE BY ACCESS;                                           --Example

SQL> AUDIT <OPERATION> WHENEVER SUCCESSFUL;
SQL> AUDIT <OPERATION> WHENEVER NOT SUCCESSFUL;
SQL> AUDIT ROLE WHENEVER SUCCESSFUL;                                   --Example
SQL> AUDIT ROLE WHENEVER NOT SUCCESSFUL;                               --Example

SQL> AUDIT <OPERATION> BY SESSION WHENEVER SUCCESSFUL;
SQL> AUDIT <OPERATION> BY ACCESS WHENEVER NOT SUCCESSFUL;
SQL> AUDIT SELECT ON hr.employees BY SESSION WHENEVER NOT SUCCESSFUL;  --Example
SQL> AUDIT SELECT ON hr.employees BY ACCESS WHENEVER SUCCESSFUL;       --Example

SQL> AUDIT NETWORK;

SQL> AUDIT DIRECT_PATH LOAD;

# Disable Auditing
SQL> NOAUDIT <OPERATION>;
SQL> NOAUDIT NETWORK;                                                  --Example
```

### Oracle FGA - Fine Grained Auditing (DBMS_FGA)
#### DBMS_FGA Subprograms

| Subprogram     | Description                                                                   |
| :------------- | :---------------------------------------------------------------------------- |
| ADD_POLICY     | Creates an audit policy using the supplied predicate as the audit condition.  |
| DROP_POLICY    | Drops an audit policy.                                                        |
| ENABLE_POLICY  | Enables an audit policy.                                                      |
| DISABLE_POLICY | Disables an audit policy.                                                     |


##### Example
```sql
DBMS_FGA.ADD_POLICY (
   object_schema      =>  'scott',
   object_name        =>  'emp',
   policy_name        =>  'mypolicy1',
   audit_condition    =>  'sal < 100',
   audit_column       =>  'comm,sal',
   handler_schema     =>   NULL,
   handler_module     =>   NULL,
   enable             =>   TRUE,
   statement_types    =>  'INSERT, UPDATE',
   audit_column_opts  =>   DBMS_FGA.ANY_COLUMNS,
   policy_owner       =>  'sec_admin);






```





## Unified Auditing - 12.2 or higher (ex: 12c, 19c, 21c)
