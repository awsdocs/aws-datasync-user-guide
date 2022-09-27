# AWS DataSync encryption at rest<a name="encrypting-data"></a>

Because AWS DataSync is a transfer service, it doesn't manage your storage data at rest\. The storage services and systems that DataSync supports are responsible for protecting data in that state\. However, there is some service\-related data that DataSync manages at rest\.

## What's encrypted?<a name="what-is-encrypted"></a>

The only data that DataSync handles at rest relates to the information that it needs to complete your transfer \(also known as a *task*\)\. DataSync stores the following data with full at\-rest encryption in Amazon DynamoDB:
+ Task configurations \(for example, details about the locations in your transfer\)\.
+ User credentials that allow your DataSync agent to authenticate with a location\. These credentials are encrypted by using your agent's public keys\. The agent can decrypt these keys as needed with its private keys\.

For more information, see [DynamoDB encryption at rest](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/EncryptionAtRest.html) in the *Amazon DynamoDB Developer Guide*\.

### Key management<a name="key-management"></a>

You can't manage the encryption keys that DataSync uses to store information in DynamoDB related to running your task\. This information includes your task configurations and the credentials that agents use to authenticate with a storage location\.

## What's not encrypted?<a name="what-is-not-encrpyted"></a>

Though DataSync doesn’t control how your storage data is encrypted at rest, we still recommend configuring your locations with the highest level of security that they support\. For example, you can encrypt objects with Amazon S3 managed encryption keys \(SSE\-S3\) or AWS Key Management Service \(AWS KMS\) keys \(SSE\-KMS\)\.

Learn more about how AWS storage services encrypt data at rest:
+ [Amazon EFS](https://docs.aws.amazon.com/efs/latest/ug/encryption-at-rest.html)
+ [Amazon FSx for Windows File Server](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/encryption-at-rest.html)
+ [Amazon FSx for Lustre](https://docs.aws.amazon.com/fsx/latest/LustreGuide/encryption-at-rest.html)
+ [Amazon FSx for OpenZFS](https://docs.aws.amazon.com/fsx/latest/OpenZFSGuide/encryption-rest.html)
+ [Amazon FSx for NetApp ONTAP](https://docs.aws.amazon.com/fsx/latest/ONTAPGuide/encryption-at-rest.html)
+ [Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/serv-side-encryption.html)