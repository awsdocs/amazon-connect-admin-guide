# Enable Customer Profiles for your instance<a name="enable-customer-profiles"></a>

Amazon Connect provides pre\-built integrations so you can quickly combine customer information from multiple external applications, with contact history from Amazon Connect\. This allows you to create a customer profile that has all the information agents need during customer interactions in a single place\.

## Before you begin<a name="enable-customer-profiles-requirements"></a>

Following is an overview of key concepts and the information that you'll be prompted for during the setup process\. 

### About the customer profiles domain<a name="customer-profiles-domain"></a>

When you enable Amazon Connect Customer Profiles, you create a customer profiles domain: a container for all data, such as customer profiles, object types, profile keys, and encryption keys\. Following are guidelines for creating Customer Profile domains: 
+ Each Amazon Connect instance can only be associated with one domain\. 
+ You can create multiple domains, but they don't share external application integrations or customer data between each other\. 
+ All the external application integrations you create are at a domain level\. All of the Amazon Connect instances associated with a domain inherit the domain's integrations\. 
+ You can change the association of your Amazon Connect instance from your current domain to a new domain at any time, by choosing a different domain\. This isn't recommended, however, because the customer profiles from the earlier domain won't be moved to the new domain\.

### How do you want to name your customer profiles domain?<a name="enable-customer-profiles-domains"></a>

When you enable customer profiles, you are prompted to provide a friendly domain name that's meaningful to you such as your organization name, for example, *CustomerProfiles\-ExampleCorp*\. You can change the friendly name using the API at any time\.

### Do you want to use a dead\-letter queue?<a name="enable-customer-profiles-deadletterqueue"></a>

A dead\-letter queue is used for reporting errors associated with processing data from external applications\. 

Amazon AppFlow handles connecting to the external application and moving data from it to Amazon Connect Customer Profiles\. Amazon Connect then processes the file\.
+ If an error occurs during the connection or while transporting the data to Amazon Connect, Amazon AppFlow surfaces the error but it doesn't write the error to the dead\-letter queue\.

  For example, a processing error could be that the external data didn’t match the specified schema or that the format of the external data format isn't correct \(currently only JSON is supported\)\.
+ If Amazon Connect encounters an error while processing the file, it writes the error to your dead\-letter queue\. You can look at the queue later and try to reprocess the error\.

When you enable Customer Profiles, you have the option of specifying an Amazon SQS queue as your dead\-letter queue\. If you select this option, add the following resource policy to Amazon SQS so Customer Profiles has permissions to send messages to that queue:

```
{
      "Sid": "Customer Profiles SQS policy",
      "Effect": "Allow",
      "Principal": {
        "Service": "profile.amazonaws.com"
      },
      "Action": "SQS:SendMessage",
      "Resource": "arn:aws:sqs:region:accountID:YourQueueName"
}
```

Step\-by\-step instructions are provided in [Enable Customer Profiles](#enable-customer-profiles-step1)\. For general information, see [Basic examples of Amazon SQS policies](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-basic-examples-of-sqs-policies.html)\.

### Create a CMK to be used by Customer Profiles to encrypt data \(required\)<a name="enable-customer-profiles-awsmanagedkey"></a>

When you enable Customer Profiles, you are prompted to create or provide a AWS Key Management Service [customer master key](https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html#master_keys) \(CMK\)\. Step\-by\-step instructions for creating a CMK are provided in [Enable Customer Profiles](#enable-customer-profiles-step1)\.

All data at rest for Customer Profiles is encrypted under the CMK you choose\. Your customer\-managed CMK is created, owned, and managed by you\. You have full control over the CMK \(AWS KMS charges apply\)\.

If you choose to set up a CMK where someone else is the administrator, it must have a policy that allows `kms:GenerateDataKey`, `kms:CreateGrant`, and `kms:Decrypt` permissions to the Customer Profiles service principal\. For information about how to change a key policy, see [Changing a key policy](https://docs.aws.amazon.com/kms/latest/developerguide/key-policy-modifying.html) in the AWS Key Management Service Developer Guide\.

## Enable Customer Profiles<a name="enable-customer-profiles-step1"></a>

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. On the instances page, choose the instance alias\. The instance alias is also your **instance name**, which appears in your Amazon Connect URL\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/instance.png)

1. In the navigation pane, choose **Customer profiles**\.

   The **Customer profiles domain** page lists the applications that are available for integration\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-domains-page.png)

1. Choose **Enable customer profiles** to get started\.

1. At the **Customer profiles enable** page, choose **Create new domain**\. Under **Specify a domain**, enter a friendly name that's meaningful to you, such as your organization name, for example, *CustomerProfiles\-ExampleCorp*\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-enable-domain.png)

1. Under **Specify dead\-letter queue**, choose whether to send failed events to a dead\-letter queue\. This is helpful if you want to get visibility into data that failed to be ingested\. It also gives you the option to retry these failed data ingestions in the future\. 

   Following are the steps to create a dead\-letter queue:
   + On the **Customer profiles enable** page, choose **Create new or select existing SQS queue** and then choose **Create a new Dead Letter Queue**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-create-dlq-choose.png)
   + A new tab in your browser opens for the Amazon SQS console\. Choose **Create queue**\.
   + On the **Create queue** page, choose **Standard**, then assign a name to your queue\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-create-dlq-name.png)
   + In the **Access policy** section, choose **Advanced**\.

     The Version name, policy ID, and Statement appear\. If needed, update this section to give access to only the appropriate roles\.
   + At the end of the Statement section \(line 15 in the following image\) add a comma after \}, and press `Enter`\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-create-dlq-statement.png)
   +  Then copy and paste the following code:

     ```
     {
           "Sid": "Customer Profiles SQS policy",
           "Effect": "Allow",
           "Principal": {
             "Service": "profile.amazonaws.com"
           },
           "Action": "SQS:SendMessage",
           "Resource": "arn:aws:sqs:region:accountID:YourQueueName"
     }
     ```
   + To replace *region*, *accountID*, and *YourQueueName* with your information, copy and paste the `Resource` information from line 14\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-create-dlq-copyandpaste.png)
   + Choose **Create queue**\.
   + Return to the tab in your browser for the Amazon Connect console, **Customer profiles enable** page\. Click or tap in the **Choose existing SQS queue** box to select the queue you just created from the dropdown list\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-create-dlq-final.png)

1. Under **Specify KMS key**, create or enter your own AWS KMS key for encryption\. Following are the steps to create your AWS KMS key:
   + On the **Customer profiles enable** page, choose **Create an AWS KMS key**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-create-kms-key.png)
   + A new tab in your browser opens for the Key Management Service \(KMS\) console\. On the **Configure key** page, choose **Symmetric**, and then choose **Next**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-create-kms-key-configure-key.png)
   + On the **Add labels** page, add a name and description for the key, and then choose **Next**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-create-kms-key-add-labels.png)
   + On the **Define key administrative permissions** page, choose **Next**\.
   + On the **Define key usage permissions** page, choose **Next**\.
   + On the **Review and edit key policy** page, choose **Finish**\.

     In the following example, the name of the key starts with **bcb6fdd**:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-create-kms-key-note-key.png)
   + Return to the tab in your browser for the Amazon Connect console, **Customer profiles enable** page\. Click or tap in the **Specify KMS key box** for the key you created to appear in a dropdown list\. Choose the key you created\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-create-kms-key-choose-key.png)

1. Choose **Submit**\. The completed page looks similar to the following image\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-enable-final.png)

You're done\! Amazon Connect Customer Profiles is enabled\. Now with every new contact that comes in, Amazon Connect creates a customer profile record\. It then tracks the contact history for that phone number \(voice\) or email address \(chat\)\.

Your agents can [create new customer profiles](create-new-customer-profile.md) and view contact trace records for your customers\. 

You can also integrate with external applications that provide customer profile data\. For more information, see [Integrate external applications with Customer Profiles](integrate-external-apps-customer-profiles.md)\.