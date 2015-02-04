tf_aws_sg aka the terraform_module_aws_security_group
===================================

A Terraform module which contains a number of common configurations for AWS security groups.
* It assumes you're putting your SGs in a VPC.

Security Group Catalog
----------------------

This module contains the following security group templates for you to use as modules in
service Terraform templates.

- `sg_common` - this is a security group that all systems should use. It is usually included in
     the other modules.
    - It allows incoming TCP 22 (SSH)
- `sg_web` - this is a security group for web applications
    - It allows incoming TCP 80 (HTTP), TCP 443 (HTTPS), TCP 8080 (HTTP/S), TCP 1099 (JMX)
- `sg_zookeeper` - this is a security group for web applications
    - It Allows incoming TCP 2181, TCP 2888, TCP 3888, TCP 7199 (Used for zk JMX)

Usage
------

You can use these in your terraform template with the following steps. 

1. Adding a module resource to your template, e.g. `main.tf`

```
module "sg_web" {
  source = "github.com/solarce/tf_aws_sg//sg-web"
  security_group_name = "${var.security_group_name}-web"
  aws_access_key = "${var.aws_access_key}"
  aws_secret_key = "${var.aws_secret_key}"
  aws_region = "${var.aws_region}"
  vpc_id = "${var.vpc_id}"
  source_cidr_block = "${var.source_cidr_block}"
}
``` 

2. Setting values for the following variables, either through `terraform.tfvars` or `-var` arguments on the CLI

- aws_access_key
- aws_secret_key
- aws_region
- security_group_name
- vpc_id
- source_cidr_block