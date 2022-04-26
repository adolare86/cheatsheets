
## Openssl Cheatsheet


### Create
```
# Create RSA Private Key
openssl genrsa -out private.key 2048

# Create a CSR from existing private key.
openssl req -new -key example.key -out example.csr -sha256
openssl req -nodes -newkey rsa:2048 -keyout example.key -out example.csr

# Create a Self-Signed Certificate
openssl req -x509 -sha256 -nodes -days 730 -newkey rsa:2048 -keyout private.key -out example.pem
```

### Verify
```
# Verify if the particular cipher is accepted on URL
openssl s_client -cipher 'ECDHE-ECDSA-AES256-SHA' -connect secureurl:443

# Check a certificate and return information about it (signing authority, expiration date, etc.):
openssl x509 -in server.crt -text -noout

# Check the SSL key and verify the consistency:
openssl rsa -in server.key -check

# Verify the CSR and print CSR data filled in when generating the CSR:
openssl req -text -noout -verify -in server.csr

# Verify a certificate and key matches
# These two commands print out md5 checksums of the certificate and key; the checksums can be compared to verify that the certificate and key match.
openssl x509 -noout -modulus -in server.crt| openssl md5
openssl rsa -noout -modulus -in server.key| openssl md5

```

### Check
```
# Check Certificate Expiration Date of SSL URL
openssl s_client -connect google.com:443 2>/dev/null | openssl x509 -noout -enddate

# Check PEM File Certificate Expiration Date
openssl x509 -noout -in cert.pem -dates

# Validate if SSL V3 is enabled or not
openssl s_client -connect secureurl.com:443 –ssl3

# To Check TLS 1.0
openssl s_client -connect secureurl.com:443 –tls1

To Check TLS 1.1
openssl s_client -connect secureurl.com:443 –tls1_1

To Check TLS 1.2
openssl s_client -connect secureurl.com:443 –tls1_2

```

### Convert
```
# Convert PKCS12 format to PEM certificate
openssl pkcs12 –in cert.p12 –out cert.pem

# Convert Certificate and Private Key to PKCS
openssl pkcs12 –export –out sslcert.pfx –inkey key.pem –in sslcert.pem

# Convert PEM to DER format
openssl x509 –outform der –in sslcert.pem –out sslcert.der

# Convert DER to PEM format
openssl x509 –inform der –in sslcert.der –out sslcert.pem
```

