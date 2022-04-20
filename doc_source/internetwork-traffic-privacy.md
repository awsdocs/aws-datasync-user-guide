# Internetwork traffic privacy<a name="internetwork-traffic-privacy"></a>

We recommend configuring your source and destination locations with the highest level of security that each one supports\. When connecting to a location, AWS DataSync works with the most secure version of the data access protocol that the storage system uses\. Additionally, consider limiting subnet traffic to known protocols and services\.

DataSync secures the connection between locations—including between AWS accounts, AWS Regions, and Availability Zones—by using Transport Layer Security \(TLS\) 1\.2\.