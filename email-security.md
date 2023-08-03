# Email Security Configuration Guide
## 1. SPF
### View SPF Record
```
$ nslookup -type=TXT example.com
$ dig TXT example.com
$ dig -t TXT example.com
$ dig TXT example.com @1.1.1.1
```
#### Example
```
$ nslookup -type=TXT google.com
$ dig TXT _dmarc.google.com
$ dig -t TXT _dmarc.google.com
$ dig TXT _dmarc.google.com @1.1.1.1
```
#### Output
```
_dmarc.google.com        "v=DMARC1; p=reject; rua=mailto:mailauth-reports@google.com"
```
---


## 2. DKIM
### View DKIM Record
```
$ nslookup -type=TXT example.com
$ dig TXT example.com
$ dig -t TXT example.com
$ dig TXT example.com @1.1.1.1
```
#### Example
```
$ nslookup -type=TXT example.com
$ dig TXT example.com
$ dig -t TXT example.com
$ dig TXT example.com @1.1.1.1
```
---


## 3. DMARC
### View DMARC Record
```
$ nslookup -type=TXT example.com
$ dig TXT _dmarc.example.com
$ dig -t TXT _dmarc.example.com
$ dig TXT _dmarc.example.com @1.1.1.1
```
#### Example
```
$ nslookup -type=TXT google.com
$ dig TXT _dmarc.google.com
$ dig -t TXT _dmarc.google.com
$ dig TXT _dmarc.google.com @1.1.1.1
```
#### Output
```
_dmarc.google.com        "v=DMARC1; p=reject; rua=mailto:mailauth-reports@google.com"
```
---





