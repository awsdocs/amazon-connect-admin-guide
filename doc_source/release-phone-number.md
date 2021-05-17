# Release a phone number<a name="release-phone-number"></a>

If you want a different phone number, or have extra numbers that you aren't using, you can release them back to inventory\. 

When a phone number is released from your Amazon Connect instance:
+ You will no longer be charged for it\.
+ You cannot reclaim the phone number\.
+ Amazon Connect reserves the right to allow it to be claimed by another customer\.

**Tip**  
If you want to "close" your Amazon Connect account, do these steps for all of your phone numbers\. This will ensure you aren't billed if people erroneously call numbers that you've claimed, and initiate your contact flows\. You may also want to [delete your instances\.](delete-connect-instance.md) 

**To release a phone number**

1. Log in to your contact center at https://*instance name*\.my\.connect\.aws/\. To find the name of your instance, see [Find your Amazon Connect instance ID/ARN](find-instance-arn.md)\.

1. On the navigation menu, choose **Routing**, **Phone numbers**\.

1. Choose the phone number you want to release, and then choose **Release**\.

If the phone number is associated with a contact flow, that flow will be deactivated until another number is associated with it\.

When customers call the phone number you have released, they will get a message that it is not a working phone number\. 