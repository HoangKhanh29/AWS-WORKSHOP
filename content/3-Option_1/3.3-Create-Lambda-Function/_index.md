---
title : "Create Lambda Function"
date: 2025-06-18
weight : 3
chapter : false
pre : " <b> 3.3. </b> "
---

1. **Search for Lambda and select AWS Lambda.**
- In the search bar, type **Lambda**.
- Select **Lambda** from the results list.
- Confirm Region: Ensure you are still in **ap-southeast-1**.
![Picture21](/images/3.3/image21.png)

2. **Click Create function:**
![Picture22](/images/3.3/image22.png)
- **Author from scratch**: Select this option.
- **Function name**: Name your function (e.g., `s3FileUploaderNotifier`).
- **Runtime**: Choose **Python 3.9** (or the latest available Python version).
- **Architecture**: Leave default **x86_64**
![Picture23](/images/3.3/image23.png)
- **Execution role**: Select **Create a new role with basic Lambda permissions**. (AWS will automatically create a basic IAM Role for Lambda with CloudWatch logging permissions).

3. **Click Create function.**
![Picture24](/images/3.3/image24.png)
![Picture25](/images/3.3/image25.png)

4. **Grant SNS permissions to Lambda's IAM Role (VERY IMPORTANT!):**
- After the Function is created, you'll be taken to the Function details page.
- Go to the **Configuration** tab (at the top, near the Function name).
- In the left menu, select **Permissions**.
- Under the "Execution role" section, you'll see the Role name (e.g., s3FileUploaderNotifier-role-xxxxxxxx). **Click on this ROLE NAME**.
![Picture26](/images/3.3/image26.png)
- A new tab will open, taking you to the IAM (Identity and Access Management) page. This is where permissions are managed.
- In the IAM Role page, click **Add permissions** → **Attach policies**.
![Picture27](/images/3.3/image27.png)
- In the search box, type **SNS** and select the **AmazonSNSFullAccess** policy (Or **AmazonSNSPublishAccess** if available and you want more restricted permissions).

{{% notice info %}}
This policy grants Lambda permission to send messages to SNS Topics. Without this permission, Lambda will return an error.
{{% /notice %}}

- Click **Add permissions** (bottom right corner).
![Picture28](/images/3.3/image28.png)
![Picture29](/images/3.3/image29.png)

5. **Add Lambda Function Code:**
- Return to the Lambda Function browser tab.
- Scroll down to the **Code source** section.
- You'll see sample Python code. **Delete all the sample code**.
![Picture30](/images/3.3/image30.png)
- **Paste the following Python code:**

```python
import json
import os
import boto3

# Khởi tạo SNS client
sns_client = boto3.client('sns')
SNS_TOPIC_ARN = os.environ.get('SNS_TOPIC_ARN')

def lambda_handler(event, context):
    print("Received S3 event:", json.dumps(event))
    
    for record in event['Records']:
        bucket_name = record['s3']['bucket']['name']
        file_key = record['s3']['object']['key']
        event_name = record['eventName']
        event_time = record['eventTime']
        
        # Tạo nội dung thông báo
        message = f"""🔔 Thông báo: File mới được upload!
        
📁 Bucket: {bucket_name}
📄 File: {file_key}
🎯 Event: {event_name}
⏰ Time: {event_time}

🔗 Link: https://s3.console.aws.amazon.com/s3/v2/buckets/{bucket_name}/objects/?prefix={file_key}&region={os.environ.get('AWS_REGION')}"""
        
        subject = f"🚀 File Upload Alert: {file_key}"
        
        try:
            response = sns_client.publish(
                TopicArn=SNS_TOPIC_ARN,
                Message=message,
                Subject=subject
            )
            print("SNS Response:", response)
        except Exception as e:
            print(f"Error: {e}")
    
    return {
        'statusCode': 200,
        'body': json.dumps('Successfully processed S3 event')
    }
```

- Click the orange **Deploy** button (above the "Code source" section) to save and deploy the code to Lambda.
![Picture31](/images/3.3/image31.png)

6. **Configure Environment Variables:**
- Still in the **Configuration** tab of the Lambda function.
- In the left menu, select **Environment variables**.
- Click **Edit**.
![Picture32](/images/3.3/image32.png)
- Click **Add environment variable**.
- **Key**: Enter `SNS_TOPIC_ARN`
- **Value**: Paste the ARN of the SNS Topic you copied in step 3.2. (Example: arn:aws:sns:ap-southeast-1:123456789012:FileUploadedNotifications).
- Click **Save**.
![Picture33](/images/3.3/image33.png)
![Picture34](/images/3.3/image34.png)

7. **Configure Lambda Trigger (Connect S3 with Lambda)**
- In your Lambda Function page (s3FileUploaderNotifier):
    - In the "Function overview" section (graphical diagram at the top), click **Add trigger**.
    ![Picture35](/images/3.3/image35.png)
- **Configure Trigger:**
    - **Select a source**: Choose **S3** from the service list.
    - **Bucket**: Select the S3 Bucket you created in Step 2 (e.g., yourname-hutech-serverless-files-2025).
    - **Event types**: Choose **All object create events** (this means any event that creates or overwrites a file in the bucket will trigger Lambda).
    ![Picture36](/images/3.3/image36.png)
    - **Recursive invocation**: Check the box **I acknowledge that enabling this trigger may result in recursive invocations...** (This is an AWS warning, in this case it's safe because our code doesn't cause infinite loops).
    - **Enable trigger**: Check this box (usually pre-selected).
- **Add Trigger:**
    - Click the orange **Add** button.
    ![Picture37](/images/3.3/image37.png)
- **Verify**: After adding, you'll see your S3 Bucket appear in the "Triggers" section of the Lambda function.
![Picture38](/images/3.3/image38.png)