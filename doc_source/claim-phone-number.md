# Claim a phone number in your country<a name="claim-phone-number"></a>

To place or receive calls in your instance, you need to claim a phone number\. If you did not claim a number when you created the instance, follow these steps to claim one now\.

**To claim a number for your contact center**

1. Log in to your contact center at https://*instance name*\.my\.connect\.aws/\.

1. On the navigation menu, choose **Channels**, **Phone numbers**\.

1. Choose **Claim a number**\. You can choose a toll free number or a Direct Inward Dialing \(DID\) number\.
**Note**  
Use the [Amazon Connect service quotas increase form](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-connect) for these situations:   
If you select a country or region, but no numbers display, you can request additional numbers for the country or region\. 
If you want to request a specific area code or prefix that you don't see listed, we'll try to accommodate your request\.

1. Enter a description for the number and, if required, attach it to a contact flow in **Flow / IVR**\.

1. Choose **Save**\.

1. Repeat this process until you have claimed all your required phone numbers\.

There is a service quota for how many phone numbers you can have in each instance\. For the default service quota, see [Amazon Connect service quotas](amazon-connect-service-limits.md)\. If you reach your quota, but want a different phone number, you can release one of previously claimed numbers\. You cannot claim the same phone number after releasing it\. 

If you need more phone numbers, you can request a service quota increase using the [Amazon Connect service quota increase form](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-connect)\.

## API instructions<a name="claim-phone-number-programmatically"></a>

To claim a phone number programmatically, use the [ClaimPhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_ClaimPhoneNumber.html) API\. 

Claiming a number by using the [ClaimPhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_ClaimPhoneNumber.html) API puts the number in one of the following three states\. You can run the [DescribePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_DescribePhoneNumber.html) API to determine the status of your number claiming process\. 
+ `CLAIMED` means the previous [ClaimedPhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_ClaimedPhoneNumber.html) or [UpdatePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdatePhoneNumber.html) operation succeeded\.
+ `IN_PROGRESS` means a [ClaimedPhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_ClaimedPhoneNumber.html) or [UpdatePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdatePhoneNumber.html) operation is still in progress and has not yet completed\. You can call [DescribePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_DescribePhoneNumber.html) at a later time to verify if the previous operation has completed\.
+ `FAILED` indicates that the previous [ClaimedPhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_ClaimedPhoneNumber.html) or [UpdatePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdatePhoneNumber.html) operation has failed\. It will include a message indicating the failure reason\. A common reason for a failure may be that the `TargetArn` value you are claiming or updating a phone number to has reached its limit of total claimed numbers\. If you received a `FAILED` status from a `ClaimPhoneNumber` API call, you have one day to retry claiming the phone number before the number is released back to the inventory for other customers to claim\.

**Note**  
You will not be billed for the phone number during the 1\-day period if number claiming fails\. 

## "You've reached the limit of Phone Numbers\. To increase the limit, contact support\."<a name="phone-number-limit-message"></a>

Even if it's the first time you've claimed a phone number, it's possible to get this error message when you attempt to claim a number\. All the issues that cause this error message require help from AWS Support to resolve\. 

 Contact AWS Support and they will provide assistance\.