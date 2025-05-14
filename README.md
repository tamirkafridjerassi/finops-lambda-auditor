# FinOps Lambda Auditor (SAM-Ready)

This project provides a production-ready AWS Lambda function designed to automate FinOps visibility. It detects idle EC2 instances, unattached EBS volumes, and idle RDS databases, and stores the findings in a structured report in S3.

## Features

- Identifies underutilized EC2 instances (based on CloudWatch CPU metrics)
- Detects unattached EBS volumes
- Flags idle RDS instances
- Automatically creates and writes to `finops-report-<account_id>` S3 bucket
- Built for serverless deployment using AWS SAM (Serverless Application Model)

## Prerequisites

- AWS CLI and `sam` CLI installed
- IAM permissions for:
  - EC2, CloudWatch, RDS (read-only)
  - S3 (create and write)

## Deployment Steps

1. Clone the repo
2. Build and deploy using SAM:

```bash
sam build
sam deploy --guided
```

This will guide you through region selection, stack naming, and create the function in your AWS account.

## Folder Structure

```
finops-lambda-auditor/
├── src/
│   ├── lambda_function.py
│   ├── ec2_idle_checker.py
│   ├── ebs_checker.py
│   ├── rds_checker.py
│   ├── s3_handler.py
│   └── requirements.txt
├── template.yaml
└── README.md
```

## Output

Uploads 3 CSVs into your S3 bucket:

- `idle_instances.csv`
- `unattached_volumes.csv`
- `idle_rds.csv`
