---
layout: post
title:  "Terraform101"
date:   2021-09-08 15:00:00 +0700
categories: devops
tags: [devops, terraform]
---

## Terraform
Terraform is Infrastruture as Code(IaC) tool that provoides ablity to manage using declarative configuration files(.tf). It helps manage and contol infrastruture configuration.

## Terminology
Plan : "terraform plan" will check actual against configuration file and produce changes that will apply later
Apply : "terraform apply" will do actual provisioning as proposed in planning

## Resources Block
Resource is the most basic and important block. This respresent resource on cloud server and its properties.
example
```
resource "aws_instance" "web" {
    ami           = "ami-005e54dee72cc1d00"
    instance_type = "t2.micro"
}
```

## Providers
Providers are plugin that helps Terraform interact with cloud providers. Available providers is shown in Terraform Registry

## Inputs and Outputs
- Input variables : like function arguments.
```
variable "instance_type" {
  description = "type of EC2 instance to provision."
  default = "t2.micro"
}

to use in resource block
-> instance_type = ${var.instance_type}
```
- Output variables : like return values. They is used for further required resource. For example, create virsual network and return ID to use for provision VM later on.
```
output "public_dns {
    value = "${aws_instance.web.public_dns}"
}
```

### Terraform Backend
Settings regard Terraform itself lies in here. The most important one is backend setting. For learning and tutorial, we can use local to store the state file. For production use, it's recommended to store in remote backend instead such as S3(AWS), Storage account(Azure).
```
terraform {
    ...
}
```

### Standard Module Structure
- main.tf : declear resource block
- variables.tf : declear variable to pass to main file
- outputs.tf : define the output of this module to let another module use later on or just to log

## Alternative
AWS CloudFormation
