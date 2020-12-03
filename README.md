# aws-sandbox
[![Docker version https://docs.docker.com/engine/install/ubuntu/](https://img.shields.io/badge/docker-19.03.11-blue)](https://docs.docker.com/engine/install/ubuntu/)
[![Docker-Compose version https://docs.docker.com/compose/install/](https://img.shields.io/badge/docker--compose-1.17.1-9cf)](https://docs.docker.com/compose/install/)
[![License](https://img.shields.io/pypi/l/localstack.svg)](https://img.shields.io/pypi/l/localstack.svg)

This project uses localstack that provides an [easy-to-use test/mocking framework for developing cloud applications](https://github.com/localstack/localstack).
One important point to remember following the next instructions until the example, is that localstack does not deploying any aws service in the local machine, it emulates the API transaction. 

## How it works

This repository is focused on create the sandbox using `docker-compose` and `aws cli`. So the requirements are:

- [docker](https://docs.docker.com/engine/install/ubuntu/)
- [docker-compose](https://docs.docker.com/compose/install/)
- [aws-cli](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)

## Usage
**Starting the container**:

```zsh
docker-compose up
```
**Checking health**: `curl http://localhost:4566/health` should return:
``` json
{
  "services": {
    "cloudformation": "running",
    "cloudwatch": "running",
    "ec2": "running",
    "iam": "running",
    "sts": "running",
    "lambda": "running",
    "logs": "running",
    "s3": "running",
    "sqs": "running",
    "events": "running",
    "apigateway": "running"
  }
}
```
**Set up your credentials** via: [aws configure](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html#cli-configure-quickstart-config).

And finally you can **start emulating api transactions:**

```bash
aws --endpoint-url=http://localhost:4566/ ec2 run-instances \
--image-id ami-123456 --instance-type t2.micro --key-name \
randkey --region us-east-1
```
## Contributing
Pull requests are welcome.

