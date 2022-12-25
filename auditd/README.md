# Linux Audit rules templates

- [CentOS/RedHat/Oracle Audit Rules](audit.rules/centos.rules)
- [Debian/Ubuntu Audit Rules](audit.rules/ubuntu.rules)
---
<br>

# Check for installed auditing packages
## RHEL/Oracle Linux/CentOS
```bash
rpm -q audit audit-libs audispd-plugins
```

## Debian/Ubuntu
```bash
apt list auditd audispd-plugins
```
or
```bash
dpkg -l auditd audispd-plugins
```
---
<br>

# Check the run levels of the packages
## RHEL/Oracle Linux/CentOS
```bash
chkconfig --list auditd
chkconfig --list audispd-plugins
```
or
```bash
systemctl is-enabled auditd
systemctl is-enabled audispd-plugins
```

## Debian/Ubuntu
```bash
systemctl is-enabled auditd
systemctl is-enabled audispd-plugins
```
---
<br>

# Enable run levels of the packages
## RHEL/Oracle Linux/CentOS
```bash
chkconfig auditd on
chkconfig audispd-plugins on
```
or
```bash
systemctl enable auditd
systemctl enable audispd-plugins
```

## Debian/Ubuntu
```bash
systemctl enable auditd
systemctl enable audispd-plugins
```
---
<br>

# Send audit logs via syslog
## Edit audispd syslog configuration file
```bash
vim /etc/audisp/plugins.d/syslog.conf
```
or
```bash
vim /etc/audit/plugins.d/syslog.conf
```

## Edit the following line to activate the feature
```
active = yes
```
