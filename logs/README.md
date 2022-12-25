# general-log-locations

- ***This is a collection of default/common log locations in different systems.***

## System Logs
### Windows
```
C:\Windows\System32\winevt\Logs\Security.evtx
C:\Windows\System32\winevt\Logs\Application.evtx
C:\Windows\System32\winevt\Logs\System.evtx
C:\Windows\System32\winevt\Logs\Windows Powershell.evtx
C:\Windows\System32\winevt\Logs\Microsoft-Windows-PowerShell%4Operational.evtx
C:\Windows\System32\winevt\Logs\Microsoft-Windows-Sysmon%4Operational.evtx
```

### Linux/Unix
```
/
└── var
    ├── log
    │   ├── messages
    │   ├── syslog
    │   ├── kern.log
    │   ├── cron
    │   ├── dmesg
    │   ├── maillog
    │   ├── mail.log
    │   ├── user.log
    │   ├── cups
    │   ├── daemon.log
    │   ├── anaconda.log
    │   ├── auth.log
    │   ├── secure
    │   ├── sulog
    │   ├── dpkg.log
    │   ├── yum.log
    │   ├── wtmp            // Binary File
    │   │                   // Commands to view:
    │   │                   //      $ last
    │   │                   //      $ last -f /var/log/wtmp
    │   │                   //      $ utmpdump /var/log/wtmp
    │   ├── btmp            // Binary File
    │   │                   // Commands to view:
    │   │                   //      $ lastb
    │   │                   //      $ last -f /var/log/btmp
    │   │                   //      $ utmpdump /var/log/btmp
    │   ├── faillog         // Binary File
    │   │                   // Command to view:
    │   │                   //      $ faillog -a
    │   ├── lastlog         // Binary File
    │   │                   // Commands to view:
    │   │                   //      $ lastlog
    │   │                   //      $ aulastlog
    │   ├── apt
    │   │   ├── history.log
    │   │   └── term.log
    │   └── audit
    │       └── audit.log   // Commands to view:
    │                       //      $ ausearch
    │                       //      $ aureport
    ├── audit/              // Binary Files
    │                       // Commands to view:
    │                       //      $ praudit
    │                       //      $ auditreduce
    ├── adm
    |   ├── messages
    |   ├── secure
    |   ├── wtmpx
    |   └── sulog
    └── run
        └── utmp            // Binary File
                            // Commands to view:
                            //      $ last -f /var/run/utmp
                            //      $ utmpdump /var/run/utmp 
```

---
## Apache Tomcat
```
C:\Program Files(x86)\Apache Software Foundation\Tomcat 7.0\Logs
C:\apache-tomcat-8.0.35\apache-tomcat-8.0.35\logs\localhost.log
C:\apache-tomcat-8.0.35\apache-tomcat-8.0.35\logs\localhost.*.log
```
## IIS
```
C:\inetpub\Logs\LogFiles
```
## MSSQL
```
C:\Program Files\Microsoft SQL Server\MSSQL10_50.MSSQLSERVER\MSSQL\Logs
```
## Linux Auth/Secure
```
/var/log/secure
/var/log/auth.log
```
## MySQL
```
/var/log/mysql/error.log
```
## PostgreSQL
```
/var/log/postgresql/postgresql-10-main.log.*
```

General Log Channels,  Tomcat c:\apache-tomcat-8.0.35\apache-tomcat-8.0.35\logs\localhost.*.log   localhost_access_log.*.txt


"General Channels,C:\apache2.4\Logs
C:\Tomcat8.5\Log"


/var/log/auth.log-not configured , /var/apache2/2.4/logs/access_log,error_log



"/var/log/secure*
/var/log/mariadb/mariadb.log
var/lib/mysql/mysql-no"
"/opt/tomcat7.1/logs
/opt/tomcat7.2/logs .txt
/opt/tomcat7.3/logs
/var/log/httpd"



