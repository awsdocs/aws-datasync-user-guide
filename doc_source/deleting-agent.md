# Deleting a DataSync agent<a name="deleting-agent"></a>

When you delete a DataSync agent, it's no longer associated with your AWS account and can't be undone\. 

**Note**  
Deleting doesn't remove the agent's virtual machine \(VM\) from your environment\. You can reuse the VM to create and activate a new agent\.

**To delete an agent**

1. Open the AWS DataSync console at [https://console\.aws\.amazon\.com/datasync/](https://console.aws.amazon.com/datasync/)\.

1. In the left navigation pane, choose **Agents**\.

1. Choose the agent that you want to delete\.

1. Choose **Delete**, enter **delete** in the text box that appears, and then choose **Delete**\.

**To create and activate an agent on a VM or Amazon EC2 instance after deleting an agent**

1. Delete the old agent \(see the preceding steps for instructions\)\. Do not delete the VM or Amazon EC2 instance\.

1. Wait until the old agent is deleted and the VM is ready to be activated, usually about three minutes\. Alternatively, you can verify that the agent has been deleted by checking the status of port 80\. When the VM is ready to be activated, port 80 will be open\.

1. Create and activate a new DataSync agent on the existing VM or Amazon EC2 instance\. For information about creating a DataSync agent, see [Creating an AWS DataSync agent](activating-agent.md)\. The new agent can be activated in a different AWS Region, depending on network connectivity\. 

