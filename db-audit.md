# Database Auditing Configuration Guide
## Oracle Database
### Check the status of audting
```sql
SQL> SHOW PARAMETER AUDIT_TRAIL
```

| Parameter    | Auditing Status    | Description                                                                                 |
| :----------- | :----------------: | :------------------------------------------------------------------------------------------ |
| NONE         | :x:                | Auditing is disabled.                                                                       |
| DB           | :heavy_check_mark: | All audit records stored in table(SYS.AUD$).                                                |
| DB,EXTENDED  | :heavy_check_mark: | Similar to DB, but the SQL_BIND and SQL_TEXT columns are also populated for SYS.AUD$ table. |
| XML          | :heavy_check_mark: | Records stored as XML format files.                                                         |
| XML,EXTENDED | :heavy_check_mark: | Similar to XML, but the SQL_BIND and SQL_TEXT columns are also populated in XML file.       |
| OS           | :heavy_check_mark: | Audit records to the operating system's text file.                                          |

### Enable/Disable audting
#### - Enable -
```sql
SQL> ALTER SYSTEM SET AUDIT_TRAIL=DB SCOPE=SPFILE;
```
OR
```sql
SQL> ALTER SYSTEM SET AUDIT_TRAIL=TRUE SCOPE=SPFILE;
```
#### - Disable -
```sql
SQL> ALTER SYSTEM SET AUDIT_TRAIL=NONE SCOPE=SPFILE;
```



