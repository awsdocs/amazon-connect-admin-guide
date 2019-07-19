# Initiate an Outbound Call<a name="using-call-number-block"></a>

Use the **Call phone number** block in an outbound whisper flow to initiate an outbound call to a customer and, optionally, specify a custom caller ID number that is displayed to call recipients\. This is useful when you have multiple telephone numbers used to make outbound calls, but want to consistently display the same company phone number for the caller ID for calls made from your contact center\. You can also use the block to display a phone number for a specific line of business, or for displaying different numbers to customers based on their account type\.

There are two ways you can set up how caller ID works for outbound calls: 
+ Select any phone number from your instance\.
+ Or, use an attribute to set the number dynamically during the contact flow\. 

## About Using Dynamic Caller ID<a name="using-dynamic-caller-id"></a>

If you use an attribute to set the caller ID number dynamically, the attribute can be one you define in the **Set contact attributes** block in the contact flow\. Or, it can be an external attribute returned from an AWS Lambda function\.

The value of the attribute must be a phone number from your instance in E\.164 format\. 
+ If the number is not in E\.164 format, the number from the queue associated with the outbound whisper flow is used for the caller ID number\.
+ If no number is set for the outbound caller ID number for the queue, the call attempt will fail\.

 For more information about E\.164, see [Use E\.164 Format for Telephone Numbers](amazon-connect-contact-control-panel.md#international-calls-ccp)\.

## How Caller ID Works in Call phone number Block<a name="call-number-block-how-it-works"></a>

Outbound whisper flows execute in Amazon Connect immediately after an agent accepts the call during direct dial and callback scenarios\. When the contact flow executes: 
+ The caller ID number is set if one is specified in the **Call phone number** block\.
+ If no caller ID is specified in the **Call phone number** block, the caller ID number defined for the queue is used when the call is placed
+ When there is an error with a call that is initiated by the **Call phone number** block, the call is disconnected and the agent is placed in ACW status\.

The **Call phone number** block is supported only in outbound whisper flow contact flows\. Only published contact flows can be selected as the outbound whisper flow for a queue\.

## Specify a Custom Caller ID Number Using a **Call phone number** Block

1. In Amazon Connect choose **Routing**, **Contact flows**\.

1. Choose the down arrow next to **Create contact flow**, and then choose **Create outbound whisper flow**\.

1. Add a **Call phone number** block to the flow, and connect the **Entry point** block to it\.

   The **Call phone number** block must be placed before a **Play prompt** block if one is included in your contact flow\.

1. Select the **Call phone number** block, and then select **Caller ID number to display**\.

1. Do one of the following:
   + To use a number from your instance, choose **Select a number from your instance**, and then search for or select the number to use from the drop\-down\.
   + Choose **Use attribute** to use a contact attribute to provide the value for the caller ID number\. You can use either a **User Defined** attribute you create using a **Set contact attributes** block, or an **External** attribute returned from an AWS Lambda function\. The value of any attribute you use must be a phone number claimed for your instance and be in E\.164 format\. If the number used from an attribute is not in E\.164 format, the number set for the **Outbound caller ID number** for the queue is used\.

1. Add any additional blocks to complete your contact flow, and connect the **Success** branch of the **Call phone number** block to the next block in the flow\. Note that there is no error branch for the block\. If a call is not successfully initiated, the contact flow ends and the agent is placed in an **AfterCallWork** \(ACW\) state\.