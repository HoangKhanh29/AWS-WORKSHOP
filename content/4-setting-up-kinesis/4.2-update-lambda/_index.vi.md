---
title : "Cập nhật Lambda"
date: 2025-06-18
weight : 2
chapter : false
pre : " <b> 4.2 </b> "
---

Trong bước này, chúng ta sẽ cập nhật Lambda.

## Cập nhật Lambda

1. Vào **Lambda Producer**
    - Chỉnh sửa đoạn mã sau:

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
2. Vào **Lambda Consumer#1** và **Lambda Consumer#2**\
    - Chỉnh sửa mã của **Consumer#1** và **Consumer#2**\
    - Thay **cusumer#1** bằng **cusumer#2**

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

3. Thêm **Trigger**
    - Vào **Lambda Customer#1** và **Lambda Customer#2**
    - Nhấn Add trigger
    - Chọn VPC Lattice
    ![ConnectPrivate](/images/4.kinesis/D-6.png)
    ![ConnectPrivate](/images/4.kinesis/D-7.png)
    ![ConnectPrivate](/images/4.kinesis/D-8.png)