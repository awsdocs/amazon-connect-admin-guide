# Set up outbound caller ID<a name="queues-callerid"></a>

This topic explains how to set up your outbound caller ID name and number\. 

**Topics**
+ [Outbound parameters: Set in queue](#set-callerID-name)
+ [How to set the caller ID number dynamically](#using-dynamic-caller-id)
+ [Use E\.164 format for international phone numbers](#international-calls-ccp)
+ [How to specify a custom caller ID number using a [Call phone number](call-phone-number.md) block](#call-number-block-how-it-works)
+ [CNAM](#CNAM)
+ [Avoid labels like "spam"](#enroll-in-CNAM-services)

## Outbound parameters: Set in queue<a name="set-callerID-name"></a>

You set the outbound caller ID name \(such as the name of your company\) and caller ID number in the queue settings\. To edit queue settings, on the navigation menu choose **Routing**, **Queues**, and then choose the queue you want to edit\.

The following image shows an **Edit queue** page with an arrow pointing to the **Outbound caller ID name** and **Outbound caller ID number**\.

![\[The Edit queue page, the Outbound caller ID name and number boxes.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-callerID-callerName.png)

### Outbound caller ID name<a name="outbound-callerID"></a>

The **Outbound caller ID name** is set to the value that is passed from the SIP header\. For example, `Alice<sip:alice@example.com>`\. 

**Important**  
Amazon Connect runs on a SIP\-only infrastructure through our carrier partners\. However, the caller ID name can be delivered to your customers only if the call path across the public telephony network is all on SIP\. Because your customers are on many different networks outside of what Amazon Connect controls, the caller ID name is not guaranteed to be delivered to your customers\. Depending on the country this will be up to 75% effective\.   
To guarantee your caller ID name is delivered to customers, see [Optimize your reputation for outbound calling](optimize-outbound-calling.md) for information about achieving it by using partner solutions\.

### Outbound caller ID number<a name="using-call-number-block"></a>

Only phone numbers that you've [claimed](get-connect-number.md) or [ported to Amazon Connect](port-phone-number.md) can be used as your caller ID number\.

To use an external phone number as your outbound caller ID number, contact AWS Support to see if it's possible\. The phone number needs to be in a [ country we support](https://d1v2gagwb6hfe1.cloudfront.net/Amazon_Connect_Telecoms_Coverage.pdf) for custom caller ID and you'll need to provide [proof of ownership](phone-number-requirements.md)\.

You can set the caller ID number as follows:
+ **[Call phone number](call-phone-number.md) block**: Use this block in an [Outbound whisper flow](create-contact-flow.md#contact-flow-types) to initiate an outbound call to a customer and, optionally, specify a custom caller ID number that is displayed to call recipients\.

  This block is useful when you have multiple telephone numbers used to make outbound calls, but want to consistently display the same company phone number for the caller ID for calls made from your contact center\. 

  You can also use this block with the [Set contact attributes](set-contact-attributes.md) block to set the callback number dynamically\. For example, you can display a certain caller ID number based on the customer's account type\.
+ **Queue:** If no caller ID number is specified in the [Call phone number](call-phone-number.md) block, then the caller ID in the queue settings is used\.

**Important**  
Telecoms regulation limit the telephone numbers that can be used to make outbound calls in various countries\. If you have set up a new number and you are not able to make outbound calls, it may be because you have configured a number that is not permitted to make outbound calls\. Check our [Amazon Connect Telecoms Country Coverage Guide](https://d1v2gagwb6hfe1.cloudfront.net/Amazon_Connect_Telecoms_Coverage.pdf) and [Region requirements for ordering and porting phone numbers](phone-number-requirements.md)\.

### Toll\-free numbers for caller ID<a name="tfn-callerid"></a>

Using toll\-free numbers for outbound communications have a number of limitations\. For example, using a toll\-free number to dial other toll\-free numbers in the United States can result in the number being filtered, blocked, or not properly routed to the destination by carriers\. Toll\-free numbers may be terminated at a higher than expected rate\. If you know you need to call toll\-free numbers in the United States you must use DIDs to make the calls to be guaranteed call delivery\.

If you're using toll\-free numbers outside of the US, refer to the [Amazon Connect Telecoms Country Coverage Guide](https://d1v2gagwb6hfe1.cloudfront.net/Amazon_Connect_Telecoms_Coverage.pdf) to see which countries support toll\-free numbers as outbound\. For example, for Australia the guide shows it's not permitted to use toll\-free numbers due to local regulations; the **National Outbound** column indicates that toll\-free numbers are not supported\. 

**Important**  
Toll\-free products are designed to be national products and phoned within the country\. We do not guarantee international reachability of any of these services as access to the numbers is controlled by the caller's network access\. 

## How to set the caller ID number dynamically<a name="using-dynamic-caller-id"></a>

Use an attribute in the [Call phone number](call-phone-number.md) block to set the caller ID number dynamically during the flow\. 

The attribute can be one you define in the [Set contact attributes](set-contact-attributes.md) block in the flow\. Or, it can be an external attribute returned from an AWS Lambda function\.

The value of the attribute must be a phone number from your instance in [ E\.164](https://www.itu.int/rec/T-REC-E.164/en) format\. 
+ If the number is not in E\.164 format, the number from the queue associated with the [Outbound whisper flow](create-contact-flow.md#contact-flow-types) is used for the caller ID number\.
+ If no number is set for the outbound caller ID number for the queue, the call attempt will fail\.

For more information about setting the caller ID dynamically, see this AWS Support Knowledge Center article: [How can I set my Amazon Connect outbound caller ID dynamically based on country?](https://aws.amazon.com/premiumsupport/knowledge-center/connect-dynamic-outbound-caller-id/) 

## Use E\.164 format for international phone numbers<a name="international-calls-ccp"></a>

Amazon Connect requires phone numbers in [ E\.164](https://www.itu.int/rec/T-REC-E.164/en) format\. 

To express a US phone number in E\.164 format, add the '\+' prefix and the country code in front of the number\. For example, for a US number: 
+  \+1\-800\-555\-1212

In the UK and many other countries internationally, local dialing requires the addition of a 0 in front of the subscriber number\. However, to use E\.164 formatting, this 0 must be removed\. A number such as 020 718 xxxxx in the UK would be formatted as \+44 20 718 xxxxx\. When you place calls from the CCP using Amazon Connect the CCP provides the correct formatting for numbers automatically\.

**Important**  
Phone numbers that are not formatted in E\.164 will not work\. They will also result in a breach of [ Amazon Connect Service Terms and conditions](http://aws.amazon.com/service-terms/) for acceptable use which may result in your service being suspended\.

## How to specify a custom caller ID number using a [Call phone number](call-phone-number.md) block<a name="call-number-block-how-it-works"></a>

1. On the left navigation menu, choose **Routing**, **Flows**\.

1. Choose the down arrow next to **Create flow**, and then choose **Create outbound whisper flow**\.

1. Add a [Call phone number](call-phone-number.md) block to the flow, and connect the **Entry point** block to it\.

   The [Call phone number](call-phone-number.md) block must be placed before a **Play prompt** block if one is included in your flow\.

1. Select the [Call phone number](call-phone-number.md) block, and then select **Caller ID number to display**\.

1. Do one of the following:
   + To use a number from your instance, choose **Select a number from your instance**, and then search for or select the number to use from the drop\-down\.
   + Choose **Use attribute** to use a contact attribute to provide the value for the caller ID number\. You can use either a **User Defined** attribute you create using a [Set contact attributes](set-contact-attributes.md) block, or an **External** attribute returned from an AWS Lambda function\. The value of any attribute you use must be a phone number claimed for your instance and be in E\.164 format\. If the number used from an attribute is not in E\.164 format, the number set for the **Outbound caller ID number** for the queue is used\.
**Important**  
The value of any attribute you use must be a phone number claimed for your instance\. The number must be in E\.164 format\. If the number used from an attribute is not in E\.164 format, calls may be terminated by the destination networks\. 
It is your responsibility to ensure the numbers you are using are legally permissible\. Certain numbers, such as \+44870 numbers in the UK, are not legally permissible\. You must ensure you're not using them\. 

1. Add any additional blocks to complete your flow, and connect the **Success** branch of the [Call phone number](call-phone-number.md) block to the next block in the flow\. 

   There is no error branch for the block\. If a call is not successfully initiated, the flow ends and the agent is placed in an **AfterContactWork** \(ACW\) state\.

## CNAM<a name="CNAM"></a>

As part of changes within the US Public Telephone network and a move to alternative reputation mechanisms described in [Optimize your reputation for outbound calling](optimize-outbound-calling.md), as of March 31, 2023, Amazon Connect no longer sets CNAM configurations\. 

We conducted research between January and March 2023, that showed CNAM was seen by fewer than 7% of users\. This is due to changes within support for mobile providers and due to the migration to app\-based reputation mechanisms\. 

All existing CNAM configurations set up before March 2023, are still in place\. We will continue to focus on supporting modern replacement mechanisms added to our marketplace, for example, [First Orion](https://firstorion.com/amazon-connect-integration/) and [Neustar](https://www.discover.neustar/202208-CS-7654-CR-Partner-Marketing-BCD---Amazon-Connect_0001-LP.html)\. 

## How to avoid labels like "spam" and "telemarketer"<a name="enroll-in-CNAM-services"></a>

See the recommended steps in [Optimize your reputation for outbound calling](optimize-outbound-calling.md)\.