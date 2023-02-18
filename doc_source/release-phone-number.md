# Release a phone number<a name="release-phone-number"></a>

If you want a different phone number, or have extra numbers that you aren't using, you can release them back to inventory\. You can do this using the Amazon Connect console, or programmatically using the [ReleasePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_ReleasePhoneNumber.html) API\.

When a phone number is released from your Amazon Connect instance:
+ You will no longer be charged for it\.
+ You cannot reclaim the phone number\.
+ Amazon Connect reserves the right to allow it to be claimed by another customer\.

**Tip**  
If you want to close your Amazon Connect account, do these steps for all of your phone numbers\. This will ensure you aren't billed if people erroneously call numbers that you've claimed, and initiate your flows\. You may also want to [delete your instances\.](delete-connect-instance.md) 

**To release a phone number**

1. Log in to Amazon Connect at https://*instance name*\.my\.connect\.aws/\. To find the name of your instance, see [Find your Amazon Connect instance ID/ARN](find-instance-arn.md)\.

1. On the navigation menu, choose **Channels**, **Phone numbers**\.

1. Choose the phone number you want to release, and then choose **Release**\.

If the phone number is associated with a flow, that flow will be deactivated until another number is associated with it\.

When customers call the phone number you have released, they will get a message that it is not a working phone number\. 

**To use the ReleasePhoneNumber API**
+ Releasing a number by using the [ReleasePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_ReleasePhoneNumber.html) API puts the number in a cool down period for 30 days\. The phone number cannot be searched for or claimed until after the cool down period ends\.
**Note**  
You will not be billed for the phone number during the 30\-day cool down period\.