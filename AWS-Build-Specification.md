The canonical AWS build specification for RIALTO lives in our [Terraform repository](https://github.com/sul-dlss/terraform-aws).

**This page is largely out of date, replaced by the aforementioned Terraform definitions.**

Here are some notes that may help building out our Terraform work.

# Region

`us-east-1` (changing to `us-west-2`)

# VPCs 

https://github.com/sul-dlss/rialto/wiki/Neptune-Lambda-Integration  
`rialto-core` VPC

# Security Groups

`rialto-core` VPC

# CloudWatch

https://github.com/sul-dlss-labs/rialto-trigger-rebuild#add-schedule-event

# API Gateway 

https://github.com/sul-dlss/rialto/wiki/RIALTO-Combine-Core-Integration  
each lambda has its own api gateway, and each gateway has a dedicated api key and usage plan for rialto-internal usage

# Lambda

All lambdas use same `RialtoLambda` execution role  
`sparqlProxy` lambda has one trigger: its API Gateway  
`derivatives` lambda has one trigger: SNS  
`triggerRebuild` lambda has two triggers: its API Gateway, and CloudWatch Events (for scheduled/cron use case)  
We use CircleCI/GitHub integration to automatically deploy lambdas to AWS.  

# EC2

one instance running ingest service  
one instance running solr  
both using same VPC and Security Group  

# Neptune

1 cluster containing 1 instance of class db.r4.xlarge  
running within same VPC and using same Security Group as above

# SNS 

Create one topic per environment (dev/stage/prod) which serves as the backbone/messaging bus for the components