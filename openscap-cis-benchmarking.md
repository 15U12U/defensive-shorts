# Install OpenSCAP and SCAP Security Guide
### CentOS 8 / RHEL 8 / Fedora / Rocky Linux 8
```
dnf install -y openscap-scanner scap-security-guide
```
### CentOS 6,7 / RHEL 6,7
```
yum install -y openscap-scanner scap-security-guide
```
### Debian / Ubuntu
```
apt install -y libopenscap8 ssg-base ssg-debderived ssg-debian ssg-nondebian ssg-applications
```
or
```
apt install -y openscap-scanner ssg-base ssg-debderived ssg-debian ssg-nondebian ssg-applications
```
---
# List profiles for Different Operating Systems
```
oscap info <SOURCE_DATA_STREAM_FILE>
oscap info --profiles <SOURCE_DATA_STREAM_FILE>
oscap info --profile <PROFILE_ID> <SOURCE_DATA_STREAM_FILE>
```
### Example
```
oscap info /usr/share/xml/scap/ssg/content/ssg-rl8-ds-1.2.xml
oscap info --profiles /usr/share/xml/scap/ssg/content/ssg-rl8-ds-1.2.xml
oscap info --profile cis /usr/share/xml/scap/ssg/content/ssg-rl8-ds-1.2.xml
```
---
# Audit the host
```
oscap xccdf eval --profile <PROFILE_ID> --results-arf <ARF_FILE> --report <REPORT_FILE> <SOURCE_DATA_STREAM_FILE>
```
### Example
```
oscap xccdf eval --profile cis --results-arf arf-results.xml --report eval-results.html /usr/share/xml/scap/ssg/content/ssg-rl8-ds-1.2.xml
```
---
# Remediate the host during scanning
```
oscap xccdf eval --remediate --profile <PROFILE_ID> --results-arf <ARF_FILE> --report <REPORT_FILE> <SOURCE_DATA_STREAM_FILE>
```
### Example
```
oscap xccdf eval --remediate --profile xccdf_org.ssgproject.content_profile_cis --report rem-results.html /usr/share/xml/scap/ssg/content/ssg-rl8-ds-1.2.xml
```
---
# Remediate the host after scanning
```
oscap xccdf eval --profile <PROFILE_ID> --results <EVAL_FILE> <SOURCE_DATA_STREAM_FILE>
oscap xccdf remediate --results <REM_FILE> <EVAL_FILE>
```
### Example
```
oscap xccdf eval --profile xccdf_org.ssgproject.content_profile_ospp --results eval-results.xml /usr/share/xml/scap/ssg/content/ssg-rhel8-ds.xml
oscap xccdf remediate --results rem-results.xml eval-results.xml
```
---
# Revert cipher scheme back to default
```
update-crypto-policies --set DEFAULT
```
