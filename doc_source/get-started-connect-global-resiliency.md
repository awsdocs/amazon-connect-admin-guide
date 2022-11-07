# Get started with Amazon Connect Global Resiliency<a name="get-started-connect-global-resiliency"></a>

**Note**  
This feature is available only for Amazon Connect instances created in the US East \(N\. Virginia\) and US West \(Oregon\) Regions\.   
To obtain access to this feature, contact your Amazon Connect Solutions Architect or Technical Account Manager\.

You get started with Amazon Connect Global Resiliency by creating a replica of your existing Amazon Connect instance in another AWS Region, and by creating a traffic distribution group\. 

A *traffic distribution group* is an Amazon Connect resource that enables you to link Amazon Connect instances that are in different AWS Regions\. Phone numbers can be attached to the traffic distribution group\. Traffic to these numbers can be distributed between the instances in the traffic distribution group\. 

## How to set up Amazon Connect Global Resiliency<a name="howto-setup-gr"></a>

1. [Create a replica of your existing Amazon Connect instance](create-replica-connect-instance.md)\. Use the [ReplicateInstance](https://docs.aws.amazon.com/connect/latest/APIReference/API_ReplicateInstance.html) API\.

1. [Create a traffic distribution group](setup-traffic-distribution-groups.md)\.

   1. Use the [CreateTrafficDistributionGroup](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateTrafficDistributionGroup.html) API\.

   1. Use [DescribeTrafficDistributionGroup](https://docs.aws.amazon.com/connect/latest/APIReference/API_DescribeTrafficDistributionGroup.html) API to determine whether the traffic distribution group has been created successfully \(`Status` must be `ACTIVE`\)\.

1. [Claim phone numbers to your traffic distribution group](claim-phone-numbers-traffic-distribution-groups.md)\. After your traffic distribution group has been created successfully \(`Status` is `ACTIVE`\), you can claim phone numbers to it using the [ClaimPhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_ClaimPhoneNumber.html) API\. 
**Note**  
The default traffic distribution for these phone numbers is set to 100% \- 0%\. That is, 100% of inbound telephony traffic will go to the source Amazon Connect instance that was used to create a replica\.   
In addition, after phone numbers are claimed to an instance, you can assign them to multiple instances across AWS Regions\. To do this, use the [UpdatePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdatePhoneNumber.html) API to assign the numbers to a traffic distribution group\.

1. [Update your traffic distribution](update-telephony-traffic-distribution.md)\. Use the [UpdateTrafficDistribution](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateTrafficDistribution.html) API to distribute traffic across the linked instances in 10% increments\. 