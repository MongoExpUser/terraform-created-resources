#
# Terraform-Created-Resources

<strong>Terraform module for creation of resources on public cloud platforms.</strong>
<br>

The following public cloud platforms and resources are currently covered:
1) <strong>```AWS```</strong> - EC2 and Lightsails instances (VMs) with Node.js, MongoDB and MySQL installations
2) <strong>```Linode```</strong> - Linode instances (VMs) with Node.js and MongoDB installations.


This repo is based on <strong>```Terraform Version 0.12.24```</strong>.

## RUNNING MODULE

A) <strong>To run the module to create resources on ```AWS```</strong>:

1) Save or download the start-up bash file(s) in the link(s) below to the current working directory (CWD): <br>
   a) https://raw.githubusercontent.com/MongoExpUser/Terraform-Created-Resources/master/init_web_server.sh <br>
   b) https://raw.githubusercontent.com/MongoExpUser/Terraform-Created-Resources/master/init_mongodb_server.sh <br>
   c) https://raw.githubusercontent.com/MongoExpUser/Terraform-Created-Resources/master/init_mysql_server.sh

2) Also, copy the following script into a file (base.tf) in the current working directory:

```hcl
# define provider(s) credential variables
variable "aws_access_key" {}
variable "aws_secret_key" {}
variable "aws_region" {}

provider "aws" {
  access_key = var.aws_access_key
  secret_key = var.aws_secret_key
  region     = var.aws_region
}

module "public_cloud_resources" {
  source = "git::https://github.com/MongoExpUser/Terraform-Created-Resources.git"
}

output "ec2_web_server_instances" {
  description = "A list of all created EC2 web server instances"
  # the list contains key-value pairs of each instance's attributes
  value = module.public_cloud_resources.aws_ec2_web_servers
}

output "ec2_db_server_instances" {
  description = "A list of all created EC2 db server instances"
  # the list contains key-value pairs of each instance's attributes
  value = module.public_cloud_resources.aws_ec2_db_servers
}

output "lightsail_web_server_instances" {
  description = "A list of all created AWS lightsail web server instances"
  # the list contains key-value pairs of each instance's attributes
  value = module.public_cloud_resources.aws_lightsail_web_servers
}

output "lightsail_db_server_instances" {
  description = "A list of all created AWS lightsail db server instances"
  # the list contains key-value pairs of each instance's attributes
  value = module.public_cloud_resources.aws_lightsail_db_servers
}

output "lightsail_web_server_static_ips" {
  description = "A list of all created AWS lightsail static ips"
  # the list contains key-value pairs of each instance's attributes
  value = module.public_cloud_resources.aws_lightsail_web_server_static_ips
}

output "lightsail_db_server_static_ips" {
  description = "A list of all created AWS lightsail static ips"
  # the list contains key-value pairs of each instance's attributes
  value = module.public_cloud_resources.aws_lightsail_db_server_static_ips
}

```


3) Finally, execute the module from the base file (base.tf) in the current working directory (CWD) by typing the following commands at the prompt (assuming running via <strong>```bash```</strong>  with <strong>```sudo```</strong> access):


```bash
  #1) run init
  sudo terraform init
  
  #2) run terraform plan
  sudo TF_VAR_aws_access_key="access-key-value" \
       TF_VAR_aws_secret_key="secret-key-value" \
       TF_VAR_aws_region="aws-region-value" \
       terraform plan
                                                                                    
  #3) run terraform apply 
  sudo TF_VAR_aws_access_key="access-key-value" \
      TF_VAR_aws_secret_key="secret-key-value" \
      TF_VAR_aws_region="aws-region-value" \
      terraform apply
```

# License

Copyright © 2015 - present. MongoExpUser

Licensed under the MIT license.
