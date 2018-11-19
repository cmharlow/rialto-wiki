See the [README](https://github.com/sul-dlss-labs/rialto-trigger-rebuild/blob/master/README.md).

This ECS task is triggered on a schedule by CloudWatch Events to make sure derivative stores are in sync with the canonical data store.

## Manual Trigger of Task

1. Log into the AWS Console
1. Select "ECS" from services
1. Click into "Rialto-[environment]"
1. Click "Task Definitions"
1. Click the checkmark next to "rialto-rebuild" and from the Actions pulldown "Run Task"
1. Select "FARGATE"
1. Assign the environment VPC
1. Select a private subnet
1. Next to security groups click "EDIT"
1. Click "Select existing security group"
1. Select "rialto-rebuild-sg" and click "SAVE"
1. Then Click "Run Task"

Alternatively, in Terraform there is a script called post-run.sh in the rialto folder that will do this for you.