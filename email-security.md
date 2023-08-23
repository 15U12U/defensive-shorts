# Email Security Configuration Guide
## 1. SPF
### View SPF Record
```
nslookup -type=TXT example.com
nslookup -q=TXT example.com
dig TXT example.com
dig -t TXT example.com
dig TXT example.com @1.1.1.1
```
#### Example
```
$ nslookup -type=TXT google.com
google.com      text = "v=spf1 include:_spf.google.com ~all"
```
```
$ dig TXT google.com
google.com.             0       IN      TXT     "v=spf1 include:_spf.google.com ~all"
```
---


## 2. DKIM
### View DKIM Record
```
nslookup -type=TXT <selector>._domainkey.example.com
nslookup -q=TXT <selector>._domainkey.example.com
dig TXT <selector>._domainkey.example.com
dig -t TXT <selector>._domainkey.example.com
dig TXT <selector>._domainkey.example.com @1.1.1.1
```
#### Example
```
$ nslookup -type=TXT arcselector9901._domainkey.microsoft.com
arcselector9901._domainkey.microsoft.com        text = "v=DKIM1; k=rsa; p=MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAohCECx8ACVIj42taMc8G2ljiDmsboUW4mgasOg3/2Ay1D37DwK0CE1aok6x0x6dQ4FC/NGdeksPjT/ZLYH+zwwUvElJwd8adtZK4E7AT9Rzr6WPtTiFHi87em6n12HTvp8plpGHXnm8vdFrTxcCUguwUBzbe6MB12Dc3vSURcOUqfa6Dlj/6cNehl+PMonql" "LxOl2KmpTJ/Vy9jhdFOu50xEhXIT5ocOa4tX12hfoMpZfBW6iU5QIyvnEFkJuF8Ibs7Hhr7Ec1GZc6tgOd5uNTAnnvh+xiYs8e722H5iDecMsBzj+I9U+CBY1ACwY9hTC1UDNu3xS+WKQNgvnifdIQIDAQAB"
```
```
$ dig TXT arcselector9901._domainkey.microsoft.com
arcselector9901._domainkey.microsoft.com. 0 IN TXT "v=DKIM1; k=rsa; p=MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAohCECx8ACVIj42taMc8G2ljiDmsboUW4mgasOg3/2Ay1D37DwK0CE1aok6x0x6dQ4FC/NGdeksPjT/ZLYH+zwwUvElJwd8adtZK4E7AT9Rzr6WPtTiFHi87em6n12HTvp8plpGHXnm8vdFrTxcCUguwUBzbe6MB12Dc3vSURcOUqfa6Dlj/6cNehl+PMonql" "LxOl2KmpTJ/Vy9jhdFOu50xEhXIT5ocOa4tX12hfoMpZfBW6iU5QIyvnEFkJuF8Ibs7Hhr7Ec1GZc6tgOd5uNTAnnvh+xiYs8e722H5iDecMsBzj+I9U+CBY1ACwY9hTC1UDNu3xS+WKQNgvnifdIQIDAQAB"
```
---


## 3. DMARC
### View DMARC Record
```
nslookup -type=TXT _dmarc.example.com
nslookup -q=TXT _dmarc.example.com
dig TXT _dmarc.example.com
dig -t TXT _dmarc.example.com
dig TXT _dmarc.example.com @1.1.1.1
```
#### Example
```
$ nslookup -type=TXT _dmarc.google.com
_dmarc.facebook.com     text = "v=DMARC1; p=reject; rua=mailto:a@dmarc.facebookmail.com; ruf=mailto:fb-dmarc@datafeeds.phishlabs.com; pct=100"
```
```
$ dig TXT _dmarc.google.com
_dmarc.facebook.com.    0       IN      TXT     "v=DMARC1; p=reject; rua=mailto:a@dmarc.facebookmail.com; ruf=mailto:fb-dmarc@datafeeds.phishlabs.com; pct=100"
```
---





