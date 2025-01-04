# MySQL/MariaDB Audit Configuration Guide
## General Query Log
The general query log is a general record of what mysqld is doing. The server writes information to this log when clients connect or disconnect, and it logs each SQL statement received from clients.

### Verify General Query Log
```mysql
SHOW VARIABLES LIKE "general_log%";
```

#### Output
```mysql
+------------------+----------------------------------+
| Variable_name    | Value                            |
+------------------+----------------------------------+
| general_log      | ON                               |
| general_log_file | /var/log/mysql/general-query.log |
+------------------+----------------------------------+
```

### Enabling General Query Log
#### Method 1: System Variable [^1]
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

#### Method 2: Option File [^2]

| Location             | Scope                                             |
| :------------------- | :------------------------------------------------ |
| /etc/my.cnf          | Global                                            |
| /etc/mysql/my.cnf    | Global                                            |
| $MARIADB_HOME/my.cnf | Server                                            |
| $MYSQL_HOME/my.cnf   | Server                                            |
| defaults-extra-file  | File specified with --defaults-extra-file, if any |
| ~/.my.cnf            | User                                              |

```mysql
[mariadb]
...
log_output=FILE
general_log
general_log_file=/var/log/mysql/mariadb.log
```


#### Sample General Query Log Output
```mysql
[Timestamp]               [ID] [Command Type] [User@Host]/[SQL Statement]   
2025-01-04 13:05:10 12345 11   Connect        root@localhost as anonymous on using socket
2025-01-04 13:05:11 12345 11   Query          SELECT DATABASE()
2025-01-04 13:05:12 12345 11   Init DB        testdb
2025-01-04 13:05:13 12345 11   Query          SELECT * FROM users
2025-01-04 13:05:14 12345 11   Quit
2025-01-04 13:15:30 12346 12   Connect        admin@localhost on
2025-01-04 13:15:31 12346 12   Query          SET autocommit=1
2025-01-04 13:15:32 12346 12   Query          SHOW TABLES
2025-01-04 13:15:33 12346 12   Query          INSERT INTO orders (id, product, quantity) VALUES (1, 'Laptop', 2)
2025-01-04 13:15:34 12346 12   Quit
```

<br>

## Error Log
The error log contains a record of mysqld startup and shutdown times. It also contains diagnostic messages such as errors, warnings, and notes that occur during server startup and shutdown, and while the server is running.

### Enabling Error Log
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


[^1]: [The General Query Log](https://dev.mysql.com/doc/refman/9.1/en/query-log.html)
[^2]: [Default Option File Locations on Linux, Unix, Mac](https://mariadb.com/kb/en/configuring-mariadb-with-option-files/#default-option-file-locations-on-linux-unix-mac)
[^3]: []()
