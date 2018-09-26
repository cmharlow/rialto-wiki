# Introduction

Our AWS development best practices expect that the development infrastructure is not left to run when not actively being used. Specifically weekends, but also overnight (especially if utilizing any expensive resources). This is largely for cost concerns as we can minimal the cost of our infrastructure by not only shutting down resources, but removing them when not in use.

The purpose of this document is to walk through building the infrastructure using terraform, shutting down the infrastructure in a manner that allows for recreation with minimal to no loss of data.

# Startup

## Clone the TERRAFORM-AWS repository

```
git clone https://github.com/sul-dlss/terraform-aws.git
```

## Get the RIALTO-DEV branch

```
cd terraform-aws
git checkout rialto-dev
git pull
``` 

## All commands must be run in the rialto path

```
cd organizations/development/rialto
```

## Initialize terraform

```
terraform init
```

## Review the terraform plan

```
terraform plan
```

Note: If this is an initial startup or startup after a shutdown, you should see well over 100 resources in the "To add" category.

## Apply the terraform plan

```
terraform apply
```

Note: It is common to see errors in terraform that are related to dependency between resources and modules. Attempt to run `terraform apply` more than once to try to clear errors.

# Shutdown

```
terraform destroy
```

# Rebuild from snapshots

