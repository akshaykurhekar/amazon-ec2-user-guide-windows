# How Reserved Instances are applied<a name="apply_ri"></a>

If you purchase a Reserved Instance and you already have a running instance that matches the specifications of the Reserved Instance, the billing benefit is immediately applied\. You do not have to restart your instances\. If you do not have an eligible running instance, launch an instance and ensure that you match the same criteria that you specified for your Reserved Instance\. For more information, see [Use your Reserved Instances](using-reserved-instances.md)\.

Reserved Instances apply to usage in the same manner, irrespective of the offering type \(Standard or Convertible\), and are automatically applied to running On\-Demand Instances with matching attributes\.

## How zonal Reserved Instances are applied<a name="apply-zonal-ri"></a>

Reserved Instances assigned to a specific Availability Zone provide the Reserved Instance discount to matching instance usage in that Availability Zone\. For example, if you purchase two `c4.xlarge` default tenancy Linux/Unix Standard Reserved Instances in Availability Zone us\-east\-1a, then up to two `c4.xlarge` default tenancy Linux/Unix instances running in the Availability Zone us\-east\-1a can benefit from the Reserved Instance discount\. The attributes \(tenancy, platform, Availability Zone, instance type, and instance size\) of the running instances must match that of the Reserved Instances\.

## How regional Reserved Instances are applied<a name="apply-regional-ri"></a>

Regional Reserved Instances are purchased for a Region and provide Availability Zone flexibility\. The Reserved Instance discount applies to instance usage in any Availability Zone in that Region\. 

Regional Reserved Instances also provide instance size flexibility where the Reserved Instance discount applies to instance usage within the instance family, regardless of size\.

**Limitations for instance size flexibility**

Instance size flexibility does not apply to the following Reserved Instances:
+ Reserved Instances that are purchased for a specific Availability Zone \(zonal Reserved Instances\)
+ Reserved Instances with dedicated tenancy
+ Reserved Instances for Windows Server, Windows Server with SQL Standard, Windows Server with SQL Server Enterprise, Windows Server with SQL Server Web, RHEL, and SUSE Linux Enterprise Server
+ Reserved Instances for G4dn instances

### Instance size flexibility determined by normalization factor<a name="ri-normalization-factor"></a>

Instance size flexibility is determined by the normalization factor of the instance size\. The discount applies either fully or partially to running instances of the same instance family, depending on the instance size of the reservation, in any Availability Zone in the Region\. The only attributes that must be matched are the instance family, tenancy, and platform\. 

Instance size flexibility is applied from the smallest to the largest instance size within the instance family based on the normalization factor\. 

The following table lists the different sizes within an instance family, and the corresponding normalization factor per hour\. This scale is used to apply the discounted rate of Reserved Instances to the normalized usage of the instance family\.


| Instance size | Normalization factor | 
| --- | --- | 
| nano | 0\.25 | 
| micro | 0\.5 | 
| small | 1 | 
| medium | 2 | 
| large | 4 | 
| xlarge | 8 | 
| 2xlarge | 16 | 
| 3xlarge | 24 | 
| 4xlarge | 32 | 
| 6xlarge | 48 | 
| 8xlarge | 64 | 
| 9xlarge | 72 | 
| 10xlarge | 80 | 
| 12xlarge | 96 | 
| 16xlarge | 128 | 
| 18xlarge | 144 | 
| 24xlarge | 192 | 
| 32xlarge | 256 | 

For example, a `t2.medium` instance has a normalization factor of 2\. If you purchase a `t2.medium` default tenancy Amazon Linux/Unix Reserved Instance in the US East \(N\. Virginia\) and you have two running `t2.small` instances in your account in that Region, the billing benefit is applied in full to both instances\. 

![\[Applying a Regional Reserved Instance\]](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/images/ri-instance-flex-full.png)

Or, if you have one `t2.large` instance running in your account in the US East \(N\. Virginia\) Region, the billing benefit is applied to 50% of the usage of the instance\.

![\[Applying a Regional Reserved Instance\]](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/images/ri-instance-flex-partial.png)

The normalization factor is also applied when modifying Reserved Instances\. For more information, see [Modify Reserved Instances](ri-modifying.md)\.

#### Normalization factor for bare metal instances<a name="ri-normalization-factor-bare-metal"></a>

Instance size flexibility also applies to bare metal instances within the instance family\. If you have regional Amazon Linux/Unix Reserved Instances with shared tenancy on bare metal instances, you can benefit from the Reserved Instance savings within the same instance family\. The opposite is also true: if you have regional Amazon Linux/Unix Reserved Instances with shared tenancy on instances in the same family as a bare metal instance, you can benefit from the Reserved Instance savings on the bare metal instance\. 

The `metal` instance size does not have a single normalization factor\. A bare metal instance has the same normalization factor as the equivalent virtualized instance size within the same instance family\. For example, an `i3.metal` instance has the same normalization factor as an `i3.16xlarge` instance\.


| Instance size | Normalization factor | 
| --- | --- | 
|  m5zn\.metal \| z1d\.metal  | 96 | 
|  i3\.metal \|  | 128 | 
| c5n\.metal | 144 | 
|  c5\.metal \| c5d\.metal \| i3en\.metal \| m5\.metal \| m5d\.metal \| m5dn\.metal \| m5n\.metal \| r5\.metal \| r5b\.metal \| r5d\.metal \| r5dn\.metal \| r5n\.metal  | 192 | 

For example, an `i3.metal` instance has a normalization factor of 128\. If you purchase an `i3.metal` default tenancy Amazon Linux/Unix Reserved Instance in the US East \(N\. Virginia\), the billing benefit can apply as follows:
+ If you have one running `i3.16xlarge` in your account in that Region, the billing benefit is applied in full to the `i3.16xlarge` instance \(`i3.16xlarge` normalization factor = 128\)\.
+ Or, if you have two running `i3.8xlarge` instances in your account in that Region, the billing benefit is applied in full to both `i3.8xlarge` instances \(`i3.8xlarge` normalization factor = 64\)\.
+ Or, if you have four running `i3.4xlarge` instances in your account in that Region, the billing benefit is applied in full to all four `i3.4xlarge` instances \(`i3.4xlarge` normalization factor = 32\)\.

The opposite is also true\. For example, if you purchase two `i3.8xlarge` default tenancy Amazon Linux/Unix Reserved Instances in the US East \(N\. Virginia\), and you have one running `i3.metal` instance in that Region, the billing benefit is applied in full to the `i3.metal` instance\.

## Examples of applying Reserved Instances<a name="ri-usage-examples"></a>

The following scenarios cover the ways in which Reserved Instances are applied\.

**Example Scenario 1: Reserved Instances in a single account**  
You are running the following On\-Demand Instances in account A:  
+ 4 x `m3.large` Linux, default tenancy instances in Availability Zone us\-east\-1a
+ 2 x `m4.xlarge` Amazon Linux, default tenancy instances in Availability Zone us\-east\-1b
+ 1 x `c4.xlarge` Amazon Linux, default tenancy instances in Availability Zone us\-east\-1c
You purchase the following Reserved Instances in account A:  
+ 4 x `m3.large` Linux, default tenancy Reserved Instances in Availability Zone us\-east\-1a \(capacity is reserved\)
+ 4 x `m4.large` Amazon Linux, default tenancy Reserved Instances in Region us\-east\-1
+ 1 x `c4.large` Amazon Linux, default tenancy Reserved Instances in Region us\-east\-1
The Reserved Instance benefits are applied in the following way:  
+ The discount and capacity reservation of the four `m3.large` zonal Reserved Instances is used by the four `m3.large` instances because the attributes \(instance size, Region, platform, tenancy\) between them match\.
+ The `m4.large` regional Reserved Instances provide Availability Zone and instance size flexibility, because they are regional Amazon Linux Reserved Instances with default tenancy\.

  An `m4.large` is equivalent to 4 normalized units/hour\.

  You've purchased four `m4.large` regional Reserved Instances, and in total, they are equal to 16 normalized units/hour \(4x4\)\. Account A has two `m4.xlarge` instances running, which is equivalent to 16 normalized units/hour \(2x8\)\. In this case, the four `m4.large` regional Reserved Instances provide the billing benefit to an entire hour of usage of the two `m4.xlarge` instances\.
+ The `c4.large` regional Reserved Instance in us\-east\-1 provides Availability Zone and instance size flexibility, because it is a regional Amazon Linux Reserved Instance with default tenancy, and applies to the `c4.xlarge` instance\. A `c4.large` instance is equivalent to 4 normalized units/hour and a `c4.xlarge` is equivalent to 8 normalized units/hour\.

  In this case, the `c4.large` regional Reserved Instance provides partial benefit to `c4.xlarge` usage\. This is because the `c4.large` Reserved Instance is equivalent to 4 normalized units/hour of usage, but the `c4.xlarge` instance requires 8 normalized units/hour\. Therefore, the `c4.large` Reserved Instance billing discount applies to 50% of `c4.xlarge` usage\. The remaining `c4.xlarge` usage is charged at the On\-Demand rate\.

**Example Scenario 2: Regional Reserved Instances in linked accounts**  
Reserved Instances are first applied to usage within the purchasing account, followed by qualifying usage in any other account in the organization\. For more information, see [Reserved Instances and consolidated billing](concepts-reserved-instances-application.md#concepts-reserved-instances-billing)\. For regional Reserved Instances that offer instance size flexibility, the benefit is applied from the smallest to the largest instance size within the instance family\.  
You're running the following On\-Demand Instances in account A \(the purchasing account\):  
+ 2 x `m4.xlarge` Linux, default tenancy instances in Availability Zone us\-east\-1a
+ 1 x `m4.2xlarge` Linux, default tenancy instances in Availability Zone us\-east\-1b
+ 2 x `c4.xlarge` Linux, default tenancy instances in Availability Zone us\-east\-1a
+ 1 x `c4.2xlarge` Linux, default tenancy instances in Availability Zone us\-east\-1b
Another customer is running the following On\-Demand Instances in account B—a linked account:  
+ 2 x `m4.xlarge` Linux, default tenancy instances in Availability Zone us\-east\-1a
You purchase the following regional Reserved Instances in account A:  
+ 4 x `m4.xlarge` Linux, default tenancy Reserved Instances in Region us\-east\-1
+ 2 x `c4.xlarge` Linux, default tenancy Reserved Instances in Region us\-east\-1
The regional Reserved Instance benefits are applied in the following way:  
+ The discount of the four `m4.xlarge` Reserved Instances is used by the two `m4.xlarge` instances and the single `m4.2xlarge` instance in account A \(purchasing account\)\. All three instances match the attributes \(instance family, Region, platform, tenancy\)\. The discount is applied to instances in the purchasing account \(account A\) first, even though account B \(linked account\) has two `m4.xlarge` that also match the Reserved Instances\. There is no capacity reservation because the Reserved Instances are regional Reserved Instances\.
+ The discount of the two `c4.xlarge` Reserved Instances applies to the two `c4.xlarge` instances, because they are a smaller instance size than the `c4.2xlarge` instance\. There is no capacity reservation because the Reserved Instances are regional Reserved Instances\.

**Example Scenario 3: Zonal Reserved Instances in a linked account**  
In general, Reserved Instances that are owned by an account are applied first to usage in that account\. However, if there are qualifying, unused Reserved Instances for a specific Availability Zone \(zonal Reserved Instances\) in other accounts in the organization, they are applied to the account before regional Reserved Instances owned by the account\. This is done to ensure maximum Reserved Instance utilization and a lower bill\. For billing purposes, all the accounts in the organization are treated as one account\. The following example might help explain this\.  
You're running the following On\-Demand Instance in account A \(the purchasing account\):  
+ 1 x `m4.xlarge` Linux, default tenancy instance in Availability Zone us\-east\-1a
A customer is running the following On\-Demand Instance in linked account B:  
+ 1 x `m4.xlarge` Linux, default tenancy instance in Availability Zone us\-east\-1b
You purchase the following regional Reserved Instances in account A:  
+ 1 x `m4.xlarge` Linux, default tenancy Reserved Instance in Region us\-east\-1
A customer also purchases the following zonal Reserved Instances in linked account C:  
+ 1 x `m4.xlarge` Linux, default tenancy Reserved Instances in Availability Zone us\-east\-1a
The Reserved Instance benefits are applied in the following way:  
+ The discount of the `m4.xlarge` zonal Reserved Instance owned by account C is applied to the `m4.xlarge` usage in account A\.
+ The discount of the `m4.xlarge` regional Reserved Instance owned by account A is applied to the `m4.xlarge` usage in account B\.
+ If the regional Reserved Instance owned by account A was first applied to the usage in account A, the zonal Reserved Instance owned by account C remains unused and usage in account B is charged at On\-Demand rates\.

For more information, see [Reserved Instances in the Billing and Cost Management Report](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/billing-reports.html#enhanced-RI)\.