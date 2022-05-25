
## Terraform Cheatsheet


### init
```
# Initializes a working directory
terraform init

# Do not download plugins
terraform init -get-plugins=false

# Do not verify plugins for Hashicorp signature
terraform init -verify-plugins=false
```

### Plan, Apply, Destroy
```
# Creates an execution plan
terraform plan
# Output the deployment plan to plan.out
terraform plan -out plan.out
# outputs a destroy plan
terraform plan -destroy

```


