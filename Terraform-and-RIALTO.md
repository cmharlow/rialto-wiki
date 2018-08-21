In order to set up our AWS infrastructure (networking, servers, access settings etc.) we use [Terraform](https://www.terraform.io/intro/index.html), a tool for cross platform [Infrastructure as Code](https://www.thoughtworks.com/insights/blog/infrastructure-code-reason-smile).

## Terraform-related repositories

* [terraform-aws](https://github.com/sul-dlss/terraform-aws/) - our main DLSS code repository (this should be your starting point)
* [terraform-module-aws-ecs](https://github.com/sul-dlss/terraform-module-aws-ecs) - [ECS](https://aws.amazon.com/ecs/) definitions
* [terraform-module-aws-network](https://github.com/sul-dlss/terraform-module-aws-network) - [VPC] (https://aws.amazon.com/vpc/)
* [terraform-module-aws-route53](https://github.com/sul-dlss/terraform-module-aws-route53) - [DNS](https://aws.amazon.com/vpc/)


## Terraform Workflow

After installing the Terraflow binary on your localhost, clone the terraform-aws repository and you're ready to start working. **When experimenting or building out new features, use the `development` organization**. The basic layout of the workflow is:

1. Make changes in the `development` organization.
2. Run `terraform init` if you have not already done so.
3. Run `terraform plan`.
4. If `terraform plan` succeeded, and its output looks sane, make AWS changes with `terraform apply`.

Unfortunately, many runtime errors do not appear until you run `terraform plan`.

For more information, see our DLSS-wide documentation in [Consul](https://consul.stanford.edu/display/dlssdevops/Terraform+and+AWS).