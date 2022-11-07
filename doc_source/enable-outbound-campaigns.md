# Enable Amazon Connect outbound campaigns<a name="enable-outbound-campaigns"></a>

This topic explains how to enable Amazon Connect outbound campaigns, a feature of Amazon Connect and formerly known as high\-volume outbound communications\.

## Before you begin<a name="campaign-prereq"></a>

There are a few things that you need in place before using outbound campaigns:
+ Make sure your instance is [enabled for outbound calling](enable-outbound-calls.md)\. 
+ Create a dedicated outbound campaigns queue to handle any contacts that will be routed to agents as a result of the campaign\.
+ Assign the queue to the agent's routing profile\.
+ Create and publish a flow that includes a [Check call progress](check-call-progress.md) block\. This block enables you to branch based on whether a person answered the phone, for example, or a voicemail was detected\.

**Note**  
If you plan to call customers in Australia or New Zealand, see *Step 4: Create a new campaign in the Amazon Connect instance* in this blog for instructions: [ Make predictive and progressive calls using Amazon Connect high\-volume outbound communications](http://aws.amazon.com/blogs/contact-center/make-predictive-and-progressive-calls-using-amazon-connect-high-volume-outbound-communications/)\.

## Create a AWS KMS key<a name="create-kms-key-campaigns"></a>

When you enable outbound campaigns, you have the option to provide your own [AWS KMS key](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html#kms_keys)\. These keys are created and managed by you \(AWS KMS charges apply\)\. You also have the option to use an AWS owned key\. 

When enabling or disabling outbound campaigns using an API, make sure the API user is either the administrator or has the following permissions: `kms:DescribeKey`, `kms:CreateGrant`, and `kms:RetireGrant` for the key\.

**Note**  
To switch the KMS key that is associated with outbound campaigns, first you need to disable outbound campaigns, and then re\-enable it using a different AWS KMS key\.

## Configure outbound campaigns<a name="configure-outbound-campaigns"></a>

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. On the instances page, choose the instance alias\. The instance alias is also your **instance name**, which appears in your Amazon Connect URL\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/instance.png)

1. In the navigation pane, choose **Telephony**\.

1. To enable outbound campaigns, choose **Enable outbound campaigns**\.

1. Under **Encryption settings**, enter your own AWS KMS key or choose **Create an AWS KMS key**\.

   If you choose **Create an AWS KMS key**:
   + A new tab in your browser opens for the Key Management Service \(KMS\) console\. On the **Configure key** page, choose **Symmetric**, and then choose **Next**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-create-kms-key-configure-key.png)
   + On the **Add labels** page, add a name and description for the key, and then choose **Next**\.
   + On the **Define key administrative permissions** page, choose **Next**\.
   + On the **Define key usage permissions** page, choose **Next**\.
   + On the **Review and edit key policy** page, choose **Finish**\.

     In the following example, the name of the key starts with **bcb6fdd**:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-create-kms-key-note-key.png)
   + Return to the tab in your browser for the Amazon Connect console, **Telephony** page\. Click or tap in the **AWS KMS key** for the key you created to appear in a dropdown list\. Choose the key you created\.

1. Choose **Save**\. 

1. It takes a few minutes for outbound campaigns to be enabled\. When it's successfully enabled, you can create outbound campaigns in Amazon Connect for voice calls\. If it does not enable, verify you have the required [IAM permissions](security-iam-amazon-connect-permissions.md)\. 