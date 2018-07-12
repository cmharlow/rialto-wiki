The dev instance of the RIALTO SPARQL Proxy is running as an AWS Lambda. See more in the [AWS Console](https://console.aws.amazon.com/lambda/home?region=us-east-1#/functions/sparqlProxy?tab=graph)

## Authorization

To access this lambda via API gateway, you need to pass an API key along with the request. See [[RIALTO Combine Core Integration]] for more details.

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

### Create an API Gateway endpoint for Lambda Execution

1. Create API
    1. API Name
    1. Endpoint Type => "Regional"
1. Create Method
    1. Actions pulldown => Create Method
    1. Select => (HTTP METHOD, i.e. POST), click check mark
1. HTTP METHOD SETUP
    1. Integration type => Lambda
    1. Lambda Region => us-east-1 (or appropriate region)
    1. Lambda Function => Name of function from above (will autocomplete)
    1. Save
1. HTTP METHOD - Method Execution
    1. **NOTE: This step is critical for passing the "raw" http data to the lambda.**
    1. Click the "Integration Request" header
    1. Select "Body Mapping Templates"
    1. Choose "When there are no templates defined (recommended)"
    1. Click "Add Mapping template"
    1. Enter the http content type (i.e. application/x-www-form-urlencoded) - click check mark
    1. In the text area:
```
{
    "body": $input.json('$')
}
```
1. Actions => Deploy API
    1. **NOTEs:**
        1. API Gateway Endpoints are NOT available until they have been "deployed"
        1. Any changes to API Gateway configuration require a redeploy
    1. Deployment state => "<endpoint name>" (this is the end of the url: http://...../<endpoint name>
