# Windows DNS Analytical Logs
## 1. Enable Windows DNS Analytical Logs




## 2. Decode 'PavcketData' in Windows DNS Analytical Logs

```python
#!/usr/bin/env python3

import binascii
from dnslib import *

packetData = input("Please input the PacketData section of the Log:\n")
byte_packetData = packetData.encode('utf-8')
packet = binascii.unhexlify(byte_packetData)
dnsRecord = DNSRecord.parse(packet)
print(f"\nDecoded Data:\n\n"+ str(dnsRecord))

```

### Example Output
```
Please input the PacketData section of the Log:
D74F8180000100010000000003646E73086D7366746E63736903636F6D00001C0001C00C001C00010000066A0010FD3E4F5A5B8100000000000000000001

Decoded Data:

;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 55119
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0
;; QUESTION SECTION:
;dns.msftncsi.com.              IN      AAAA
;; ANSWER SECTION:
dns.msftncsi.com.       1642    IN      AAAA    fd3e:4f5a:5b81::1
```

