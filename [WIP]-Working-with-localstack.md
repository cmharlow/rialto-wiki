# Using Localstack for local AWS development

**NOTE:** some of this documentation has been adapted from [https://lobster1234.github.io/2017/04/05/working-with-localstack-command-line/](https://lobster1234.github.io/2017/04/05/working-with-localstack-command-line/)

## SNS
### Create a topic

```
bash-3.2$ awslocal sns list-topics
{
    "Topics": []
}

bash-3.2$ awslocal sns create-topic --name test-topic
{
    "TopicArn": "arn:aws:sns:us-east-1:123456789012:test-topic"
}
bash-3.2$ awslocal sns list-topics
{
    "Topics": [
        {
            "TopicArn": "arn:aws:sns:us-east-1:123456789012:test-topic"
        }
    ]
}
```

### Subscribe a lambda to a topic

```
awslocal sns subscribe \
  --topic-arn arn:aws:sns:us-east-1:123456789012:test-topic \
  --protocol lambda \
  --notification-endpoint arn:aws:lambda:localstack:000000000000:function:f1
```