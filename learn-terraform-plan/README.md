# Create a Terraform Plan

This repo is a companion repo to the [Create a Terraform Plan](https://developer.hashicorp.com/terraform/tutorials/cli/plan) tutorial.
It contains Terraform configuration you can use to learn how Terraform generates an execution plan.

```bash
terraform show "tfplan"
terraform show -json "tfplan" | jq > tfplan.json
jq '.terraform_version, .format_version' tfplan.json
jq '.configuration.provider_config' tfplan.json
jq '.configuration.root_module.resources' tfplan.json
jq '.configuration.root_module.module_calls' tfplan.json
jq '.configuration.root_module.module_calls.hello.expressions.hellos.references' tfplan.json
jq '.resource_changes[] | select( .address == "module.ec2-instance.aws_instance.main")' tfplan.json
jq '.planned_values' tfplan.json


terraform plan -out "tfplan-input-var"
terraform show -json tfplan-input-var | jq > tfplan-input-var.json
jq '.variables' tfplan-input-var.json
jq '.prior_state' tfplan-input-var.json
jq '.resource_changes[] | select( .address == "module.hello.random_pet.server")' tfplan-input-var.json

```