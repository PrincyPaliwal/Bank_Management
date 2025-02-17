# Serverless Databricks Job Orchestrator

## Overview
The **Serverless Databricks Job Orchestrator** eliminates the need for Apache Airflow by leveraging AWS-native orchestration tools. This approach simplifies workflow management, reduces infrastructure overhead, and enhances security and scalability by utilizing AWS Step Functions, AWS Lambda, and AWS CloudWatch.

## Features
- **No Airflow Dependency**: Reduces the burden of maintaining an Airflow instance.
- **Cost Efficiency**: Pay-as-you-go pricing model without persistent infrastructure.
- **Native AWS Integration**: Seamless connectivity with AWS Step Functions, Lambda, and CloudWatch.
- **Simplified Security and Access Control**: Uses IAM roles and AWS Secrets Manager.
- **Scalability and Fault Tolerance**: Automatic scaling with built-in error handling.

## Folder Structure
The project is structured into key components to ensure modularity and ease of use:

### 1. **Orchestration Scripts**
This folder contains automation scripts that integrate with AWS services:
- **Lambda Functions**: Serverless functions to trigger Databricks jobs.
- **Step Functions Definitions**: AWS Step Functions state machine definitions for job orchestration.

### 2. **IAM Policies & Security**
Contains IAM role and policy definitions required to securely execute Databricks jobs:
- **IAM Role for Lambda**: Grants permissions to invoke Step Functions, write logs, and call the Databricks API.
- **AWS Secrets Manager Integration**: Securely stores and manages Databricks API credentials.

### 3. **Monitoring & Logging**
Includes configurations for centralized logging and monitoring:
- **CloudWatch Logs**: Stores logs from Lambda and Step Functions.
- **Step Functions Execution History**: Tracks execution logs and error handling.

## Getting Started

### Prerequisites
To use this orchestrator, ensure you have:
- **AWS Account** with permissions to use Step Functions, Lambda, and CloudWatch.
- **Databricks Workspace** and API credentials.
- **AWS CLI & Terraform (Optional)** for deployment automation.

### Installation
Clone the repository to your local machine:
```bash
git clone https://github.com/your-repo/serverless-databricks-orchestrator.git
cd serverless-databricks-orchestrator
```

### Setup
#### 1. **Create an IAM Role for Lambda**
Grant necessary permissions by attaching the following IAM policy:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["logs:CreateLogGroup", "logs:CreateLogStream", "logs:PutLogEvents"],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": "states:StartExecution",
      "Resource": "*"
    }
  ]
}
```

#### 2. **Deploy Lambda Function**
- Configure the **Databricks API** details.
- Deploy the function using AWS Lambda.

#### 3. **Create an AWS Step Functions State Machine**
- Define the state machine JSON configuration.
- Replace placeholders for **region, account ID, and Lambda function name**.
- Deploy the state machine via AWS Console or Terraform.

### Usage
1. **Manually Trigger the Step Function**
   - Navigate to AWS Step Functions.
   - Start execution and monitor logs.
2. **Automate Execution**
   - Set up an AWS EventBridge rule to trigger workflows based on schedule or events.

## Monitoring & Debugging
- **CloudWatch Logs**: Find execution logs under `/aws/lambda/YourLambdaFunctionName`.
- **Step Functions Execution History**: Track execution flow and errors in the AWS Console.

## Contributions
We welcome contributions! If you have ideas for improvements, submit a pull request.

## License
This project is licensed under the **MIT License**.

## Contact
For issues, support, or questions, please use the GitHub Issues section or contact the project maintainer via email.

