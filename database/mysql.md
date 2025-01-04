# MySQL/MariaDB Audit Configuration Guide
## General Query Log
### Enabling General Query Log
```mysql
SET GLOBAL log_output = 'FILE';                                         -- Available Options [ 'FILE' | 'TABLE' | 'NONE' ]
SET GLOBAL general_log = 'ON';  /* or */ SET GLOBAL general_log = 1;    -- Available Options [ 'ON'/1 | 'OFF'/0 ]
```

> [!NOTE]
> If you want to change the general log file location, you can run the following commands and change the location accordingly

```mysql
SET GLOBAL general_log_file = 'C:/Temp/mysql_general_query.log';    -- Windows
SET GLOBAL general_log_file = '/tmp/mysql_general_query.log';       -- Linux
```

```mysql
SET GLOBAL general_log_file = 'C:/Temp/mariadb_general_query.log';    -- Windows
SET GLOBAL general_log_file = '/tmp/mariadb_general_query.log';       -- Linux
```

