# Using multiple AWS DataSync agents for a location<a name="multiple-agents"></a>

For most workloads, we recommend that you use one AWS DataSync agent for each self\-managed location\.

Some workloads can have tens of millions of small files, though\. In these situations, we recommend up to four agents for each location\.

When using multiple agents for a location, remember the following:
+ All the agents must be online to run your DataSync task\.
**Note**  
If even one of the agents goes offline, you can't use the location in a task\.
+ If you're using a virtual private cloud \(VPC\) endpoint to communicate with AWS, all the agents must use the same endpoint and subnet\.