The dev instance of the RIALTO SPARQL Proxy is running as an AWS Lambda. See more in the [AWS Console](https://console.aws.amazon.com/lambda/home?region=us-east-1#/functions/sparqlProxy?tab=graph)

## In the AWS Console

### Create a new Lambda Function

1. Create Function
  1. Name
  1. Runtime => Go 1.x
  1. Role => "Choose an existing role"
  1. Existing Role => RialtoLambda
1. Configuration
  1. Designer - used to setup triggers... TBD
  1. Function Code => Upload the ZIP file created for the Lambda
    1. Runtime (verify set to Go 1.x)
    1. Handler => "main"
  1. Environment variables
  1. Tags => N/A
  1. Execution Role (Verify set to "RialtoLambda")
  1. Network
    1. Select "vpc-xxx | rialto-core"
    1. Subnets
    1. Security Groups => " ... | rialto-core"
  1. Execution Role 

MORE HERE