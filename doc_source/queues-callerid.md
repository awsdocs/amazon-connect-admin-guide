# Set up outbound caller ID<a name="queues-callerid"></a>

We recommend setting your outbound caller ID\. Not doing so may result in some PSTN carriers considering your outbound calls fraudulent activity, and they may drop them\. 

There are a few times when your outbound caller ID—your company name and number—will appear to contacts:
+ During customer callbacks\.
+ If an agent makes an outbound call\.
+ If an agent transfers a call, for example, to an external number\.

## Caller ID name: Set in queue<a name="set-callerID-name"></a>

You set the caller ID name, such as the name of your company, in the queue settings\. To edit queue settings, on the navigation menu choose **Routing**, **Queues**, and then choose the queue you want to edit\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-callerID-callerName.png)

**If your DID/TFN phone number is in the US/CANADA:** The name you use should be the same one that's registered in the CNAM \(Caller Name\) database provided by Amazon Connect; this is a nationwide resource available in the US/CANADA to provide the name of the calling party on incoming calls if recipients subscribe to CNAM services from their telecom carrier\.

Open an AWS Support ticket to register your US based phone number with your company name in the CNAM database of the Amazon Connect carrier\. We'll handle the registration process for you\. **It may take up to 30 days for the caller ID names to propagate through the database\.** 

**If you are using CNAM phoning into CANADA**, the end network may support Caller ID lookups, but this functionality is not guaranteed, as not all receiving networks support this feature\. We are currently unable to provide support for lookups in other locales\.

**Important**  
CNAM is not supported for custom caller IDs, third\-party numbers, or with the use of whisper flow transfers\.

**Tip**  
If you want each agent to have their own caller ID name while calling out \(such as *Example Corp Billing Dept*\), create a queue for each agent/caller ID name\.

## Caller ID number: Set in the queue or Call phone number block<a name="using-call-number-block"></a>

Only phone numbers that you've [claimed](claim-phone-number.md) or [ported to Amazon Connect](port-phone-number.md) can be used as your caller ID number\.

To use an external phone number as your outbound caller ID number, contact AWS Support to see if it's possible\. You'll need to provide [proof of ownership](phone-number-requirements.md)\.

You can set the caller ID number as follows:
+ **[Call phone number](call-phone-number.md) block**: Use this block in an [Outbound whisper flow](create-contact-flow.md#contact-flow-types) to initiate an outbound call to a customer and, optionally, specify a custom caller ID number that is displayed to call recipients\.

  This block is useful when you have multiple telephone numbers used to make outbound calls, but want to consistently display the same company phone number for the caller ID for calls made from your contact center\. 

  You can also use this block with the [Set contact attributes](set-contact-attributes.md) block to set the callback number dynamically\. For example, you can display a certain caller ID number based on the customer's account type\.
+ **Queue:** If no caller ID number is specified in the [Call phone number](call-phone-number.md) block, then the caller ID in the queue settings is used\.

**Important**  
**In Australia**: The caller ID must be an Amazon Connect provided DID \(Direct Inward Dialing\) phone number\. If a toll free number or a number not provided by Amazon Connect is used in the caller ID, local telephony suppliers may reject outbound calls due to local anti\-fraud requirements\.

## Setting the caller ID dynamically<a name="using-dynamic-caller-id"></a>

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

In the UK and many other countries internationally, local dialing requires the addition of a 0 in front of the subscriber number\. However, to use E\.164 formatting, this 0 must be removed\. A number such as 020 718 xxxxx in the UK would be formatted as \+44 20 718 xxxxx\.

Phone numbers that are not formatted in E\.164 may work, but it depends on the phone or handset that is being used as well as the carrier from which the call is originated\.

When you place calls from the CCP using Amazon Connect the CCP provides the correct formatting for numbers automatically\.

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

## Why your caller ID might not appear correctly to customers<a name="why-callerid-name-might-not-appear-correctly"></a>

Amazon Connect presents Outbound Caller ID Name correctly via the Calling Line/Party Presentation service on outbound calls\. In testing, with all of our telephony providers, the Outbound Caller ID Name value comes back to us intact on all the carriers we use\. This service is not consistent because downstream carriers \(including mobile carriers\) often ignore the value we set in the Outbound Caller ID Name and CNAM is not regulated or enforced\. 

## How to avoid labels like "spam" and "telemarketer"<a name="enroll-in-CNAM-services"></a>

Amazon Connect has contracted with a leading provider of CNAM services for US numbers to provide Calling Name to the extent possible\. This enables outbound calls that show the enrolled Calling Line Identity \(CLI\) to generally avoid reputation\-sensitive labels like "spam" or "telemarketer\."

To enroll your numbers with this CNAM services provider, open an AWS Support ticket\. Our support team will gather the required information to enroll your numbers\. For instructions on how to access AWS Support, see [Get administrative support for Amazon Connect](get-admin-support.md)\.

**Note**  
Only numbers in the 50 US states, Puerto Rico, and Virgin Islands are eligible\.

## Toll\-free numbers for caller ID<a name="tfn-callerid"></a>

Using toll\-free numbers for outbound communications have a number of limitations\. For example, using a toll\-free number to dial other toll\-free numbers in the United States can result in the number being filtered, blocked, or not properly routed to the destination by carriers\. Toll\-free numbers may be terminated at a higher than expected rate\. If you know you need to call toll\-free numbers in the United States you must use DIDs to make the calls to be guaranteed call delivery\.

If you're using toll\-free numbers outside of the US, refer to the [Amazon Connect Telecoms Country Coverage Guide](https://d1v2gagwb6hfe1.cloudfront.net/Amazon_Connect_Telecoms_Coverage.pdf) to see which countries support toll\-free numbers as outbound\. For example, for Australia the guide shows it's not permitted to use toll\-free numbers due to local regulations; the **National Outbound** column indicates that toll\-free numbers are not supported\. 

**Important**  
Toll\-free products are designed to be national products and phoned within the country\. We do not guarantee international reachability of any of these services as access to the numbers is controlled by the caller's network access\. 