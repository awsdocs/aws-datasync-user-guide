# Transferring data from a self\-managed storage array<a name="best-practices-storage-array"></a>

You might want to transfer data from a self\-managed enterprise storage array to Amazon EFS\. In this case, files in the source file system might be modified by another application while the files are being transferred from Network File System \(NFS\) or Server Message Block \(SMB\) file share to Amazon EFS\. 

To ensure that DataSync successfully performs a transfer with full consistency verification, we recommend that the source location point to a read\-only snapshot\. This setup ensures that files at the source location can't be modified while the files are being transferred, and makes sure that verification works\.

For information about how to take a snapshot in an enterprise storage array, see one of the following: 
+ EMC VNX: [How to create a VNX snapshot and attach it to a server](https://community.emc.com/docs/DOC-24251)
+ NetApp: [Snapshot management](https://library.netapp.com/ecmdocs/ECMP1635994/html/GUID-DF14D62D-99D1-4B2B-8065-884C9E914259.html)
+ HPE 3PAR: [Creating virtual volume snapshots](https://support.hpe.com/hpesc/public/videoDisplay?videoId=vtc00000327en_us)
+ HDS: [Hitachi Copy\-on\-Write Snapshot User Guide](https://support.hds.com/download/epcra/rd701311.pdf)