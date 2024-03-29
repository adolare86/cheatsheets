## AWSCLI-EC2 Cheatsheet

### describe-instances
```
aws ec2 describe-instances \
    --region us-west-2 \
    --output text \
    --query 'Reservations[*].Instances[*].[Tags[?Key==`Name`].Value, InstanceType]' \
    | sed '$!N;s/\n/\t\t/'
aws ec2 describe-instances  \
    --region us-west-1 \
    --filters 'Name=tag:Name,Values=autoscaling-*' \
    --output text \
    --query 'Reservations[*].Instances[*].[PrivateIpAddress]'
# Find the ec2 classic instances    
  aws ec2 describe-instances \
      --region us-east-1  \
      --filters Name=instance-state-name,Values=pending,running,shutting-down,stopping,stopped \
      | jq '.Reservations[].Instances[] | select(.VpcId == null)' 
```

### Change attributes of Ec2 instance
```
aws ec2 modify-instance-attribute \
    --instance-id <instance id> \
    --no-ebs-optimized \
    --region us-west-1
```

### Volume
```
aws ec2 attach-volume \
    --volume-id vol-xxxxxxf0 \
    --instance-id i-xxxxx9480 \
    --device /dev/sdf
```

### Image
```
aws ec2 copy-image \
    --source-image-id ami-xxxxxx \
    --source-region us-east-1 \
    --region ap-northeast-1 \
    --name "test"
aws ec2 create-image \
    --instance-id i-0xxxxxxxxxx \
    --name "test" \
    --no-reboot
aws ec2 describe-images \
    --image-ids ami-xxxxxxxx \
    --query "Images[*].{State:State}" \
    --output text
```

### Key Pair
```
aws ec2 create-key-pair \
    --key-name MyKeyPair
```
