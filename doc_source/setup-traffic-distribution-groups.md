# Create traffic distribution groups<a name="setup-traffic-distribution-groups"></a>

You can create a traffic distribution group for your existing Amazon Connect instance by using the [CreateTrafficDistributionGroup](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateTrafficDistributionGroup.html) API\. 

A *traffic distribution group* is an Amazon Connect resource that enables you to link Amazon Connect instances that are in different AWS Regions\. Phone numbers can be attached to the traffic distribution group\. Traffic to these numbers can be distributed between the instances in the traffic distribution group\. 

## Important things to know<a name="important-tips-tdg"></a>
+ When creating a traffic distribution group, it must be created in the source AWS Region\. A *source Region* is the Region where you set up your existing Amazon Connect instance\.
+ When associating phone numbers to a traffic distribution group:
  + You can associate only phone numbers that are claimed in the source Region\.
  + The phone number must be in the same Region as where the traffic distribution group was created\.
+ You can claim numbers to a traffic distribution group, or get or update traffic distribution for a traffic distribution group only when its `Status` is `ACTIVE`\. Use the [DescribeTrafficDistributionGroup](https://docs.aws.amazon.com/connect/latest/APIReference/API_DescribeTrafficDistributionGroup.html) API to determine whether it has been created successfully \(`Status` must be `ACTIVE`\)\. 

## Traffic distribution group statuses<a name="tdg-statuses"></a>

Following is a description of the traffic distribution group statuses:
+ `CREATION_IN_PROGRESS`: Traffic distribution group creation is in progress\.
+ `ACTIVE`: Traffic distribution group has been created\.
+ `CREATION_FAILED`: Traffic distribution group creation failed\.
+ `PENDING_DELETION`: Traffic distribution group deletion is in progress\.
+ `DELETION_FAILED`: Traffic distribution group deletion failed\.
+ `UPDATE_IN_PROGRESS`: Traffic distribution group update is in progress\.

## Why a CreateTrafficDistributionGroup call fails<a name="why-createtrafficdistributiongroup-fails"></a>

A [CreateTrafficDistributionGroup](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateTrafficDistributionGroup.html) API call fails with an `InvalidRequestException` in the following cases:
+ The [ReplicateInstance](https://docs.aws.amazon.com/connect/latest/APIReference/API_ReplicateInstance.html) API was not called before creating a traffic distribution group for the linked instances\.
+ The [CreateTrafficDistributionGroup](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateTrafficDistributionGroup.html) API was not called in the same Region where the [ReplicateInstance](https://docs.aws.amazon.com/connect/latest/APIReference/API_ReplicateInstance.html) API was called\. The Region where this API is called must match the Region of the instance that was used to create a replica\.