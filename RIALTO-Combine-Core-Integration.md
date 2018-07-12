RIALTO Combine can connect to RIALTO Core APIs, such as the [SPARQL Proxy](https://github.com/sul-dlss/rialto/wiki/RIALTO-SPARQL-Proxy-Lambda-(Dev-Env)), by hitting HTTP endpoints exposed by [API Gateway](https://aws.amazon.com/api-gateway/) ([AWS console](https://console.aws.amazon.com/apigateway/home?region=us-east-1#/apis)).

To secure these endpoints, AWS provides a number of [mechanisms](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-control-access-to-api.html). For simplicity's sake, we have chosen to use API keys, and we're storing these in [shared_configs](https://github.com/sul-dlss/shared_configs/blob/rialto-etl-prod/config/settings/production.yml). Pass the appropriate API key to the endpoint as a header named `X-API-Key`, e.g.:

```shell
curl -i -H 'X-API-Key: API_KEY_VALUE' https://RESOURCE_IDENTIFIER.execute-api.AVAILABILITY_ZONE.amazonaws.com/STAGE_NAME
```