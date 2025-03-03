# Attach an Amazon EBS volume to an instance<a name="ebs-attaching-volume"></a>

You can attach an available EBS volume to one or more of your instances that is in the same Availability Zone as the volume\.

For information about adding EBS volumes to your instance at launch, see [Instance block device mapping](block-device-mapping-concepts.md#instance-block-device-mapping)\.

**Prerequisites**
+ Determine how many volumes you can attach to your instance\. For more information, see [Instance volume limits](volume_limits.md)\.
+ If a volume is encrypted, it can only be attached to an instance that supports Amazon EBS encryption\. For more information, see [Supported instance types](EBSEncryption.md#EBSEncryption_supported_instances)\.
+ If a volume has an AWS Marketplace product code:
  + The volume can only be attached to a stopped instance\.
  + You must be subscribed to the AWS Marketplace code that is on the volume\.
  + The configuration \(instance type, operating system\) of the instance must support that specific AWS Marketplace code\. For example, you cannot take a volume from a Windows instance and attach it to a Linux instance\.
  + AWS Marketplace product codes are copied from the volume to the instance\.

**To attach an EBS volume to an instance using the console**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, choose **Elastic Block Store**, **Volumes**\.

1. Select an available volume and choose **Actions**, **Attach Volume**\.

1. For **Instance**, start typing the name or ID of the instance\. Select the instance from the list of options \(only instances that are in the same Availability Zone as the volume are displayed\)\.

1. For **Device**, you can keep the suggested device name, or type a different supported device name\. For more information, see [Device names on Windows instances](device_naming.md)\.

1. Choose **Attach**\.

1. Connect to your instance and mount the volume\. For more information, see [Make an Amazon EBS volume available for use on Windows](ebs-using-volumes.md)\.

**To attach an EBS volume to an instance using the command line**

You can use one of the following commands\. For more information about these command line interfaces, see [Access Amazon EC2](concepts.md#access-ec2)\.
+ [attach\-volume](https://docs.aws.amazon.com/cli/latest/reference/ec2/attach-volume.html) \(AWS CLI\)
+ [Add\-EC2Volume](https://docs.aws.amazon.com/powershell/latest/reference/items/Add-EC2Volume.html) \(AWS Tools for Windows PowerShell\)

**Note**  
In some situations, you may find that a volume other than the volume attached to `/dev/xvda` or `/dev/sda` has become the root volume of your instance\. This can happen when you have attached the root volume of another instance, or a volume created from the snapshot of a root volume, to an instance with an existing root volume\. For more information, see [Boot from the wrong volume](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-booting-from-wrong-volume.html)\.