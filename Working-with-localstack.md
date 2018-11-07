# Comprehensive Setup for Localstack Development

see https://github.com/sul-dlss-labs/rialto-dev/

# Other resources

## Using Localstack for local AWS development

**NOTE:** some of this documentation has been adapted from [https://lobster1234.github.io/2017/04/05/working-with-localstack-command-line/](https://lobster1234.github.io/2017/04/05/working-with-localstack-command-line/)

### Requirements

* SNS Message Queue
* ES domain
* Lambda Function (to read message queue)
* The code and README in [https://github.com/sul-dlss/rialto/pull/103](https://github.com/sul-dlss/rialto/pull/103)

### SNS
#### Create a topic

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

#### Create the ElasticSearch domain
```
AWS_ACCESS_KEY_ID=999999 AWS_SECRET_ACCESS_KEY=1231 aws es \
--endpoint-url=http://localhost:4578 create-elasticsearch-domain \
--domain-name records \
--elasticsearch-version 6.2 \
--elasticsearch-cluster-config InstanceType=t2.small.elasticsearch,InstanceCount=1 \
--ebs-options EBSEnabled=true,VolumeType=standard,VolumeSize=10
```

#### Subscribe a lambda to a topic

**Note:** The topic-arn is the value from above

```
awslocal sns subscribe \
  --topic-arn arn:aws:sns:us-east-1:123456789012:test-topic \
  --protocol lambda \
  --notification-endpoint arn:aws:lambda:localstack:000000000000:function:f1
```

#### Publish a message to the SNS topic
```
awslocal sns publish --topic-arn arn:aws:sns:us-east-1:123456789012:test-topic --message 'Test Message!'
```

#### View the output
```
curl http://localhost:4571/records/_search
```

The output should look like:
```
{"took":3,"timed_out":false,"_shards":{"total":5,"successful":5,"failed":0},"hits":{"total":2,"max_score":1.0,"hits":[{"_index":"records","_type":"item","_id":"AWQaLSPcX7BG1AsnTYKW","_score":1.0,"_source":{"foo": "bar -- Test Message!"}},{"_index":"records","_type":"item","_id":"AWQaJQRQX7BG1AsnTYKU","_score":1.0,"_source":{"foo": "bar"}}]}}
```