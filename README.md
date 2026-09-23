# AWS S3 → Lambda → CloudWatch File Processing

## 📌 Project Overview

This project demonstrates an event-driven serverless architecture using **Amazon S3, AWS Lambda, IAM, and Amazon CloudWatch**.

Whenever a file is uploaded to an S3 bucket, the upload event automatically triggers an AWS Lambda function. The Lambda function receives the S3 event information and writes the details to CloudWatch Logs.

## 🏗️ Architecture

```text
User
  │
  │ Upload file
  ▼
┌─────────────────────┐
│     Amazon S3       │
│   demobucket1guvi   │
└──────────┬──────────┘
           │
           │ ObjectCreated event
           ▼
┌─────────────────────┐
│     AWS Lambda      │
│  s3-file-processor  │
└──────────┬──────────┘
           │
           │ Logs
           ▼
┌─────────────────────┐
│   Amazon CloudWatch │
│       Logs          │
└─────────────────────┘
```

## ☁️ AWS Services Used

| Service           | Purpose                               |
| ----------------- | ------------------------------------- |
| Amazon S3         | Stores uploaded files                 |
| AWS Lambda        | Processes the S3 event                |
| IAM               | Provides Lambda execution permissions |
| Amazon CloudWatch | Stores Lambda execution logs          |

## ⚙️ How It Works

1. A file is uploaded to the S3 bucket.
2. Amazon S3 generates an `ObjectCreated` event.
3. The S3 event triggers the Lambda function.
4. Lambda receives information about the uploaded object.
5. Lambda prints the event details.
6. CloudWatch automatically stores the Lambda logs.

## 🪣 S3 Bucket

Example bucket:

```text
demobucket1guvi
```

AWS Region:

```text
us-east-1
```

## ⚡ Lambda Function

Function name:

```text
s3-file-processor
```

Runtime:

```text
Python 3.14
```

## 🐍 Lambda Code

```python
import json

def lambda_handler(event, context):

    print("S3 file upload detected!")

    print(json.dumps(event))

    return {
        "statusCode": 200,
        "body": json.dumps("File processed successfully!")
    }
```

## 🔐 IAM Permissions

The Lambda execution role uses:

```text
AWSLambdaBasicExecutionRole
```

This allows Lambda to send execution logs to Amazon CloudWatch.

The S3 bucket is configured to invoke the Lambda function when an object is created.

## 🧪 Testing

A test file was uploaded to the S3 bucket:

```text
Interview+-1.txt
```

File size:

```text
1339 bytes
```

S3 generated the following event:

```text
ObjectCreated:Put
```

The Lambda function successfully received the event.

## 📋 Sample CloudWatch Output

```text
START RequestId: ...

S3 file upload detected!

{
  "Records": [
    {
      "eventSource": "aws:s3",
      "eventName": "ObjectCreated:Put",
      "s3": {
        "bucket": {
          "name": "demobucket1guvi"
        },
        "object": {
          "key": "Interview+-1.txt",
          "size": 1339
        }
      }
    }
  ]
}

END RequestId: ...
```

## ✅ Project Status

* [x] Create S3 bucket
* [x] Create Lambda function
* [x] Configure IAM execution role
* [x] Add S3 trigger
* [x] Upload test file
* [x] Trigger Lambda automatically
* [x] Verify CloudWatch logs

## 🚀 Future Improvements

The project can be extended to:

* Read the uploaded file from S3
* Count the number of words in the file
* Create a processed output file
* Store the output back in S3
* Add S3 event filtering
* Add CloudWatch alarms
* Add SNS email notifications
* Manage the infrastructure using Terraform
* Deploy Lambda using Jenkins CI/CD
* Add automated testing
* Add API Gateway integration

## 🎯 DevOps Skills Demonstrated

This project demonstrates practical knowledge of:

* AWS Lambda
* Amazon S3
* IAM
* CloudWatch
* Event-driven architecture
* Serverless computing
* Python
* AWS troubleshooting
* AWS monitoring and logging

