# Syslog Configuration
## Syslog Facility Levels

| Number 	| Keyword  	| Facility description                     	|
| :-----:	| :--------	| :----------------------------------------	|
| 0      	| kern     	| kernel messages                          	|
| 1      	| user     	| user-level messages                      	|
| 2      	| mail     	| mail system                              	|
| 3      	| daemon   	| system daemons                           	|
| 4      	| auth     	| security/authorization messages          	|
| 5      	| syslog   	| messages generated internally by syslogd 	|
| 6      	| lpr      	| line printer subsystem                   	|
| 7      	| news     	| network news subsystem                   	|
| 8      	| uucp     	| UUCP subsystem                           	|
| 9      	| –        	| clock daemon                             	|
| 10     	| authpriv 	| security/authorization messages          	|
| 11     	| ftp      	| FTP daemon                               	|
| 12     	| –        	| NTP subsystem                            	|
| 13     	| –        	| log audit                                	|
| 14     	| –        	| log alert                                	|
| 15     	| cron     	| clock daemon                             	|
| 16     	| local0   	| local use 0                             	|
| 17     	| local1   	| local use 1                             	|
| 18     	| local2   	| local use 2                             	|
| 19     	| local3   	| local use 3                             	|
| 20     	| local4   	| local use 4                             	|
| 21     	| local5   	| local use 5                             	|
| 22     	| local6   	| local use 6                             	|
| 23     	| local7   	| local use 7                             	|

## Syslog Severity Levels

| Code 	| Severity      	| Keyword        	| Description                       	|
| :---:	| :--------------	| :--------------	| :----------------------------------	|
| 0    	| Emergency     	| emerg (panic)  	| System is unusable.               	|
| 1    	| Alert         	| alert          	| Action must be taken immediately. 	|
| 2    	| Critical      	| crit           	| Critical conditions.              	|
| 3    	| Error         	| err (error)    	| Error conditions.                 	|
| 4    	| Warning       	| warning (warn) 	| Warning conditions.               	|
| 5    	| Notice        	| notice         	| Normal but significant condition. 	|
| 6    	| Informational 	| info           	| Informational messages.           	|
| 7    	| Debug         	| debug          	| Debug-level messages.             	|
---

## Syslog Priority
```math
(FacilityNumber * 8) + SeverityCode = PRI
```

## Test Rsyslog configuration
```bash
rsyslogd -N 5
```
---

## Test syslog forwarding
### Using Netcat
```bash
echo "message" | nc -q0 127.0.0.1 514
```

### Using Logger
```bash
logger "test message"
```
---

# Install a syslog daemon
| Rsyslog | Syslog-ng |
| :----- | :------ |
| <pre lang=bash>sudo apt install rsyslog -y</pre><br><pre lang=bash>sudo yum install rsyslog -y</pre></br><pre lang=bash>sudo dnf install rsyslog -y</pre> | <pre lang=bash>sudo apt install syslog-ng -y</pre><br><pre lang=bash>sudo yum install syslog-ng -y</pre></br><pre lang=bash>sudo dnf install syslog-ng -y</pre> |

# Syslog over TLS (Server Configuration)
## Install TLS protocol support for rsyslog (GnuTLS/OpenSSL)
| GnuTLS | OpenSSL |
| :----- | :------ |
| <pre lang=bash>sudo apt install rsyslog-gnutls -y</pre><br><pre lang=bash>sudo yum install rsyslog-gnutls -y</pre></br><pre lang=bash>sudo dnf install rsyslog-gnutls -y</pre> | <pre lang=bash>sudo apt install rsyslog-openssl -y</pre><br><pre lang=bash>sudo yum install rsyslog-openssl -y</pre></br><pre lang=bash>sudo dnf install rsyslog-openssl -y</pre> |

## Server Configuration
- [rsyslog-tls.conf](rsyslog/rsyslog.d/rsyslog-tls.conf)

## Client Configuration
- [imfile.conf](rsyslog/rsyslog.d/imfile.conf)

