# Find the flow ID<a name="find-contact-flow-id"></a>

The flow ID is the flow you want to use for inbound Apple Messages for Business messages\. Flows define the experiences for your customer when they begin a new chat\.

You can either reuse an existing flow that you’re already using for voice or chat contacts, or create a new one specifically for Apple Messages for Business contacts\. For instructions about creating a new inbound flow, see [Create an inbound flow](create-contact-flow.md#create-inbound-contact-flow)\. 

For more information about flows, see [Create Amazon Connect Flows](connect-contact-flows.md)\.

**To find your flow ID for Apple Messages for Business**

1. Log in to the Amazon Connect console with an **Admin** account, or an account assigned to a security profile that has permissions to view contact flows\.

1. On the navigation menu, choose **Routing**, **Contact flows**\.

1. Select the flow you want to use\.
**Note**  
Only choose flows that are type **Flow \(inbound\)**\. Apple Messages for Business doesn't work with other flow types, such as **Customer queue**, **Customer hold**, **Customer whisper**, etc\.

1. In the flow designer, expand **Show additional flow information**\.  
![\[A sample flow, the show additional flow information section.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/abc-find-contactflow-id.png)

1. Under the ARN \(Amazon Resource Number\), copy everything after contact\-flow/\. For example, in the following image, you would copy the underlined part\.   
![\[The ARN.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/abc-find-contactflow-id-copy.png)

   1. Notice the **Type** = **Flow \(Inbound\)**\. 

   1. The flow ID is at the end of the ARN\. Only copy this end part\.