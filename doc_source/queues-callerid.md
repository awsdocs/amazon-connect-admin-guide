# Set Up Outbound Caller ID<a name="queues-callerid"></a>

There are a few times when your outbound caller ID—your company name and number—will appear to contacts:
+ During customer callbacks\.
+ If an agent makes an outbound call\.

There are a few places where you can specify what your outbound caller ID will be:
+ In a queue\. You can specify both the outbound caller ID name and the phone number\. For instructions, see [Create a Queue](create-queue.md)\.
+ In the **Set callback number** block in a contact flow\. Use this block to set up customer callback\. You can only specify the phone number\. For more information about this block, see [Contact Block Definitions](contact-blocks.md)\. 
+ In the **Call phone number** block in an outbound whisper contact flow\. You can use this block with the **Set contact attributes** block to set the callback number dynamically\. For example, you can display a certain caller ID number based on the customer's account type\. For more information, see [Initiate an Outbound Call](using-call-number-block.md)\. 

## Why Your Caller ID Might Not Appear Correctly to Customers<a name="w11aac13c17c23c11"></a>

When Amazon Connect initiates a call, it sends the callback name and number as the origination party\. However, the information displayed to the person called may not always match the callback name or number you set\. This is because in some cases the callback name is provided by the carrier of the person you're calling\.

What's more, the information may not be up\-to\-date with that carrier, or the number may get passed differently between systems due to hardware or configuration differences\. If this happens, the person you call may not see the phone number, or may see the name of a previously registered owner of the number, instead of the name of the registered person from your organization\.