# Set up outbound caller ID<a name="queues-callerid"></a>

We recommend setting your outbound caller ID\. Not doing so may result in some PSTN carriers considering your outbound calls fraudulent activity, and they may drop them\. 

There are a few times when your outbound caller ID—your company name and number—will appear to contacts:
+ During customer callbacks\.
+ If an agent makes an outbound call\.
+ If an agent transfers a call, for example, to an external number\.

There are a few places where you can specify what your outbound caller ID:
+ In a queue\. You can specify both the outbound caller ID name and the phone number\. For instructions, see [Create a queue](create-queue.md)\.
+ In the **Call phone number** block in an outbound whisper contact flow\. You can use this block with the **Set contact attributes** block to set the callback number dynamically\. For example, you can display a certain caller ID number based on the customer's account type\. For more information, see [Initiate an outbound call](using-call-number-block.md)\. 
+ In the **Transfer to phone number** block\. For more information, see [Set up contact transfers](transfer.md)\. 

## Why your caller ID might not appear correctly to customers<a name="why-callerid-name-might-not-appear-correctly"></a>

Amazon Connect presents Outbound Caller ID Name correctly via the Calling Line/Party Presentation service on outbound calls\. In testing, with all of our telephony providers, the Outbound Caller ID Name value comes back to us intact on all the carriers we use\. This service is not consistent because downstream carriers \(including mobile carriers\) often ignore the value we set in the Outbound Caller ID Name and CNAM is not regulated or enforced\. 

## How to avoid labels like "spam" and "telemarketer"<a name="enroll-in-CNAM-services"></a>

Amazon Connect has contracted with a leading provider of CNAM services for US numbers to provide Calling Name to the extent possible\. This enables outbound calls that show the enrolled Calling Line Identity \(CLI\) to generally avoid reputation\-sensitive labels like "spam" or "telemarketer\."

To enroll your numbers with this CNAM services provider, open a Support ticket\. Our Support team will gather the required information to enroll your numbers\. For instructions on how to access Support, see [Get administrative support for Amazon Connect](get-admin-support.md)\.

**Note**  
Only numbers in the 50 US states, Puerto Rico, and Virgin Islands are eligible\.