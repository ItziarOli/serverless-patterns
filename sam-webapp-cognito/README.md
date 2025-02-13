# AWS SAM Pattern for Serverless Web Application

This pattern creates a Serverless WebApp using Amazon S3, Amazon CloudFront, Amazon API Gateway HTTP API, AWS Lambda, Amazon DynamoDB table and Amazon Cognito

Learn more about this pattern at Serverless Land Patterns: https://serverlessland.com/patterns/sam-webapp-cognito

Important: this application uses various AWS services and there are costs associated with these services after the Free Tier usage - please see the [AWS Pricing page](https://aws.amazon.com/pricing/) for details. You are responsible for any AWS costs incurred. No warranty is implied in this example.

## Requirements

- [Create an AWS account](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html) if you do not already have one and log in. The IAM user that you use must have sufficient permissions to make necessary AWS service calls and manage AWS resources.
- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html) installed and configured
- [Git Installed](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [AWS Serverless Application Model](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html) (AWS SAM) installed

## Deployment Instructions

1. Create a new directory, navigate to that directory in a terminal and clone the GitHub repository:
   ```
   git clone https://github.com/aws-samples/serverless-patterns
   ```
2. Change directory to the pattern directory:
   ```
   cd sam-webapp-cognito
   ```
3. From the command line, use AWS SAM to deploy the AWS resources for the pattern as specified in the template.yml file:
   ```
   sam deploy --guided
   ```
4. During the prompts:

   - Enter a stack name
   - Enter the desired AWS Region
   - Allow SAM CLI to create IAM roles with the required permissions.

   Once you have run `sam deploy --guided` mode once and saved arguments to a configuration file (samconfig.toml), you can use `sam deploy` in future to use these defaults.

5. Note the outputs from the SAM deployment process. These contain the resource names and/or ARNs which are used for testing.

## How it works

This pattern deploys a serverless web application using S3, CloudFront, API Gateway, DynamoDB and Cognito. CloudFront CDN serves static and dynamic content with two separate origins for S3 and API Gateway. It deploys a Cognito user pool and user pool client for authentication. The HTTP API is deployed with default route and basic CORS configuration. The defaul route is intergrated with Lambda written Node.js. HTTP API is protected using JWT authorizer using Cognito as the issuer.

This pattern uses the frontend and lambda code as shown in https://webapp.serverlessworkshops.io/. Once the deployment is complete;

1. Copy the contents of frontend folder to S3 bucket. You can use the command `aws s3 sync ./src/frontend s3://<bucketname-from-stack-output>`
2. Copy Cognito user pool id, user pool client id and CloudFront domain name from the stack output. Open config.js under /frontend/js/config.js and paste the values stack output to the respective fields.

## Testing

Once the application is deployed, you can test it by entering the cloudfront url in a browser. Goto /register.html to create a Cognito user and /signin.html to login. Refer to https://webapp.serverlessworkshops.io for further information on how the application works.

## Cleanup

1. Delete the stack
   ```bash
   aws cloudformation delete-stack --stack-name STACK_NAME
   ```
1. Confirm the stack has been deleted
   ```bash
   aws cloudformation list-stacks --query "StackSummaries[?contains(StackName,'STACK_NAME')].StackStatus"
   ```

---

Copyright 2023 Amazon.com, Inc. or its affiliates. All Rights Reserved.

SPDX-License-Identifier: MIT-0
