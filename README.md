# aws-sandbox

This project uses localstack that provides an [easy-to-use test/mocking framework for developing cloud applications](https://github.com/localstack/localstack).
One important point to remember following the next instructions until the example, is that localstack does not deploying any aws service in the local machine, it emulates the API transaction. 

## How it works

- [docker-compose](https://docs.docker.com/compose/install/)
- [aws-cli](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)

## Usage
**Starting the container**:

```zsh
docker-compose up
```
**Checking available services**: `curl http://localhost:4566/health` should return:
``` json
{
  "services": {
    "acm": "available",
    "apigateway": "available",
    "cloudformation": "available",
    "cloudwatch": "available",
    "config": "available",
    "dynamodb": "available",
    "dynamodbstreams": "available",
    "ec2": "available",
    "es": "available",
    "events": "available",
    "firehose": "available",
    "iam": "available",
    "kinesis": "available",
    "kms": "available",
    "lambda": "available",
    "logs": "available",
    "opensearch": "available",
    "redshift": "available",
    "resource-groups": "available",
    "resourcegroupstaggingapi": "available",
    "route53": "available",
    "route53resolver": "available",
    "s3": "available",
    "s3control": "available",
    "secretsmanager": "available",
    "ses": "available",
    "sns": "available",
    "sqs": "available",
    "ssm": "available",
    "stepfunctions": "available",
    "sts": "available",
    "support": "available",
    "swf": "available",
    "transcribe": "available"
  },
  "version": "2.0.3.dev"
}
```
**install aws cli** via: [aws configure](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html#cli-configure-quickstart-config).

And finally you can **start emulating api transactions:**

```bash
aws --endpoint-url=http://localhost:4566/ ec2 run-instances \
--image-id ami-123456 --instance-type t2.micro --key-name \
randkey --region us-east-1
```

