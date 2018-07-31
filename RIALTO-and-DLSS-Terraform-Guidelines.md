We prefer to use the open source [Terraform](https://www.terraform.io/docs/index.html) tool to define our Amazon Web Service [infrastructure as code](https://www.thoughtworks.com/insights/blog/infrastructure-code-reason-smile). Terraform can work with all the major cloud computing providers, not just AWS.

## Modules

In Terraform, [modules](https://www.terraform.io/docs/modules/index.html) are essentially special directories that let you group together infrastructure definitions in order to reuse them later. The recommended structure for a module is laid out [here](https://www.terraform.io/docs/modules/create.html#standard-module-structure).

At DLSS, we observe the following guidelines regarding modules:

* When writing significant chunks of Terraform code, organize them in modules whenever possible.
* Consider breaking modules up into stand-alone GitHub repositories for versioning, for example the [terraform-aws-lambda repository](https://github.com/sul-dlss-labs/terraform-aws-lambda), which is used to create lambda functions.

