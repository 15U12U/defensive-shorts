# Email Security Configuration Guide
## 1. SPF
### View SPF Record
```
$ nslookup -type=TXT example.com
$ nslookup -q=TXT example.com
$ dig TXT example.com
$ dig -t TXT example.com
$ dig TXT example.com @1.1.1.1
```
#### Example
```
$ nslookup -type=TXT google.com
google.com      text = "v=spf1 include:_spf.google.com ~all"
$ dig TXT google.com
google.com.             0       IN      TXT     "v=spf1 include:_spf.google.com ~all"
```
---


## 2. DKIM
### View DKIM Record
```
$ nslookup -type=TXT <selector>._domainkey.example.com
$ nslookup -q=TXT <selector>._domainkey.example.com
$ dig TXT <selector>._domainkey.example.com
$ dig -t TXT <selector>._domainkey.example.com
$ dig TXT <selector>._domainkey.example.com @1.1.1.1
```
#### Example
```
$ nslookup -type=TXT <selector>._domainkey.google.com

$ dig TXT <selector>._domainkey.google.com

```
---


## 3. DMARC
### View DMARC Record
```
$ nslookup -type=TXT _dmarc.example.com
$ nslookup -q=TXT _dmarc.example.com
$ dig TXT _dmarc.example.com
$ dig -t TXT _dmarc.example.com
$ dig TXT _dmarc.example.com @1.1.1.1
```
#### Example
```
$ nslookup -type=TXT _dmarc.google.com
_dmarc.google.com       text = "v=DMARC1; p=reject; rua=mailto:mailauth-reports@google.com"
$ dig TXT _dmarc.google.com
_dmarc.google.com.      0       IN      TXT     "v=DMARC1; p=reject; rua=mailto:mailauth-reports@google.com"
```
---





