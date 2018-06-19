# Using Localstack for local AWS development

**NOTE:** some of this documentation has been adapted from [https://lobster1234.github.io/2017/04/05/working-with-localstack-command-line/](https://lobster1234.github.io/2017/04/05/working-with-localstack-command-line/)

## SNS
### Create a topic

```
bash-3.2$ aws --endpoint-url=http://localhost:4575 sns list-topics
{
    "Topics": []
}

bash-3.2$ aws --endpoint-url=http://localhost:4575 sns create-topic --name test-topic
{
    "TopicArn": "arn:aws:sns:us-east-1:123456789012:test-topic"
}
bash-3.2$ aws --endpoint-url=http://localhost:4575 sns list-topics
{
    "Topics": [
        {
            "TopicArn": "arn:aws:sns:us-east-1:123456789012:test-topic"
        }
    ]
}
```