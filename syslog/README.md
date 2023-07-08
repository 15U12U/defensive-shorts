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
### RSyslog
```bash
rsyslogd -N 5
rsyslogd -N 1 -f /etc/rsyslog.conf
```
### Syslog-ng
```bash
syslog-ng --syntax-only
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


# 1. Configure Syslog Forwarding
## 1.1. Verify Syslog/Rsyslog installation and version on the host
### 1.1.1. RHEL-based Systems (CentOS / Fedora / Rocky Linux / Oracle Linux / Alma Linux etc.)
```
$ rpm -qa syslog
$ rpm -qa rsyslog
```
### 1.1.2. Debian-based Systems (Ubuntu / Kubuntu / Linux Mint etc.)
```
$ apt list | grep -i "installed" | grep -i "syslog"
$ apt list | grep -i "installed" | grep -i "rsyslog"
```
### 1.1.3. Solaris
```
$ pkginfo | grep -i "syslog"
$ pkginfo | grep -i "rsyslog"
```
> **Note** : Check the default system syslog configuration
```
# svcs system-log
# svcs -a | grep -i "system-log"
```
### 1.1.4. AIX
```
$ lslpp -l | grep -i "syslog"
$ lslpp -l | grep -i "rsyslog"
```
or
```
$ rpm -qa syslog
$ rpm -qa rsyslog
```

---
## 1.2. Install Rsyslog on the host
### 1.2.1. RHEL-based Systems (CentOS / Fedora / Rocky Linux / Oracle Linux / Alma Linux etc.)
```
$ sudo yum install -y rsyslog
# yum install -y rsyslog
```
or
```
$ sudo dnf install -y rsyslog
# dnf install -y rsyslog
```
### 1.2.2. Debian-based Systems (Ubuntu / Kubuntu / Linux Mint etc.)
```
$ sudo apt install -y rsyslog
# apt install -y rsyslog
```
### 1.2.3. Solaris
```
# pkg install system/rsyslog
```

---
## 1.3. Enable and Start Syslog/Rsyslog Service
### 1.3.1. RHEL-based Systems / Debian-based Systems
#### SystemD
```
$ sudo systemctl enable --now syslog.service
# systemctl enable --now syslog.service
```
```
$ sudo systemctl enable --now rsyslog.service
# systemctl enable --now rsyslog.service
```
#### SysVInit
```
$ sudo service syslog start
# service syslog start
```
```
$ sudo service rsyslog start
# service rsyslog start
```
### 1.3.2. Solaris
```
# svcadm enable svc:/system/system-log:syslog
# svcadm refresh svc:/system/system-log:syslog
```
```
# svcadm enable svc:/system/system-log:rsyslog
# svcadm refresh svc:/system/system-log:rsyslog
```
> **Note** : You may have to disable ```system-log:default``` before enabling rsyslog
```
# svcadm disable svc:/system/system-log:default
```

### 1.3.3. AIX
```
# startsrc -s syslogd
# startsrc -s rsyslogd
```

---
## 1.4. Configure syslog forwarding on the host
### 1.4.1. Syslog / Rsyslog v7.x and below
#### Edit the ```/etc/syslog.conf``` or ```/etc/rsyslog.conf``` configuration file as follows,
```
$ sudo vi /etc/syslog.conf
# vi /etc/syslog.conf
```
```
$ sudo vi /etc/rsyslog.conf
# vi /etc/rsyslog.conf
```

#### Append the following configuration to the file
```
*.* @@<Log_Collector_IP>:514
```

##### - Example
```
*.* @@192.168.100.10:514
```

### 1.4.2. Rsyslog v8.x and above
#### Edit the ```/etc/rsyslog.conf``` configuration file as follows,
```
$ sudo vi /etc/rsyslog.conf
# vi /etc/rsyslog.conf
```

#### Append the following configuration to the file
```
*.* action(type="omfwd" target="<Log_Collector_IP>" port="514" protocol="tcp")
```

##### - Example
```
*.* action(type="omfwd" target="192.168.100.10" port="514" protocol="tcp")
```

---
## 1.5. Restart Syslog/Rsyslog Service
### 1.5.1. RHEL-based Systems / Debian-based Systems
#### SystemD
```
$ sudo systemctl restart syslog.service
# systemctl restart syslog.service
```
```
$ sudo systemctl restart rsyslog.service
# systemctl restart rsyslog.service
```
#### SysVInit
```
$ sudo service syslog restart
# service syslog restart
```
```
$ sudo service rsyslog restart
# service rsyslog restart
```

### 1.5.2. Solaris
```
# svcadm restart system/system-log:syslog
# svcadm restart system/system-log:rsyslog
```

### 1.5.3. AIX
```
# refresh -s syslogd
# refresh -s rsyslogd
```
---
