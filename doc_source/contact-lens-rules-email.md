# Create Contact Lens rules that send email notifications<a name="contact-lens-rules-email"></a>

You can create Contact Lens rules that send email notifications to people in your organization\. This helps you to respond more expediently to potential issues in your contact center\. For example, you can create a rule to notify:
+ A team supervisor when there is an account escalation or cancellation\.
+ A group of people in your contact center as a result of certain words being mentioned during a call\.
+ A designated person in your contact center when a disagreement occurs during the call\.

All emails are sent from `no-reply@amazonconnect.com`\. 

**To create a Contact Lens rule that sends an email notification**

1. Log in to Amazon Connect with a user account that has the [required permissions](permissions-for-rules.md) to create rules\.

1. Navigate to **Analytics and optimization**, **Rules**\.

1. On the **Rules** page, choose **Create a rule**, and then from the dropdown list, choose **Contact lens**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-create-rule.png)

1. On the **New rule** page, define the conditions for the rule\. For more information, see [Step 1: Define conditions](build-rules-for-contact-lens.md#rule-conditions)\. 

1. When you define actions for the rule, choose **Send email notification** for the action\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-rules-email-action.png)

1. In the **Send email notification** section, choose who is going to receive the email by using one of these options: 
   + **Select recipients by login: Routes the email to the specified user\.**
   + **Select recipients by tags**\. Routes the email dynamically based on the agent's tag values\.

   In the following example, the rule sends a notification email to the agent's team supervisor\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-rules-email-tag.png)

1. In **Subject**, add the email subject\. In **Body**, add the contents of the email notification\.

   To specify contact attributes in the body of the email, type **\[** and a list of available attributes appears, as shown in the following image\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-rules-email-attributes.png)

1. Choose **Next**\. Review your selections, and then choose **Save**\.

1. After you add rules, they are applied to new contacts that occur after the rule was added\. Rules are applied when Contact Lens analyzes conversations\.

   You cannot apply rules to past, stored conversations\. 

## Email limits<a name="email-notification-limits"></a>
+ Amazon Connect has a default limit of 500 emails a day\. When that limit is exceeded, the Amazon Connect instance is blocked for 24 hours from sending more email\. This is because the emails are subject to bounce and complaint limits\. For more information, see the **Bounce** and **Complaint** sections in [Understanding email deliverability in Amazon SES](https://docs.aws.amazon.com/ses/latest/dg/send-email-concepts-deliverability.html)\. 
+ All emails are sent from `no-reply@amazonconnect.com`, which you cannot customize\.

Alternatively, you can use your own Amazon Simple Email Service \(Amazon SES\) instance to send emails, as discussed in the next section\. 

## Use Amazon SES to send email notifications<a name="contactlens-ses"></a>

Setting up Amazon Simple Email Service to send email notifications can be useful in the following situations to: 
+ Change `no-reply@amazonconnect.com` to a different email address that you own\.
+ Send more than 500 emails a day\. 
+ Receive delivery, complaint, and bounce reports\. Amazon SES enables you to [monitor sending activity](https://docs.aws.amazon.com/ses/latest/dg/monitor-sending-activity)\. 

**To set up Amazon SES**

1. [Create and verify an email address](https://docs.aws.amazon.com/ses/latest/dg/creating-identities.html#verify-email-addresses-procedure) as your sending identity\. 
**Note**  
Do not choose a domain as your sending identity\. The following setup steps will fail\.

1. [Move your instance out of the Amazon SES sandbox](https://docs.aws.amazon.com/ses/latest/dg/request-production-access.html)\. The sandbox has a limit of 200 emails per day\. If your business needs meet this 200 email limit, we recommend using the Amazon Connect email notification solution instead, because there are fewer steps to setting it up\.

1. Associate your Amazon SES instance to Amazon Connect, using the [CreateIntegrationAssociation](https://docs.aws.amazon.com/sconnect/latest/APIReference/API_CreateIntegrationAssociation.html) API\. 

   Following is a sample integration association command\. Replace EMAIL with an email address that's type `SES_IDENTITY`\.
   + `aws connect create-integration-association --instance-id $your_AmazonConnect_instanceId --integration-type SES_IDENTITY --integration-arn aaaaaaaa-aaaa-aaaa-EXAMPLE012`

     Where `integration-arn` at the end is the Amazon SES ARN of the email ID setup\.

1. You can associate only one Amazon SES instance with your Amazon Connect instance\. 

   **To change the association**, run [DeleteIntegrationAssociation](https://docs.aws.amazon.com/sconnect/latest/APIReference/API_DeleteIntegrationAssociation.html) and then create the association again\. The following example shows how to delete an integration association\.
   + `aws connect delete-integration-association --instance-id $your_AmazonConnect_instanceId --integration-association-id dd2f871a-a312-4d54-EXAMPLE012 `

1. **To verify if the association exists**, run [ListIntegrationAssociations](https://docs.aws.amazon.com/sconnect/latest/APIReference/API_ListIntegrationAssociations.html) as shown in the following example\. 
   + `aws connect list-integration-associations —instance-id $your_AmazonConnect_instanceId —integration-type SES_IDENTITY`

After you complete these steps, emails will be sent from the associated Amazon SES identity\. 

If the associated Amazon SES identity is deleted, emails will be sent from the default ID, `no-reply@amazonconnect.com`\.