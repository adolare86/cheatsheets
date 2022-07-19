
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

### plan, apply, destroy
```
# Creates an execution plan
terraform plan

# Output the deployment plan to plan.out
terraform plan -out plan.out

# outputs a destroy plan
terraform plan -destroy

# Output the deployment plan to plan.out
terraform apply -out plan.out

# Apply changes without being prompted to enter “yes”
terraform apply --auto-approve

# Apply changes to the targeted resource/module
terraform apply -target=aws_instance.my_ec2
terraform apply -target=module.prod-alb

# Pass a variable via command-line
terraform apply -var region=us-east-1

# Disable resource refresh
terraform apply --refresh=false

# Execute number of simultaneous operations
terraform apply --parallelism=5
```

### fmt, validate, providers
```
# Format code per HCL canonical standard
terraform fmt

# Validate code for syntax
terraform validate

# Validate code skip backend validation
terraform -backend=false

# get provider's info
terraform providers
```

### workspace, state
```
# List workspaces
terraform workspace list

# Create a new workspace
terraform workspace new myworkspace

# Change the workspace
terraform workspace select myworkspace

# Show resource info in state file
terraform state show aws_instance.ec2

# Download state output in file
terraform state pull > terraform.tfstate

# List out all resources from state file
terraform state list

# Delete resource from stage file
terraform state rm  aws_instance.ec2
```

### import, output
```
# List out all outputs
terraform output
terraform output vpc_id
terraform output -json

# import existing ec2 instance as a teraform resource
terraform import aws_instance.new_ec2_instance i-xxxx1234
terraform import 'aws_instance.new_ec2_instance[1]' i-xxxx3444
```

### console, graph, taint
```
# verify expected result using console
echo 'join(",",["a","b","c"])' | terraform console
a,b,c
echo "aws_instance.ec2.public_ip" | terraform console
2x.44.22.5

# png diagram of resources
terraform graph | dot -Tpng > terraform.png

# Mark resource for recreation
terraform taint aws_instance.ec2

# Remove taint from resource
terraform untaint aws_instance.ec2
```
