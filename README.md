Cloud Security Automation: Automated Security Compliance with AWS Config

Project Overview

This project automates the security compliance of AWS resources using AWS Config, ensuring that resources follow security best practices. By leveraging AWS Config, AWS Lambda, and AWS CloudWatch, we automatically check resources like S3 buckets for security misconfigurations and notify the team of violations in real time.

Key Features:

Automates security compliance monitoring for AWS resources.

Uses AWS Config to track configuration changes and ensure compliance.

Custom Lambda functions check specific security policies (e.g., S3 bucket public access).

Integrates AWS CloudWatch and SNS for automated alerts and notifications.

Infrastructure as code (IaC) using CloudFormation for deployment.



---

Technologies Used:

AWS Config - Monitors resource configurations and compliance.

AWS Lambda - Executes custom compliance checks on AWS resources.

AWS CloudWatch - Monitors AWS Config compliance metrics.

Amazon SNS - Sends notifications for non-compliant resources.

AWS CloudFormation - Automates resource provisioning and configuration.

Python - Lambda function programming language.



---

Project Structure

.
├── cloudformation
│   ├── aws-config-template.yaml  # CloudFormation template to deploy AWS Config resources
│   ├── s3-bucket-check-lambda.py # Lambda function for checking S3 bucket public access
│   ├── config-rule-template.yaml  # CloudFormation template to create AWS Config rule
│   ├── sns-cloudwatch-template.yaml  # CloudFormation template to set up SNS and CloudWatch alarm
└── README.md                     # This file


---

Requirements:

1. AWS Account - You need an AWS account to deploy the resources.


2. IAM Role - Ensure the proper IAM roles with permissions for AWS Config, Lambda, CloudWatch, and SNS.


3. AWS CLI - For deploying CloudFormation templates and interacting with AWS services.




---

How to Deploy:

Step 1: Deploy CloudFormation Templates

1. Deploy AWS Config and Lambda: Use the aws-config-template.yaml and config-rule-template.yaml to deploy AWS Config, Lambda, and create the security compliance rule.

aws cloudformation create-stack --stack-name security-compliance-stack --template-body file://cloudformation/aws-config-template.yaml --capabilities CAPABILITY_IAM


2. Deploy SNS and CloudWatch Alarm: Use the sns-cloudwatch-template.yaml to set up an SNS topic and CloudWatch alarms to notify you when resources are non-compliant.

aws cloudformation create-stack --stack-name security-notification-stack --template-body file://cloudformation/sns-cloudwatch-template.yaml --capabilities CAPABILITY_IAM



Step 2: Lambda Function Setup

The Lambda function, defined in s3-bucket-check-lambda.py, will be automatically created during the CloudFormation deployment. Ensure that it is linked to AWS Config and is set to check for public access on S3 buckets.


Step 3: Monitor Compliance

Once deployed, AWS Config will continuously monitor your AWS resources. The Lambda function will check S3 bucket public access configurations and return compliance results.

Violations will trigger CloudWatch alarms, which will notify you through SNS.



---

How It Works:

1. AWS Config monitors resource configurations across your account.


2. When an S3 bucket’s configuration changes, it triggers the AWS Config rule to check the resource.


3. Lambda evaluates the security of the S3 bucket (e.g., checks if it is publicly accessible).


4. If a violation is detected, AWS Config updates its compliance status.


5. CloudWatch monitors AWS Config’s compliance status and triggers an alert.


6. SNS sends notifications (e.g., via email) about non-compliant resources.




---

Project Customization:

Custom Rules: You can extend the Lambda function to check for additional security policies (e.g., EC2 instance configurations, IAM roles, etc.).

Notifications: You can modify the SNS configuration to send notifications to different channels (e.g., Slack, Email, etc.).

Other AWS Resources: Expand this project to monitor other AWS resources by creating additional Lambda functions and Config rules.



---

Example Output:

When an S3 bucket is found to be public, the Lambda function returns the following output:

{
  "complianceType": "NON_COMPLIANT",
  "annotation": "Bucket my-bucket is public"
}

If the S3 bucket is secure:

{
  "complianceType": "COMPLIANT",
  "annotation": "Bucket my-bucket is secure."
}


---

Conclusion:

This project demonstrates how to automate cloud security compliance with AWS Config and other AWS services. It automates the monitoring of AWS resources for security best practices, ensuring real-time alerts for any policy violations. It serves as an excellent solution for cloud security automation, simplifying compliance management in a scalable manner.


---

License:

This project is licensed under the MIT License - see the LICENSE file for details.


---

Acknowledgments:

AWS Documentation for guidance on AWS Config, Lambda, CloudWatch, and SNS.

CloudFormation for automating infrastructure provisioning.



---

This README outlines the project setup and usage, providing clear instructions for anyone to deploy and customize the cloud security automation system.

