# Find the contact flow ID<a name="find-contact-flow-id"></a>

The contact flow ID is the contact flow you want to use for inbound Apple Business Chat messages\. Contact flows define the experiences for your customer when they begin a new chat\.

You can either reuse an existing contact flow that you’re already using for voice or chat contacts, or create a new one specifically for Apple Business Chat contacts\. For instructions about creating a new inbound contact flow, see [Create an inbound contact flow](create-contact-flow.md#create-inbound-contact-flow)\. 

For more information about contact flows, see [Create Amazon Connect contact flowsCreate contact flows](connect-contact-flows.md)\.

**To find your contact flow ID for Apple Business Chat**

1. Log in to the Amazon Connect console with an **Admin** account, or an account assigned to a security profile that has permissions to view contact flows\.

1. On the navigation menu, choose **Routing**, **Contact flows**\.

1. Select the contact flow you want to use\.
**Note**  
Only choose flows that are type **Contact flow \(inbound\)**\. Apple Business Chat doesn't work with other contact flow types, such as **Customer queue**, **Customer hold**, **Customer whisper**, etc\.

1. In the contact flow designer, expand **Show additional flow information**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/abc-find-contactflow-id.png)

1. Under the ARN \(Amazon Resource Number\), copy everything after contact\-flow/\. For example, in the following image, you would copy the underlined part\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/abc-find-contactflow-id-copy.png)

   1. Notice the **Type** = **Contact flow \(Inbound\)**\. 

   1. The contact flow ID is at the end of the ARN\. Only copy this end part\.