# Data protection in AWS DataSync<a name="data-protection"></a>

AWS DataSync securely transfers data between self\-managed storage systems and AWS storage services and also between AWS storage services\. How your storage data is encrypted in transit depends in part on the locations involved in the transfer\. 

After the transfer completes, data is encrypted at rest by the system or service that's storing the data \(not DataSync\)\.

**Topics**
+ [AWS DataSync encryption in transit](encryption-in-transit.md)
+ [AWS DataSync encryption at rest](encrypting-data.md)
+ [Internetwork traffic privacy](internetwork-traffic-privacy.md)