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
##### Linux
| Location             | Scope                                             |
| :------------------- | :------------------------------------------------ |
| /etc/my.cnf          | Global                                            |
| /etc/mysql/my.cnf    | Global                                            |
| $MARIADB_HOME/my.cnf | Server                                            |
| $MYSQL_HOME/my.cnf   | Server                                            |
| defaults-extra-file  | File specified with --defaults-extra-file, if any |
| ~/.my.cnf            | User                                              |

##### Windows
| Location                        | Scope                                             |
| :------------------------------ | :------------------------------------------------ |
| System Windows Directory\my.ini | Global                                            |
| System Windows Directory\my.cnf | Global                                            |
| Windows Directory\my.ini        | Global                                            |
| Windows Directory\my.cnf        | Global                                            |
| C:\my.ini                       | Global                                            |
| C:\my.cnf                       | Global                                            |
| INSTALLDIR\my.ini               | Server                                            |
| INSTALLDIR\my.cnf               | Server                                            |
| INSTALLDIR\data\my.ini          | Server                                            |
| INSTALLDIR\data\my.cnf          | Server                                            |
| %MARIADB_HOME%\my.ini           | Server (from MariaDB 10.6)                        |
| %MARIADB_HOME%\my.cnf           | Server (from MariaDB 10.6)                        |
| %MYSQL_HOME%\my.ini             | Server                                            |
| %MYSQL_HOME%\my.cnf             | Server                                            |
| defaults-extra-file             | File specified with --defaults-extra-file, if any |

```mysql
[mysqld]
...
log_output = FILE                                              -- Available Options [ 'FILE' | 'TABLE' | 'NONE' ]
general_log = 1                                                -- Available Options [ 1 | 0 ]
general_log_file = /var/log/mysql/mysql_general_query.log
```

```mysql
[mariadb]
...
log_output = FILE                                              -- Available Options [ 'FILE' | 'TABLE' | 'NONE' ]
general_log = 1                                                -- Available Options [ 1 | 0 ]
general_log_file = /var/log/mysql/mariadb_general_query.log
```

```bash
sudo systemctl restart mysql.service
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

> [!NOTE]
> If you have set the _'log_output'_ to `TABLE`, you can view the General Query Logs on the table as follows

```mysql
SELECT * FROM mysql.general_log;
```

| event_time          | user_host                      | thread_id | server_id | command_type | argument |
| :------------------ | :----------------------------- | :-------: | :-------: | :----------- | :------: |
| 2025-01-04 13:35:10 | admin[admin] @ localhost [::1] | 12350     | 1         | Connect      | `BLOB`   |
| 2025-01-04 13:35:11 | admin[admin] @ localhost [::1] | 12350     | 1         | Query        | `BLOB`   |
| 2025-01-04 13:35:12 | admin[admin] @ localhost [::1] | 12350     | 1         | Query        | `BLOB`   |
| 2025-01-04 13:35:13 | admin[admin] @ localhost [::1] | 12350     | 1         | Query        | `BLOB`   |
| 2025-01-04 13:35:14 | admin[admin] @ localhost [::1] | 12350     | 1         | Quit         | `BLOB`   |

```mysql
SELECT *, CAST(argument as char(100)) as 'cast_arg' FROM mysql.general_log;
```

| event_time          | user_host                      | thread_id | server_id | command_type | argument | cast_arg                    |
| :------------------ | :----------------------------- | :-------: | :-------: | :----------- | :------: | :-------------------------- |
| 2025-01-04 13:35:10 | admin[admin] @ localhost [::1] | 12350     | 1         | Connect      | `BLOB`   |                             |
| 2025-01-04 13:35:11 | admin[admin] @ localhost [::1] | 12350     | 1         | Query        | `BLOB`   | SHOW DATABASES              |
| 2025-01-04 13:35:12 | admin[admin] @ localhost [::1] | 12350     | 1         | Query        | `BLOB`   | USE production              |
| 2025-01-04 13:35:13 | admin[admin] @ localhost [::1] | 12350     | 1         | Query        | `BLOB`   | SELECT COUNT(*) FROM orders |
| 2025-01-04 13:35:14 | admin[admin] @ localhost [::1] | 12350     | 1         | Quit         | `BLOB`   |                             |

<br>

## Error Log
The error log contains a record of mysqld startup and shutdown times. It also contains diagnostic messages such as errors, warnings, and notes that occur during server startup and shutdown, and while the server is running.

### Verify General Query Log
```mysql
SHOW VARIABLES LIKE "log_error%";
```

#### Output
##### MysSQL
```mysql
+----------------------------+---------------------------------------+
| Variable_name              | Value                                 |
+----------------------------+---------------------------------------+
| log_error                  | /var/log/mysql/error.log              |
| log_error_services         | log_sink_json                         |
| log_error_suppression_list | MY-000031,ER_SERVER_SHUTDOWN_COMPLETE |
| log_error_verbosity        | 2                                     |
+----------------------------+---------------------------------------+
```

##### MariaDB
```mysql
+---------------+------------------------------+
| Variable_name | Value                        |
+---------------+------------------------------+
| log_error     | /var/log/mariadb/mariadb.err |
+---------------+------------------------------+
```

### Enabling Error Log [^3]
#### Method 1: System Variable
```mysql
SET GLOBAL log_error_services = 'log_filter_internal,log_sink_internal'; -- OR
SET PERSIST log_error_services = 'log_filter_internal; log_sink_internal; log_sink_json';
```

#### Method 2: Option File
```mysql
[mysqld]
log_error_services='log_filter_internal; log_sink_internal; log_sink_json'
```

#### Sample Error Log Output
```mysql
[Timestamp]                 [Thread] [Label]   [Error Code] [Subsystem] [Message]
2020-08-06T14:25:02.835618Z 0        [Note]    [MY-012487]  [InnoDB]    DDL log recovery : begin
2020-08-06T14:25:02.936146Z 0        [Warning] [MY-010068]  [Server]    CA certificate /var/mysql/sslinfo/cacert.pem is self signed.
2020-08-06T14:25:02.963127Z 0        [Note]    [MY-010253]  [Server]    IPv6 is available.
2020-08-06T14:25:03.109022Z 5        [Note]    [MY-010051]  [Server]    Event Scheduler: scheduler thread started with id 5
```


[^1]: [The General Query Log](https://dev.mysql.com/doc/refman/9.1/en/query-log.html)
[^2]: [Default Option File Locations on Linux, Unix, Mac](https://mariadb.com/kb/en/configuring-mariadb-with-option-files/)
[^3]: [Error Log Configuration](https://dev.mysql.com/doc/refman/8.4/en/error-log-configuration.html)
