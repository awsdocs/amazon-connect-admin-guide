# Set Up Outbound Caller ID<a name="queues-callerid"></a>

There are a few times when your outbound caller ID—your company name and number—will appear to contacts:
+ During customer callbacks\.
+ If an agent makes an outbound call\.
+ If an agent transfers a call, for example, to an external number\.

There are a few places where you can specify what your outbound caller ID will be:
+ In a queue\. You can specify both the outbound caller ID name and the phone number\. For instructions, see [Create a Queue](create-queue.md)\.
+ In the **Call phone number** block in an outbound whisper contact flow\. You can use this block with the **Set contact attributes** block to set the callback number dynamically\. For example, you can display a certain caller ID number based on the customer's account type\. For more information, see [Initiate an Outbound Call](using-call-number-block.md)\. 
+ In the **Transfer to phone number** block\. For more information, see [Set Up Contact Transfers](transfer.md)\. 

## Why Your Caller ID Might Not Appear Correctly to Customers<a name="why-callerid-name-might-not-appear-correctly"></a>

Amazon Connect presents Outbound Caller ID Name correctly via the Calling Line/Party Presentation service on outbound calls\. In testing, with all of our telephony providers, the Outbound Caller ID Name value comes back to us intact on all the carriers we use\. This service is not consistent because downstream carriers \(including mobile carriers\) often ignore the value we set in the Outbound Caller ID Name and CNAM is not regulated or enforced\. 

To have this work more consistently, in the US, telephony providers will likely require registering your name with CNAM databases, such as Neustar, \(formerly Targus\), VeriSign, or Syniverse\. Amazon Connect does not support CNAM registration directly\. We are considering adding CNAM registration as a feature of Amazon Connect in the future\.  

While we can't speak for a specific provider, Neustar has historically been used by companies such as Verizon, CenturyLink, Fairpoint, Frontier, Windstream, Comcast, Cox, and others\. You can and may want to register with multiple CNAM databases\. Even so, CNAM registration is not a guarantee since not all carriers do a CNAM look up, and some charge you for it\.