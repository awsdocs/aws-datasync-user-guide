# Agent requirements<a name="agent-requirements"></a>

Your AWS DataSync agent must adhere to the requirements that apply to your scenario\. 

**Topics**
+ [Supported hypervisors](#hosts-requirements)
+ [Virtual machine requirements](#hardware)
+ [Amazon EC2 instance requirements](#ec2-instance-types)

## Supported hypervisors<a name="hosts-requirements"></a>

DataSync supports the following hypervisor versions and hosts:
+  **VMware ESXi Hypervisor \(version 6\.5, 6\.7, or 7\.0\)**: A free version of VMware is available on the [VMware website](http://www.vmware.com/products/vsphere-hypervisor/overview.html)\. You also need a VMware vSphere client to connect to the host\. 
**Note**  
 When VMware ends general support for an ESXi hypervisor version, DataSync also ends support for that version\. For information about VMware's supported hypervisor versions, see [VMware lifecycle policy](https://www.vmware.com/support/policies/general.html) on the VMware website\. 

  
+ **Microsoft Hyper\-V Hypervisor \(version 2012 R2, 2016, or 2019\)**: A free, standalone version of Hyper\-V is available at the [Microsoft Download Center](http://www.microsoft.com/en-us/search/Results.aspx?q=hyper-V&form=DLC)\. For this setup, you need a Microsoft Hyper\-V Manager on a Microsoft Windows client computer to connect to the host\.
**Note**  
The DataSync VM is a generation 1 virtual machine\. For more information about the differences between generation 1 and generation 2 VMs, see [Should I create a generation 1 or 2 virtual machine in Hyper\-V?](https://docs.microsoft.com/en-us/windows-server/virtualization/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v) 
+ **Linux Kernel\-based Virtual Machine \(KVM\)**: A free, open\-source virtualization technology\. KVM is included in Linux versions 2\.6\.20 and newer\. AWS DataSync is tested and supported for the CentOS/RHEL 7\.8, Ubuntu 16\.04 LTS, and Ubuntu 18\.04 LTS distributions\. Any other modern Linux distribution might work, but function or performance is not guaranteed\. We recommend this option if you already have a KVM environment up and running and you're already familiar with how KVM works\.
**Note**  
Running KVM on Amazon EC2 isn't supported, and cannot be used for DataSync agents\. To run the agent on Amazon EC2, deploy an agent Amazon Machine Image \(AMI\)\. For more information about deploying an agent AMI on Amazon EC2, see [Deploy your agent as an Amazon EC2 instance](deploy-agents.md#ec2-deploy-agent)\.
+ **Amazon EC2 instance**: DataSync provides an Amazon Machine Image \(AMI\) that contains the DataSync VM image\. For the recommended instance types, see [Amazon EC2 instance requirements](#ec2-instance-types)\.

## Virtual machine requirements<a name="hardware"></a>

When deploying AWS DataSync on\-premises, make sure that the underlying hardware where you deploy the DataSync VM can dedicate the following minimum resources:
+ **Virtual processors**: Four virtual processors assigned to the VM\.
+ **Disk space**: 80 GB of disk space for installation of VM image and system data\. 
+ **RAM**: Depending on your configuration, one of the following:
  + 32 GB of RAM assigned to the VM, for tasks that transfer up to 20 million files\.
  + 64 GB of RAM assigned to the VM, for tasks that transfer more than 20 million files\.

## Amazon EC2 instance requirements<a name="ec2-instance-types"></a>

When deploying a DataSync agent with Amazon EC2, the instance size must be at least 2xlarge\.

We recommend using one of the following instance sizes: 
+ **m5\.2xlarge**: For tasks to transfer up to 20 million files\.
+ **m5\.4xlarge**: For tasks to transfer more than 20 million files\.

**Note**  
An exception to this is if you're running DataSync on a AWS Snowcone device\. Use the default instance snc1\.medium, which provides 2 CPU cores and 4 GiB of memory\.

To connect to an Amazon EC2 agent using SSH, you must use the following cryptographic algorithms:
+ **SSH cipher**: aes128\-ctr
+ **Key exchange**: diffie\-hellman\-group14\-sha1