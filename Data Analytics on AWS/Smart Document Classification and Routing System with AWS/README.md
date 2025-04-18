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

### Step 1: Create S3 Buckets
These will be used to upload documents and route them after classification.
Action:
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
Action:
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
Click Next → Name the role: `LambdaDocumentProcessorRole `
Click Create Role

![Role Policies](https://github.com/user-attachments/assets/76b81944-e930-4dc2-b6df-b850b4d5686b)


### Step 3: Create SNS Topic (for Email Alerts)
Action:
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

![Sub-Conf](https://github.com/user-attachments/assets/79cb4e5b-07df-48ee-b5db-e155b7ddfdf5)

### Step 4: Create the Lambda Function
Action:
- Go to AWS Lambda → Create Function
- Choose:
- Name: DocumentClassifier
- Runtime: Python 3.10
- Execution Role: Use existing role → Select ```LambdaDocumentProcessorRole```
- Click Create Function

Step 5: Add Classification Code to Lambda
Scroll to Function Code section

Replace everything in the code editor with this:

```python
import json, boto3
import urllib.parse

s3 = boto3.client('s3')
textract = boto3.client('textract')
sns = boto3.client('sns')

def lambda_handler(event, context):
    bucket = event['Records'][0]['s3']['bucket']['name']
    key = urllib.parse.unquote_plus(event['Records'][0]['s3']['object']['key'])

    # Extract text from document using Textract
    response = textract.detect_document_text(
        Document={'S3Object': {'Bucket': bucket, 'Name': key}}
    )
    
    lines = [item['Text'] for item in response['Blocks'] if item['BlockType'] == 'LINE']
    extracted_text = " ".join(lines).lower()

    # Simple classification logic
    if "invoice" in extracted_text:
        doc_type = "Invoice"
        target_bucket = "classified-invoices-bucket"
    elif "resume" in extracted_text or "curriculum" in extracted_text:
        doc_type = "Resume"
        target_bucket = "classified-resumes-bucket"
    elif "contract" in extracted_text or "agreement" in extracted_text:
        doc_type = "Contract"
        target_bucket = "classified-contracts-bucket"
    else:
        doc_type = "Unknown"
        target_bucket = "classified-contracts-bucket"  # fallback

    # Move file to the classified bucket
    s3.copy_object(
        CopySource={'Bucket': bucket, 'Key': key},
        Bucket=target_bucket,
        Key=key
    )
    s3.delete_object(Bucket=bucket, Key=key)

    # Send notification
    sns.publish(
        TopicArn='arn:aws:sns:us-east-1:YOUR_ACCOUNT_ID:DocumentNotifications',
        Message=f"Document '{key}' classified as {doc_type} and moved to {target_bucket}.",
        Subject="New Document Routed"
    )

    return {'statusCode': 200, 'body': json.dumps('Success')}

```
✅ Replace YOUR_ACCOUNT_ID with your actual AWS account ID (find it in top-right corner of AWS console).

Click Deploy to save.

🔁 Step 6: Add Trigger for S3 Upload
This tells AWS to run the Lambda function when a file is uploaded.

🔧 Action:
Go to S3 → incoming-docs-bucket

Click Properties → Scroll down to Event notifications

Click Create event notification

Name: TriggerLambda

Event type: PUT

Prefix/Suffix: Leave empty

Destination: Lambda function

Select DocumentClassifier

Save.

🧪 PART 3: Test the System
📄 Upload a Sample File:
Go to S3 → incoming-docs-bucket → Click Upload

Use one of these sample texts in a .txt, .pdf, or .docx:

“This is an invoice for $5000.” → Should go to classified-invoices-bucket

“My name is John Doe. Attached is my resume.” → Should go to classified-resumes-bucket

“This contract is signed on March 15.” → Should go to classified-contracts-bucket

📩 Check the Output:
Go to the correct target bucket – your file should now be there

Check your email inbox – you'll get a message like:

"Document 'invoice.pdf' classified as Invoice and moved to classified-invoices-bucket."

🧾 View Logs:
Go to CloudWatch → Logs → Lambda → Select your function

View logs for detailed success/failure messages

🎯 What You Achieved
✅ Built an automated document classification system
✅ Used AWS S3, Lambda, Textract, SNS together
✅ Learned how to classify text using Python
✅ Learned how to route and manage files using AWS
✅ Got real-time email alerts when files were processed
