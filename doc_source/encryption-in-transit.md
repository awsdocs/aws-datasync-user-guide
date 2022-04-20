# AWS DataSync encryption in transit<a name="encryption-in-transit"></a>

Your storage data \(including metadata\) is encrypted in transit, but how it's encrypted throughout the transfer depends on your source and destination locations\.

When connecting with a location, DataSync uses the most secure options provided by that location's data access protocol\. For example, when connecting with a Server Message Block \(SMB\) file system, DataSync uses the security features provided by SMB\.

## Network connections in a transfer<a name="understanding-network-connections-in-transit"></a>

DataSync requires three network connections to copy data: a connection to read data from a source location, another to transfer data between locations, and one more to write data to a destination location\. 

The following diagram is an example of the network connections that DataSync uses to transfer data from an on\-premises storage system to an AWS storage service\. To understand where the connections happen and how data is protected as it moves through each connection, use the accompanying table\.

![\[The first connection is for communicating with the source storage location. The second connection is for transferring between locations. The third and final connection is with the destination storage location.\]](http://docs.aws.amazon.com/datasync/latest/userguide/images/datasync-encryption-in-transit-diagram.png)


| Reference | Network connection | Description | 
| --- | --- | --- | 
| 1 | Reading data from the source location | DataSync connects by using the storage system's protocol for accessing data \(for example, SMB or the Amazon S3 API\)\. For this connection, data is protected by using the security features of the storage system's protocol\. | 
| 2 | Transferring data between locations | For this connection, DataSync encrypts all network traffic with Transport Layer Security \(TLS\) 1\.2\. | 
| 3 | Writing data to the destination location | Like it did with the source location, DataSync connects by using the storage system's protocol for accessing data\. Data is again protected by using the security features of the storage system's protocol\. | 

## TLS ciphers<a name="tls-ciphers-in-transit"></a>

When transferring data between locations, DataSync uses different TLS ciphers\. The TLS cipher that DataSync uses depends on the type of endpoint that's used to activate your DataSync agent\.

### Public or VPC endpoints<a name="tls-ciphers-in-transit-non-fips"></a>

For these endpoints, DataSync uses one of the following TLS ciphers:
+ TLS\_ECDHE\_RSA\_WITH\_AES\_256\_GCM\_SHA384 \(ecdh\_x25519\)
+ TLS\_ECDHE\_RSA\_WITH\_CHACHA20\_POLY1305\_SHA256 \(ecdh\_x25519\)
+ TLS\_ECDHE\_RSA\_WITH\_AES\_128\_GCM\_SHA256 \(ecdh\_x25519\)

### FIPS endpoints<a name="tls-ciphers-in-transit-fips"></a>

For FIPS endpoints, DataSync uses the following TLS cipher: 
+ TLS\_ECDHE\_RSA\_WITH\_AES\_128\_GCM\_SHA256 \(ecdh\_x25519\)