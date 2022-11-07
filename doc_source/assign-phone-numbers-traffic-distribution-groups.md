# Assign claimed phone numbers to traffic distribution groups<a name="assign-phone-numbers-traffic-distribution-groups"></a>
+ You created a new traffic distribution group and it's status is `ACTIVE`\. We recommend using the [DescribeTrafficDistributionGroup](https://docs.aws.amazon.com/connect/latest/APIReference/API_DescribeTrafficDistributionGroup.html) API to verify the status\.
+ You have already claimed phone numbers to instances or other traffic distribution groups\.

 Now you can assign those claimed phone numbers to your new traffic distribution group by using the [UpdatePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdatePhoneNumber.html) API\. Provide the traffic distribution group ARN in the `TargetArn` parameter\. 

**Note**  
To update the **Description** field, you must use the Amazon Connect console\. 

## Example workflow<a name="example-workflow-assign"></a>

Following is an example workflow to assign claimed phone numbers to your traffic distribution group:

1. Call the [UpdatePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdatePhoneNumber.html) API to assign the phone number to a new `TargetArn`\. 

   The `TargetArn` can be for another Amazon Connect instance or for a traffic distribution group created in the same Region where the phone number was initially claimed\. 

1. Perform the following steps to associate flows to phone numbers\. Do them in both Regions where the traffic distribution group operates\. 

   These steps ensure your telephony traffic will route correctly to your flows to support your traffic distribution configuration\.

   1. In your existing Amazon Connect instance in the Region where the traffic distribution group was created, do the following steps:

      1. Call the [ListContactFlows](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListContactFlows.html) API\. Provide the `InstanceId` that corresponds to the instance that was replicated\. 

      1. A list of flow ARNs is returned\. Use these flow ARNs to associate a flow to a phone number; call the [AssociatePhoneNumberContactFlow](https://docs.aws.amazon.com/connect/latest/APIReference/API_AssociatePhoneNumberContactFlow.html) API\. 

   1. In the replicated Amazon Connect instance in the other Region, do the following steps:

      1. Call the [ListContactFlows](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListContactFlows.html) API\. Provide the `InstanceId` that corresponds to the instance that was replicated\. 

      1. A list of flow ARNs is returned\. Use these flow ARNs to associate a flow to a phone number; call the [AssociatePhoneNumberContactFlow](https://docs.aws.amazon.com/connect/latest/APIReference/API_AssociatePhoneNumberContactFlow.html) API\. 

## Why an UpdatePhoneNumber call fails<a name="why-updatephonenumber-fails"></a>

Your [UpdatePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdatePhoneNumber.html) API call will fail with a `ResourceNotFoundException` in the following case:
+ The specified traffic distribution group does not exist, the status of the traffic distribution group is not `ACTIVE`, or you do not have ownership of the traffic distribution group\.

[UpdatePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdatePhoneNumber.html) will fail with a `InvalidParameterException` error in the following case:
+ The endpoint you are calling is not in the same Region where the traffic distribution group was created\.

## Phone number statuses defined<a name="update-phone-number-status"></a>

Following is a description of phone number statuses:
+ `CLAIMED` means the previous [ClaimPhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_ClaimPhoneNumber.html) or [UpdatePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdatePhoneNumber.html) operation succeeded\.
+ `IN_PROGRESS` means a [ClaimPhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_ClaimPhoneNumber.html), [UpdatePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdatePhoneNumber.html) operation is still in progress and has not yet completed\. You can call [DescribePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_DescribePhoneNumber.html) at a later time to verify if the previous operation has completed\.
+ `FAILED` indicates that the previous [ClaimPhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_ClaimPhoneNumber.html) or [UpdatePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdatePhoneNumber.html) operation has failed\. It includes a message indicating the failure reason\. A common reason for a failure is that the `TargetArn` value you are claiming or updating a phone number to has reached its limit of total claimed numbers\.