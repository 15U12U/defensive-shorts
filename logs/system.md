## System Logs
### Windows
```
C:
└── Windows
    └── System32
        └── winevt
            └── Logs
                ├── Security.evtx
                ├── Application.evtx
                ├── System.evtx
                ├── Windows Powershell.evtx
                ├── Microsoft-Windows-PowerShell%4Operational.evtx
                └── Microsoft-Windows-Sysmon%4Operational.evtx
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
