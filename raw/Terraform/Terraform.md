Infra Orchestration vs Config Management - analogies below
	ansible vs terraform
	individual elements clothing, mats, utilities vs transport, hotel, tents
	terraform - deploy servers, ec2s
	ansible - config ec2 to run wordpress

terraform statefile
	Record of your existing infrastructure.
	Helps ensure idempotency -  everytime its run, it produces the same result, does not deploy resources multiple times.
	Desired state .tf vs. Current state .tfstate
		Desired state - contains changes and updates 
		Current state - contains the current/existing setup the resources

terraform workflow
	init - initialize terraform project folder
	validate - check syntax issues
	plan - compare current state with desired state
	apply - apply changes from current state
	destroy - destroy created resources

terraform import
	allows you to import existing resources using the resource id.
	Eliminates the need to delete existing resources to run terraform.
--
40

Variable hierarchy precedence
command line vars // -var
TF_VAR environment vars
.tfvars - vars defined in this file type
default values 

```
variables.tf — declares the variable, optionally with a default
variable "instance_type" {
  type    = string
  default = "t2.micro"      # <- the "Default Value"
}

terraform.tfvars — assigns a value, overriding the default
instance_type = "t3.small"
```

variable types
	list - contains items of a primitive type (string,number,bool)
	map - key value - like dict
	object - mulitple attr

