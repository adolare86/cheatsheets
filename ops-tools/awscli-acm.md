## AWSCLI-ACM Cheatsheet

Use AWS Certificate Manager (ACM) to manage SSL/TLS certificates for AWS-based websites and applications.

### delete-certificate
#### To delete an ACM certificate from your account
```
aws acm delete-certificate --certificate-arn arn:aws:acm:us-east-1:123456789012:certificate/12345678-1234-1234-1234-123456789012
```

### get-certificate
#### To retrieve an ACM certificate
```
aws acm get-certificate --certificate-arn arn:aws:acm:us-east-1:123456789012:certificate/12345678-1234-1234-1234-123456789012
```

### import-certificate
#### Import certificate in ACM
```
domain=${1}
region=${2}
acm_arn=$(aws acm list-certificates --region ${region} | \
        jq -jr  '.CertificateSummaryList[] | select(.DomainName == "'${domain}'") | .CertificateArn')

aws acm import-certificate --certificate-arn  ${acm_arn}  --certificate  file:///etc/letsencrypt/live/${domain}/cert.pem --private-key   file:///etc/letsencrypt/live/${domain}/privkey.pem --certificate-chain file:///etc/letsencrypt/live/${domain}/fullchain.pem
```

### list-certificates
####
```
aws acm list-certificates --region us-east-1| jq -r '.CertificateSummaryList[] | [.CertificateArn, .DomainName] | @tsv '
```

### request-certificate
#### Request a new certificate for the domain
Note: Idempotency tokens time out after one hour. Therefore, if you call RequestCertificate multiple times with the same idempotency token within one hour, ACM recognizes that you are requesting only one certificate and will issue only one. If you change the idempotency token for each call, ACM recognizes that you are requesting multiple certificates. 
```
aws acm request-certificate --domain-name example.com --validation-method DNS
aws acm request-certificate --domain-name example.com --validation-method EMAIL  --domain-validation-options DomainName=example.com,ValidationDomain=example.com
aws acm request-certificate --domain-name www.example.com --validation-method DNS --idempotency-token 91adc45q
```

#### Request a new certificate the domain with more subject alternative names using DNS validation
```
aws acm request-certificate --domain-name example.com --subject-alternative-names example.in --validation-method DNS
aws acm request-certificate --domain-name example.com --subject-alternative-names *.example.com *.example.in  --validation-method DNS
```
