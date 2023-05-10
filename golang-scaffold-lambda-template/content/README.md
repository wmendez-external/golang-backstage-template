<div align="center">
  <img src="https://img.shields.io/badge/Go-00ADD8?style=for-the-badge&logo=go&logoColor=white" alt="golang">
  <a href="https://app.datadoghq.com/dashboard/mx2-xt5-aet?live=true"><img src="https://img.shields.io/badge/Dashboard-774aa4?style=for-the-badge&logo=datadog&logoColor=white" alt="datadog"></a>
  <a href="https://play-sistemico.atlassian.net/wiki/spaces/OB/pages/4380065814/ob-authorizer-function"><img src="https://img.shields.io/badge/Docs-172B4D?style=for-the-badge&logo=confluence&logoColor=white" alt="confluence"></a>
  <br>
  <a href="#"><img src="https://img.shields.io/badge/Prod-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white" alt="prod"></a>
  <a href="https://us-east-1.console.aws.amazon.com/lambda/home?region=us-east-1#/functions/TechLab-api-gw-authorizer?tab=code"><img src="https://img.shields.io/badge/Develop-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white" alt="develop"></a>
</div>
# ${{ values.name }}
${{ values.description }}

# Index

- Development
  - [Dependencies](#dependencies)
  - [Generate mocks](#generate-mocks)
  - [Run local](#run-local)
  - [Build](#build-and-zip)
  - [Upload to localstack](#upload-to-localstack)
  - [Environment variables](#environment-variables)
- Request examples
  - [Example local](#example-local)

---

### Dependencies

1. Docker
2. Localstack (`pip3 install localstack`)
3. AWS CLI (`pip3 install awscli`)
4. AWS CLI Local (`pip3 install awscli-local`)

---

### Generate mocks

```bash
mockery --all --inpackage
```

---

### Run local

1. Install dependencies
2. Start localstack service (`localstack start -d`)
3. Build and zip
4. Upload to localstack

---

### Build and zip

```bash
make build
```

### Upload to localstack

```bash
make deploy-local
```

_Tip: You can run both in a single line using `make build deploy-local`_

### Upload to development

```bash
make deploy-development
```

_Note: You must have an AWS profile named `ob-dev`._

### Environment variables

In AWS go to Lambda > Your function > Configuration > Environment variables.

```bash
VERSION=M.m.p
SERVICE_NAME=${{ values.name }}
ENVIRONMENT=<environment (dev,...)>
AUTHORIZER_TABLE = <DynamoDB table name>
AWS_DOMAIN = arn:aws:execute-api:us-east-1:<id>:<API Gateway ID>/<API Gateway deploy stage>/
```

---

### Example local

```bash
awslocal lambda invoke \
--function-name ${{ values.name }} \
--payload '{
    // put your payload here
}' \
/dev/stdout
```
