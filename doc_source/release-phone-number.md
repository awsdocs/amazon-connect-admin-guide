# Release a phone number<a name="release-phone-number"></a>

If you want a different phone number, or have extra you aren't using you can release them back to inventory\. 

You cannot claim the same phone number after releasing it\.

**Tip**  
If you want to "close" your Amazon Connect account, do these steps for all of your phone numbers\. This will ensure you aren't billed if people erroneously call numbers that you've claimed, and trigger your contact flows\. You may also want to [delete your instances\.](delete-connect-instance.md) 

**To release a phone number**

1. Log in to your contact center at https://*instance name*\.awsapps\.com/connect/\. To find the name of your instance, see [Find your Amazon Connect instance ID/ARN](find-instance-arn.md)\.
**Note**  
IT administrators: In the future, the access URL is going to change\. For the release schedule and technical details, see [Upcoming change: Domain for new Amazon Connect instances is "my\.connect\.aws"New domain for access URL](amazon-connect-release-notes.md#new-domain)\. 

1. On the navigation menu, choose **Routing**, **Phone numbers**\.

1. Choose the phone number you want to release, and then choose **Release**\.

If the phone number is associated with a contact flow, that flow will be deactivated until another number is associated with it\.

When customers call the phone number you've released, they'll get a message that it's not a working phone number\. 