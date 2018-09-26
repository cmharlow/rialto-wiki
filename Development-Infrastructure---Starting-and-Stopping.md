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

## Option 1 - Create a snapshot on shutdown

### Remove prior development snapshot(s)

Terraform will error out if the `final-snapshot-identifier` already exists. 

1. Log into AWS Console
1. Select RDS
1. Click Snapshots
1. Select Snapshot (`rialto-development-rds-hold`)
1. Actions > Delete snapshot
1. Select Neptune
1. Click Snapshots
1. Select Snapshot (`rialto-development-neptune-hold`)
1. Actions > Delete snapshot

### Edit rialto-rds.tf

#### Under resource > aws_db_instance > rialto_db_instance
```
  skip_final_snapshot       = false
  ...
  final_snapshot_identifier = "rialto-development-rds-hold"
```

### Edit rialto-neptune.tf

```
   TBD
```

### Destroy infrastructure

```
terraform destroy
```

## Option 1 - Manually create snapshot(s) before shutdown

1. Log into AWS Console
1. Select RDS
1. Select Instance `rialto-development-rds`
1. Create Snapshot
    1. Instance actions
    1. Take snapshot
    1. Enter a snapshot name (i.e. `rialto-development-rds-hold`)
1. Select Neptune
1. Select Instance `rialto-dev`
1. Create Snapshot
    1. Instance actions
    1. Take snapshot
    1. Enter a snapshot name (i.e. `rialto-development-neptune-hold`)

# Rebuild from snapshots

TBD
