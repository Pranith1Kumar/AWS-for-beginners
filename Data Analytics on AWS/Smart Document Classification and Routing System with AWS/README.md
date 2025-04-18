#  *Intelligent Document Classification and Routing System Using AWS*

## Prerequisites
- AWS Account (Free Tier is sufficient) → Sign up here
- Basic familiarity with AWS Console UI
- Use us-east-2 as your region (or you can use based on your preferences)


## Project Overview
This project is an automated serverless pipeline built using AWS services that intelligently processes and classifies incoming documents. When a document (e.g., PDF, Word) is uploaded to an S3 bucket, it automatically:

- Accepts documents (PDF/DOCX) via S3
- Uses Amazon Textract to extract text
- Classifies documents (Invoice, Resume, Contract) using keyword matching
- Moves documents to appropriate S3 buckets
- Sends email notifications using Amazon SNS
Perfect for automating HR document processing, financial records, or contracts.

## Architecture
![Project-flow](https://github.com/user-attachments/assets/1b4e2f4e-87c8-4d56-a37a-54e208beb116)


## Setup the Environment

### Step 1: Create S3 Buckets
These will be used to upload documents and route them after classification.

### Action:
- Go to AWS Console → S3 → Click Create bucket
Create these 4 buckets: (Bucket name should be in lowercase)
- incoming-docs-bucket
- classified-bucket-invoices
- classified-bucket-resumes
- classified-bucket-contracts

![classifed-bucket](https://github.com/user-attachments/assets/8736c0c7-8275-4c42-bad5-293acc055cca)
![Incoming-bucket](https://github.com/user-attachments/assets/cc9c1e02-e0f3-429b-8777-ed43e01d63c5)

- Continue with other two buckets don't uncheck the Block all public access beacause we are using it private

Bucket Settings:
Leave all settings default
DO NOT enable public access
Enable versioning for backup tracking
Repeat this 4 times for each bucket.

![4-Buckets](https://github.com/user-attachments/assets/42cc0c78-1ea1-444e-b8ad-29ac4c7f12d3)

### Step 2: Create an IAM Role for Lambda
This role allows your Lambda function to access S3, Textract, SNS, and logs.

### Action:
- Go to AWS Console → IAM → Roles → Click Create role
- Choose Trusted Entity: AWS Service
- Choose Use Case: Lambda → Click Next

![IAM Role](https://github.com/user-attachments/assets/298e88d4-38c1-4ed5-9915-eeeb10106c5d)

Attach the following policies:
Search and select each of these:

- AmazonS3FullAccess
- AmazonTextractFullAccess
- ComprehendFullAccess
- AmazonSNSFullAccess
- CloudWatchLogsFullAccess
Click Next → Name the role:

`LambdaDocumentProcessorRole `

Click Create Role

![Role Policies](https://github.com/user-attachments/assets/76b81944-e930-4dc2-b6df-b850b4d5686b)


### Step 3: Create SNS Topic (for Email Alerts)
### Action:
1. Go to Amazon SNS → Topics → Click Create topic
2. Choose:
  - Type: Standard
  - Name: DocumentNotifications
3. Click Create Topic

![SNS-Topic](https://github.com/user-attachments/assets/3a83e670-f71c-4722-8860-1282821ad2c3)

Create Subscription:
1. Go to the topic → Click Create subscription
2. Choose:
  - Protocol: Email
  - Endpoint: Your email (e.g., you@example.com)
3. Go to your inbox and click Confirm subscription
