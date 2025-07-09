---
title : "Enhanced Lambda Function with DynamoDB"
date: 2025-06-18
weight : 3
chapter : false
pre : " <b> 4.3. </b> "
---
### Update the Lambda Function Created in OPTION 1:
1. Go to the Lambda Console → Select the S3FileNotifier function you created.
2. Go to the Code tab → Delete the old code and replace it with the new code:
```python
import json
import os
import boto3
import uuid
from decimal import Decimal
from datetime import datetime

# Initialize clients
sns_client = boto3.client('sns')
dynamodb = boto3.resource('dynamodb')
sqs_client = boto3.client('sqs')

# Environment variables
SNS_TOPIC_ARN = os.environ.get('SNS_TOPIC_ARN')
DYNAMODB_TABLE = os.environ.get('DYNAMODB_TABLE')
SQS_QUEUE_URL = os.environ.get('SQS_QUEUE_URL')

table = dynamodb.Table(DYNAMODB_TABLE)

def lambda_handler(event, context):
    print("Processing S3 event:", json.dumps(event))
    
    for record in event['Records']:
        bucket_name = record['s3']['bucket']['name']
        file_key = record['s3']['object']['key']
        file_size = record['s3']['object']['size']
        event_name = record['eventName']
        event_time = record['eventTime']
        
        # Generate unique file ID
        file_id = str(uuid.uuid4())
        timestamp = int(datetime.now().timestamp())
        
        # Save to DynamoDB
        try:
            table.put_item(
                Item={
                    'fileId': file_id,
                    'timestamp': timestamp,
                    'bucketName': bucket_name,
                    'fileName': file_key,
                    'fileSize': file_size,
                    'eventType': event_name,
                    'uploadTime': event_time,
                    'status': 'uploaded'
                }
            )
            print(f"Saved to DynamoDB: {file_id}")
        except Exception as e:
            print(f"DynamoDB Error: {e}")
        
        # Send to SQS for further processing
        try:
            sqs_message = {
                'fileId': file_id,
                'bucketName': bucket_name,
                'fileName': file_key,
                'action': 'process_file'
            }
            
            sqs_client.send_message(
                QueueUrl=SQS_QUEUE_URL,
                MessageBody=json.dumps(sqs_message)
            )
            print(f"Sent to SQS: {file_id}")
        except Exception as e:
            print(f"SQS Error: {e}")
        
        # Enhanced notification
        message = f"""🎉 File Processing Started!
        
📁 Bucket: {bucket_name}
📄 File: {file_key}
📊 Size: {file_size} bytes
🆔 File ID: {file_id}
📋 Status: Processing initiated
⏰ Time: {event_time}

Your file has been queued for processing and metadata saved to database."""
        
        # Send SNS notification
        try:
            sns_client.publish(
                TopicArn=SNS_TOPIC_ARN,
                Message=message,
                Subject=f"🔄 Processing Started: {file_key}"
            )
        except Exception as e:
            print(f"SNS Error: {e}")
    
    return {
        'statusCode': 200,
        'body': json.dumps('File processing initiated successfully')
    }
```
3. Click the orange Deploy button (at the top of the "Code source" section) to save and deploy the code to Lambda.
4. Update Environment Variables:
- Go to the Configuration tab → Environment variables → Edit
![Picture59](/images/4.3/image59.png)
- Add 2 new variables:
    - Key: DYNAMODB_TABLE / Value: FileMetadata
    - Key: SQS_QUEUE_URL / Value: Copy the URL from the SQS queue you created
    ![Picture60](/images/4.3/image60.png)
- Save
![Picture61](/images/4.3/image61.png)
5. Update IAM Permissions:
- Go to the Configuration tab → Permissions → Click on the Role name.
![Picture62](/images/4.3/image62.png)
- Add permissions → Attach policies:
![Picture63](/images/4.3/image63.png)
    - AmazonDynamoDBFullAccess
    ![Picture64](/images/4.3/image64.png)
    - AmazonSQSFullAccess
    ![Picture65](/images/4.3/image65.png)
- Add permissions
![Picture66](/images/4.3/image66.png)