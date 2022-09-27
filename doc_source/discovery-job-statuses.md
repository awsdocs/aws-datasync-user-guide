# AWS DataSync Discovery statuses<a name="discovery-job-statuses"></a>


|  | 
| --- |
| AWS DataSync Discovery is in preview release for DataSync and is subject to change\. | 

You can check the status of your discovery jobs and whether AWS DataSync Discovery can provide recommendations for your AWS migrations\.

## Discovery job statuses<a name="discovery-job-statuses-table"></a>

Use the following table to understand what's going on with your discovery job\.


| Console status | API status | Description | 
| --- | --- | --- | 
|  In progress  |  `RUNNING`  |  Your discovery job is running\. The job collects data about your on\-premises storage system for the duration that you specified\.  | 
| In error | `ERROR` |  Your discovery job has encountered errors and currently can't collect data\. Review the Amazon CloudWatch logs and address these issues within 12 hours, or the job will be terminated\.  | 
| Stopped | `STOPPED` | You stopped your discovery job before the job was expected to finish\. | 
|  Completed  |  `COMPLETED`  |  Your discovery job successfully collected all data from your on\-premises storage system\.  | 
| Completed with error | `COMPLETED_WITH_ERROR` | There were times during the discovery job when DataSync Discovery couldn't collect data\. For details, see your CloudWatch logs\. | 
| Terminated | `TERMINATED` | Your discovery job was canceled because of unresolved issues and some data wasn’t collected\. For details, see your CloudWatch logs\. | 
| Failed | `FAILED` | Your discovery job encountered issues and couldn’t collect data from the on\-premises storage system\. For details, see your CloudWatch logs\. | 

## Recommendation statuses<a name="recommendation-statuses-table"></a>

Use the following table to understand whether DataSync Discovery recommendations are ready to view, incomplete, or can't be determined\. 


| Console status | API status | Description | 
| --- | --- | --- | 
|  Get recommendations  | `NONE` |  Your discovery job collected enough data for DataSync Discovery to generate recommendations\.  | 
| Unavailable | `NONE` | If your discovery job fails, DataSync Discovery can't generate recommendations\. | 
|  Generating  |  `IN_PROGRESS`  |  DataSync Discovery is generating recommendations\.  | 
| Available | `COMPLETED` | Your recommendations are ready to view\. | 
| Available with issues | `COMPLETED_WITH_ERROR` | DataSync Discovery couldn't generate recommendations for some of your storage system's resources\. You can review your CloudWatch logs to learn more, and then try generating the recommendations again\. | 
| Failed | `FAILED` | DataSync Discovery couldn't generate any recommendations\. You can review your CloudWatch logs to identify the issue, and then try generating the recommendations again\. | 