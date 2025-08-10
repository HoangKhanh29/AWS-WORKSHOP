---
title : "Update Lambda"
date: 2025-06-18
weight : 2
chapter : false
pre : " <b> 4.2 </b> "
---

In this step, we will update lambda.

## Update Lambda

1. Go to **Lambada Producer**
    - Correct the following code.

```javascript
  const AWS = require('aws-sdk');
AWS.config.update({
  region: "us-east-1"
});

const s3 = new AWS.S3();
const kinesis = new AWS.Kinesis();

export const handler = async (event) => {
  console.log(JSON.stringify(event));
  const bucketName = event.Records[0].s3.bucket.name;
  const keyName = event.Records[0].s3.object.key; 

  const params = {
    Bucket: bucketName,
    Key: keyName
  };


  await s3.getObject(params).promise().then(async (data) => { 
    const dataString = data.Body.toString();
    const payload = {
      data: dataString
    };

    await sendToKinesis(payload, keyName);
  }, error => {
    console.error(error);
  });
};


async function sendToKinesis(payload, partitionKey) {
  const params = {
    Data: JSON.stringify(payload),
    PartitionKey: partitionKey,
    StreamName: 'demo-datasrc-stream'
  };

  
  await kinesis.putRecord(params).promise().then(response => {
    console.log(response);
  }, error => {
    console.error(error);
  });
}
```
![ConnectPrivate](/images/4.kinesis/D-4.png)  
2. Go to **Lambda Consumer#1** and **Lambda Consumer#2**\
    - Correct the code of **Consumer#1** and **Consumer#2**\
    - Replace **cusumer#1** with **cusumer#2**
```javascript
  export const handler = async (event) => {
  console.log(JSON.stringify(event));
  for (const record of event.Records) {
    const data = JSON.parse(Buffer.from(record.kinesis.data,'base64'));
    console.log('cusumer #1',data);

  }
};
```
```javascript
   export const handler = async (event) => {
   console.log(JSON.stringify(event));
   for (const record of event.Records) {
     const data = JSON.parse(Buffer.from(record.kinesis.data,'base64'));
     console.log('cusumer #2',data);

   }
 };
```
![ConnectPrivate](/images/4.kinesis/D-5.png)

3. Add **Trigger**
    - Go to **Lambda Customer#1** and **Lambda Customer#2**
    - Click Add trigger
    - Click VPC Lattice
    ![ConnectPrivate](/images/4.kinesis/D-6.png)
    ![ConnectPrivate](/images/4.kinesis/D-7.png)
    ![ConnectPrivate](/images/4.kinesis/D-8.png)