# Compatibility for changing the instance type<a name="resize-limitations"></a>

You can change the instance type only if the instance's current configuration is compatible with the instance type that you want\. If the instance type that you want is not compatible with the instance's current configuration, you must launch a new instance with a configuration that is compatible with the instance type, and then migrate your application to the new instance\.

For compatibility information for changing Linux instance types, see [Compatibility for changing the instance type](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/resize-limitations.html) in the *User Guide for Linux Instances*\.

Compatibility is determined in the following ways:

**Architecture**  
AMIs are specific to the architecture of the processor, so you must select an instance type with the same processor architecture as the current instance type\. For example:  
+ If the current instance type has a processor based on the Arm architecture, you are limited to the instance types that support a processor based on the Arm architecture, such as C6g and M6g\.
+ The following instance types are the only instance types that support 32\-bit AMIs: `t2.nano`, `t2.micro`, `t2.small`, `t2.medium`, `c3.large`, `t1.micro`, `m1.small`, `m1.medium`, and `c1.medium`\. If you are changing the instance type of a 32\-bit instance, you are limited to these instance types\.

**Network**  
Newer instance types must be launched in a VPC\. Therefore, if the instance is in the EC2\-Classic platform, you can't change the instance type to one that is available only in a VPC unless you have a nondefault VPC\. To check whether your instance is in a VPC, check the **VPC ID** value on the details pane of the **Instances** screen in the Amazon EC2 console\. For more information, see [Migrate from EC2\-Classic to a VPC](vpc-migrate.md)\.

**Network adapters**  
If you switch from a driver for one network adapter to another, the network adapter settings are reset when the operating system creates the new adapter\. To reconfigure the settings, you might need access to a local account with administrator permissions\. The following are examples of moving from one network adapter to another:  
+ AWS PV \(T2 instances\) to Intel 82599 VF \(M4 instances\)
+ Intel 82599 VF \(most M4 instances\) to ENA \(M5 instances\)
+ ENA \(M5 instances\) to high\-bandwidth ENA \(M5n instances\)

**Enhanced networking**  
Instance types that support [enhanced networking](enhanced-networking.md) require the necessary drivers installed\. For example, instances based on the [Nitro System](instance-types.md#ec2-nitro-instances) require EBS\-backed AMIs with the Elastic Network Adapter \(ENA\) drivers installed\. To change from an instance type that does not support enhanced networking to an instance type that supports enhanced networking, you must install the [ENA drivers](enhanced-networking-ena.md) or [ixgbevf drivers](sriov-networking.md) on the instance, as appropriate\.

**NVMe**  
EBS volumes are exposed as NVMe block devices on instances built on the [Nitro System](instance-types.md#ec2-nitro-instances)\. If you change from an instance type that does not support NVMe to an instance type that supports NVMe, you must first install the [NVMe drivers](nvme-ebs-volumes.md) on your instance\. Also, the device names for devices that you specify in the block device mapping are renamed using NVMe device names \(`/dev/nvme[0-26]n1`\)\.

**AMI**  
For information about the AMIs required by instance types that support enhanced networking and NVMe, see the Release Notes in the following documentation:  
+ [General purpose instances](general-purpose-instances.md)
+ [Compute optimized instances](compute-optimized-instances.md)
+ [Memory optimized instances](memory-optimized-instances.md)
+ [Storage optimized instances](storage-optimized-instances.md)