# Certificate/Key Extensions

| Extension | Description                                                                                                                                                                                                               | Private Key        | Public Key         | Certificate        |
|:----------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------:|:------------------:|:------------------:|
| .pem      | Privacy Enhanced Mail Certificate. A PEM file is Base64 encoded and may be an X.509 certificate file, a private key file, or any other key material. PEM encoded files are commonly used in Apache and Tomcat servers. | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| .crt      | Shorthand way to say “cert”, the .crt file extension is a security extension that may be either Base64 encoded or binary. Most commonly, .crt is a Base64 encoded certificate.                                          | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| .cer      | Shorthand way to almost say “cert”, the .cer file extension is an Internet Security Certificate that may be either Base64 encoded or binary. Most commonly, .cer is a binary certificate.                                 | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| .cert     |                                  | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| .der      | The .der file extension is for a certificate file in binary format.                                                                                                                                                       |
| .pfx      | The .pfx file extension is a PKCS12 certificate bundle which may contain an end entity certificate, a certificate chain, and matching private key. .pfx can be interchanged with .p12 and may be protected by a password. | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| .p12      | Personal Information Exchange File that is encrypted with a password and is interchangeable with the .pfx file extension.                                                                                                 | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| .pkcs12   | | |  |  |
| .jks      | Java Keystore File. A file encrypted with a password used in a Java program. Similar to the .p12 file, but .jks is considered proprietary.                                                                               | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |
| .p7b      |                                                                                                                                                                                                                           | :x:                | :x:                | :heavy_check_mark: |
| .ppk      | PuTTY Private Key File. This is a private key file created by the putty key generator used for ssh.                                                                                                                       | :heavy_check_mark: | :x:                | :x:                |
| .key      | Private/Public Keys in PEM Format.                                                                                                                                                                                       | :heavy_check_mark: | :heavy_check_mark: | :x:                |
| .csr      |                                                 | :x:                | :heavy_check_mark: | :x:                |

## Conversions

| Conversion   | Command              | Remarks                               |
|--------------|----------------------|---------------------------------------|
| .pem -> .crt | mv cert.pem cert.crt | .crt will be in Base64 encoded format |
| .crt -> .pem | mv cert.crt cert.pem |                                       |
|              |                      |                                       |
|              |                      |                                       |
|              |                      |                                       |
|              |                      |                                       |
|              |                      |                                       |
|              |                      |                                       |

# Public Root Certificate Locations in Linux/Unix

| OS                                | Location                         |
| :-------------------------------- | :------------------------------- |
| Debian/Ubuntu/Gentoo/FreeBSD/SLES | /etc/ssl/certs/                  |
| Fedora/RHEL 6                     | /etc/pki/tls/certs/              |
| CentOS/RHEL 7                     | /etc/pki/ca-trust/extracted/pem/ |
| OpenSUSE/Alpine Linux             | /etc/ssl/                        |
| Android                           | /system/etc/security/cacerts/    |
| NetBSD                            | /etc/openssl/certs/              |
| AIX                               | /var/ssl/certs/                  |
| Solaris                           | /etc/sfw/openssl/                |


# Check/Verify details of a Certificate
```bash
openssl x509 -in <cert> -text -noout
```

# Check/Verify Public Key by generating the Hash
```bash
openssl pkey -pubout -in <private-key> | openssl sha256
openssl req -pubkey -in <csr> -noout | openssl sha256
openssl x509 -pubkey -in <certificate> -noout | openssl sha256
```
### Example
```bash
openssl pkey -pubout -in pvt-key.key | openssl sha256
openssl req -pubkey -in CSR.csr -noout | openssl sha256
openssl x509 -pubkey -in cert.crt -noout | openssl sha256
```
