# Overview

- AWS CLI is built on top of `botocore` low-level Python SDK
    + https://botocore.amazonaws.com/v1/documentation/api/latest/index.html
- https://docs.aws.amazon.com/cli/
- https://aws.amazon.com/cli/
- https://github.com/aws/aws-cli

- Set up auto completion for AWS CLI:
    + https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-completion.html

# Authentication and access credentials

- https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-authentication.html
- Configuration and credential precedence (provider chain)
    + Command line options
    + Environment variables
    + Assume role
    + Assume role with web identity
    + AWS IAM Identity Center (successor to AWS SSO)
    + Credentials file: `~/.aws/credentials`
    + Custom process
    + Configuration file: `~/.aws/config`
    + Amazon EC2 instance profile credentials
    + Container credentials

# Global options

- `--no-cli-pager`: turn off the pager for AWS CLI return value
  (response).
- `--cli-binary-format <string>`
    + The formatting style to be used for binary blobs. The default
      format is base64. The base64 format expects binary blobs to be
      provided as a base64 encoded string. The raw-in-base64-out format
      preserves compatibility with AWS CLI V1 behavior and binary values
      must be passed literally. When providing contents from a file that
      map to a binary blob fileb:// will always be treated as binary and
      use the file contents directly regardless of the cli-binary-format
      setting. When using file:// the file contents will need to
      properly formatted for the configured cli-binary-format.
- `--profile <string>`: Use a specific profile from your credential file.
- `--region <string>`: The region to use. Overrides config/env settings.

# How to use?

## Specify Parameter Values

- JSON
    + `--option file://value.json`
- Shorthand

```
aws ecs update-cluster \
--cluster IPCSimInventoryTransferServiceTI-EcsCluster-gamma-ClusterEB0386A7-MRWTVrdXp7j5 \
--configuration 'executeCommandConfiguration={logging=DEFAULT}'
```

# Lambda

- List all Lambda function that has runtime is Python 3.6
    + `aws lambda list-functions --function-version ALL --region us-east-1 --output text --query "Functions[?Runtime=='python3.6'].FunctionArn"`
- Delete a event source mapping
    + `aws lambda delete-event-source-mapping --uuid 36e0122a-c9d7-49c3-86c3-0379c0d4b177 --region us-east-1 --profile sandop-labor-plan-gamma`

# Secret Manager (secretmanager)

- Create your secret in a file, e.g., `mycreds.json`

```json
{
    "username": "myusername",
    "password": "mypassword"
}
```

- Store your values

```bash
aws secretsmanager create-secret --name MyRedshiftSecret  --tags Key="RedshiftDataFullAccess",Value="serverless" --secret-string file://mycreds.json
```

- The response from the above command

```json
{
    "ARN": "arn:aws:secretsmanager:region:accountId:secret:MyRedshiftSecret-mvLHxf",
    "Name": "MyRedshiftSecret",
    "VersionId": "a1603925-e8ea-4739-9ae9-e509eEXAMPLE"
}
```

# API Gateway

## Data Actuals

```
# Get API
aws apigateway test-invoke-method --region us-west-2 --profile trnso-dev --rest-api-id u60mdlkbd7 --resource-id fb9w99 --http-method POST --path-with-query-string '/US/metric/Inventory/PRODUCTLINE-SORTTYPE-WAREHOUSE/DAILY' --body file://us-fullcase-get.json

# PayloadBasedGet API
aws apigateway test-invoke-method --region us-west-2 --profile trnso-dev --rest-api-id u60mdlkbd7 --resource-id q3sy9c --http-method POST --body file://jp-payloadGet.json

# Put API
aws apigateway test-invoke-method --region us-west-2 --profile trnso-dev --rest-api-id u60mdlkbd7 --resource-id ruwd7k --http-method PUT --path-with-query-string '/JP/metric/TransferInReceipts/PRODUCTLINE-SORTTYPE-WAREHOUSE/WEEKLY/2023-03-12?replace=false&namespace=Default&clientInfo=trnso' --body file://jp-put.json

aws apigateway test-invoke-method --region us-east-1 --profile sandop-data-actuals-prod --rest-api-id pki018cv5j --resource-id 0llo8m --http-method POST --body file://us-fullcase-payloadBasedGet.json

```

- Get API

```json
{
    "periodStartDate": "2023-03-19",
    "periodEndDate": "2023-04-04",
    "groupBy": ["periodStartDate"],
    "filters": {
        "productLine": ["Amazon Digital Products 21 Accessory"],
        "sortType": ["fullcase"]
    }
}
```

- PayloadBasedGet API

```json
{
  "metricId": "Inventory",
  "timeGranularity": "DAILY",
  "queryOptions": {
    "periodStartDate": "2023-03-19",
    "periodEndDate": "2023-04-04",
    "groupBy": ["periodStartDate"],
    "filters": {
        "productLine": ["Amazon Digital Products 21 Accessory"],
        "sortType": ["fullcase"]
    }
  },
  "scope": "US",
  "planGranularity": "PRODUCTLINE-SORTTYPE-WAREHOUSE"
}
```
