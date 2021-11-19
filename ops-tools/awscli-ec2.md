## AWSCLI-EC2 Cheatsheet


### attach-volume
#### To attach a volume to an instance
```
aws ec2 attach-volume --volume-id vol-1234567890abcdef0 --instance-id i-01474ef662b89480 --device /dev/sdf
```

### copy-image
#### To copy an AMI to another region
```
aws ec2 copy-image --source-image-id ami-5731123e --source-region us-east-1 --region ap-northeast-1 --name "My server"
```

### create-image
#### To create an AMI from an Amazon EBS-backed instance without reboot
```
aws ec2 create-image \
    --instance-id i-0b09a25c58929de26 \
    --name "My server" \
    --no-reboot
```

### create-key-pair
#### To create a key pair
```
aws ec2 create-key-pair --key-name MyKeyPair
```

### request-certificate
#### Request a new certificate for the domain
Note: Idempotency tokens time out after one hour. Therefore, if you call RequestCertificate multiple times with the same idempotency token within one hour, ACM recognizes that you are requesting only one certificate and will issue only one. If you change the idempotency token for each call, ACM recognizes that you are requesting multiple certificates. 
```
aws acm request-certificate --domain-name example.com --validation-method DNS
aws acm request-certificate --domain-name example.com --validation-method EMAIL  \
--domain-validation-options DomainName=example.com,ValidationDomain=example.com
aws acm request-certificate --domain-name www.example.com --validation-method DNS --idempotency-token 91adc45q
```

#### Request a new certificate the domain with more subject alternative names using DNS validation
```
aws acm request-certificate --domain-name example.com --subject-alternative-names example.in --validation-method DNS
aws acm request-certificate --domain-name example.com \
--subject-alternative-names *.example.com *.example.in  --validation-method DNS
```
