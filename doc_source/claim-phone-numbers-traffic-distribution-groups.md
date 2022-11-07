# Claim phone numbers to traffic distribution groups<a name="claim-phone-numbers-traffic-distribution-groups"></a>

**Note**  
This feature is available only for Amazon Connect instances created in the US East \(N\. Virginia\) and US West \(Oregon\) Regions\.   
To obtain access to this feature, contact your Amazon Connect Solutions Architect or Technical Account Manager\.

After your traffic distribution group is created successfully \(`Status` is `ACTIVE`\), you can claim available phone numbers to it by using the [ClaimPhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_ClaimPhoneNumber.html) API\. 

Before you claim a phone number to your traffic distribution group, we recommend using the [DescribeTrafficDistributionGroup](https://docs.aws.amazon.com/connect/latest/APIReference/API_DescribeTrafficDistributionGroup.html) API to verify the status of the traffic distribution group is `ACTIVE`\. Assigning a phone number to a traffic distribution group that isn't `ACTIVE` results in `ResourceNotFoundException`\. 

You can claim a phone number to a traffic distribution group by providing the traffic distribution group ARN in the **TargetArn** parameter when calling the [ClaimPhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_ClaimPhoneNumber.html) API\. You can also use the [UpdatePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdatePhoneNumber.html) API to assign a phone number previously claimed to an instance to a traffic distribution group\. 

**Note**  
To update the **Description** field, you must use the Amazon Connect console\.

## Example workflow<a name="example-workflow-claim"></a>

Following is an example workflow to claim phone numbers and use them across multiple AWS Regions:

1. Create a replica of your instance: 

   1. Call the [ReplicateInstance](https://docs.aws.amazon.com/connect/latest/APIReference/API_ReplicateInstance.html) API\.

1. Create a traffic distribution group that links these instances together:

   1. Call the [CreateTrafficDistributionGroup](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateTrafficDistributionGroup.html) API\.

1. Find available phone numbers that can be claimed to your traffic distribution group:

   1. Call the [SearchAvailablePhoneNumbers](https://docs.aws.amazon.com/connect/latest/APIReference/API_SearchAvailablePhoneNumbers.html) API in the Region where the traffic distribution group was created\. Provide the traffic distribution group ARN for the `TargetArn` parameter\.

1. In the Region where the traffic distribution group was created, call the [ClaimPhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_ClaimPhoneNumber.html) API: 

   1. Provide your traffic distribution group ARN for the `TargetArn` parameter\.

   1. Provide the E164 phone number value that was returned by the [SearchAvailablePhoneNumbers](https://docs.aws.amazon.com/connect/latest/APIReference/API_SearchAvailablePhoneNumbers.html) API call in step 3\.

   A `PhoneNumberId` and `PhoneNumberArn` are returned\. You can use these values for follow\-up operations\. 

1. Verify that the phone number status is `CLAIMED`:

   1. Call the [DescribePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_DescribePhoneNumber.html) API\.

     \(DescribePhoneNumber can also be called in the other Region associated with the traffic distribution group\. It will return the same phone number details\.\)

   The phone number can be used by follow\-up operations only after its status is `CLAIMED`\. 

   For a description of possible statuses, see [Phone number statuses defined](#claim-phone-number-status)\. 

1. Repeat steps 3\-5 for all phone numbers you need to claim to your traffic distribution group\.

1. Perform the following steps to associate flows to phone numbers\. Do them in both Regions where the traffic distribution group operates\. 

   These steps ensure your telephony traffic will route correctly to your flows to support your traffic distribution configuration\.

   1. In your existing Amazon Connect instance in the Region where the traffic distribution group was created, do the following steps:

      1. Call [ListContactFlows](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListContactFlows.html) API\. Provide the `InstanceId` that corresponds to the instance that was replicated\. 

      1. A list of flow ARNs is returned\. Use these flow ARNs to associate a flow to a phone number; call the [AssociatePhoneNumberContactFlow](https://docs.aws.amazon.com/connect/latest/APIReference/API_AssociatePhoneNumberContactFlow.html) API\. 

   1. In the replicated Amazon Connect instance in the other Region, do the following steps:

      1. Call [ListContactFlows](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListContactFlows.html) API\. Provide the `InstanceId` that corresponds to the instance that was replicated\. 

      1. A list of flow ARNs is returned\. Use these flow ARNs to associate a flow to a phone number; call the [AssociatePhoneNumberContactFlow](https://docs.aws.amazon.com/connect/latest/APIReference/API_AssociatePhoneNumberContactFlow.html) API\. 

## Why a ClaimPhoneNumber call fails<a name="why-claimphonenumber-fails"></a>

Your [ClaimPhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_ClaimPhoneNumber.html) API call will fail with a `ResourceNotFoundException` in the following cases:
+ The specified traffic distribution group does not exist, the status of the traffic distribution group is not `ACTIVE`, or you do not have ownership of the traffic distribution group\.
+ The phone number is not available for claiming\. In some cases, a phone number found from [SearchAvailablePhoneNumbers](https://docs.aws.amazon.com/connect/latest/APIReference/API_SearchAvailablePhoneNumbers.html) may have been claimed by another customer\.

[ClaimPhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_ClaimPhoneNumber.html) will fail with a `InvalidParameterException` error in the following case:
+ The endpoint you are calling is not in the same Region where the traffic distribution group was created\.

## Phone number statuses defined<a name="claim-phone-number-status"></a>

Following is a description of phone number statuses:
+ `CLAIMED` means the previous [ClaimPhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_ClaimPhoneNumber.html) or [UpdatePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdatePhoneNumber.html) operation succeeded\.
+ `IN_PROGRESS` means a [ClaimPhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_ClaimPhoneNumber.html), [UpdatePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdatePhoneNumber.html) operation is still in progress and has not yet completed\. You can call [DescribePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_DescribePhoneNumber.html) at a later time to verify if the previous operation has completed\.
+ `FAILED` indicates that the previous [ClaimPhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_ClaimPhoneNumber.html) or [UpdatePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdatePhoneNumber.html) operation has failed\. It includes a message indicating the failure reason\. 

   A common reason for a failure is that the `TargetArn` value you are claiming or updating a phone number to has reached its limit of total claimed numbers\. 

  If you received a `FAILED` status from a `ClaimPhoneNumber` API call, you have one day to retry claiming the phone number before the number is released back to the inventory for other customers to claim\.