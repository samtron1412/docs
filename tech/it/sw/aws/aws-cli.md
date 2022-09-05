# Overview

- https://docs.aws.amazon.com/cli/
- https://aws.amazon.com/cli/
- https://github.com/aws/aws-cli

- Set up auto completion for AWS CLI:
    + https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-completion.html

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
