## AWSCLI-EC2 Cheatsheet

### describe-instances
```
aws ec2 describe-instances  --region us-west-2 --output text --query 'Reservations[*].Instances[*].[Tags[?Key==`Name`].Value, InstanceType]'  | sed '$!N;s/\n/\t\t/'
aws ec2 describe-instances  --region us-west-1 --filters 'Name=tag:Name,Values=autoscaling-*' \
  --output text --query 'Reservations[*].Instances[*].[PrivateIpAddress]'
```

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
