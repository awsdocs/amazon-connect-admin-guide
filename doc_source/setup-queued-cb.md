# Set up queued callback by creating flows, queues, and routing profiles<a name="setup-queued-cb"></a>

You can create flows that provide the ability for customers to leave their phone number and get a callback from an agent\. 

**Topics**
+ [Steps to set up queued callback](#setup-queued-callback-overview)
+ [The routing process](#cb-routing)
+ [How queued callbacks affect queue limits](#queued-callback-limits)
+ [Create a flow for queued callbacks](#queued-callback-contact-flow)
+ [Learn more about queued callbacks](#queued-callback-no-agents-available)

## Steps to set up queued callback<a name="setup-queued-callback-overview"></a>

Use the steps provided in the following overview to set up queued callback\. 
+ [Set up a queue](create-queue.md) specifically for callbacks\. In your real\-time metrics reports, you can look at that queue and see how many customers are waiting for callbacks\.
+ [Set up caller ID](queues-callerid.md)\. When setting your callback queue, specify the caller ID name and phone number that appears to customers when you call back\. 
+ [Add the callback queue to a routing profile](routing-profiles.md)\. Set this up so that contacts waiting for a call are routed to agents\. 
+ [Create a flow for queued callbacks](#queued-callback-contact-flow)\. You offer the option for a callback to the customer\. 
+ [Associate a phone number with the inbound flow](associate-claimed-ported-phone-number-to-flow.md)\. 
+ \(Optional\) Create an outbound whisper flow\. When a queued call is placed, the customer hears this message after they pick up and before they connect to the agent\. For example, "Hello, this is your scheduled callback\.\.\."
+ \(Optional\) Create an agent whisper flow\. This is what the agent hears right after they accept the contact, before they are joined to the customer\. For example, "You're about to be connected to Customer John, who requested a refund for\.\.\."

## The routing process<a name="cb-routing"></a>

1. When a customer leaves their number it's put in a queue and then routed to the next available agent\.

1. After an agent accepts the callback in the CCP, Amazon Connect calls the customer\.

   If no agents are available to work on callbacks, the callbacks can stay in queue for at least 7 days and up to 14 days after they are created before Amazon Connect automatically removes them\.
**Tip**  
To manually remove a callback from the queue, use the [StopContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StopContact.html) API\.

1. If there is no answer when the Amazon Connect calls the customer, it retries based on the number of times you've specified\. 

1. If the call goes to **voicemail**, it's considered connected\.

1. If the customer calls again while in the callback queue, it's treated as a new call and will be handled as usual\. To avoid duplicate callback requests in a callback queue, see this blog: [Preventing duplicate callback requests in Amazon Connect](http://aws.amazon.com/blogs/contact-center/preventing-duplicate-callback-requests-in-amazon-connect/)\. 

## How queued callbacks affect queue limits<a name="queued-callback-limits"></a>
+ Queued callbacks count towards the queue size limit, but they are routed to the error branch\. For example, if you have a queue that handles callbacks and incoming calls, and that queue reaches the size limit:
  + The next callback is routed to the error branch\.
  + The next incoming call gets a reorder tone \(also known as a fast busy tone\), which indicates no transmission path to the called number is available\.
+ Consider setting up your queued callbacks to be lower priority than your queue for incoming calls\. This way, your agents only work on queued callbacks when the incoming call volume is low\.

## Create a flow for queued callbacks<a name="queued-callback-contact-flow"></a>

To see what a flow looks like with queued callback, in new Amazon Connect instances see [Sample queue configurations](sample-queue-configurations.md)\. In previous instances, see [Sample queued callback](sample-queued-callback.md)\.

The following procedure shows how to:
+ Request a callback number from a customer\.
+ Store the callback number in an attribute\.
+ Reference the attribute in a **Set callback number** block to set the number to dial the customer\.
+ Transfer the customer to the callback queue\.

At the basic level, here's what this queued callback flow looks like, without any of the alternative branches or error handling configured\. The following image shows a flow with the following blocks: **Get customer input**, **Store customer input**, **Set callback number**, **Play prompt**, **Transfer to queue**, and **Disconnect/hang up**\.

![\[A queued callback flow in the flow designer.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/queued-callback-flow.png)

Following are the steps to create this flow\.

**To create a flow for queued callbacks**

1. In Amazon Connect, choose **Routing**, **Contact flows**\.

1. Select an existing flow, or choose **Create contact flow** to create a new one\.
**Tip**  
You can create this flow using different flow types: Customer queue flow, Transfer to agent, Transfer to queue\. 

1. Add a [Get customer input](get-customer-input.md) block\.

1. Configure the block to prompt the customer for a callback\. The following image shows a message in the **Text\-to\-speech** box: **Press 1 to receive a callback\. Press 2 to stay in queue**\.   
![\[The properties page of the Get customer input block, configured for text-to-speech or chat text.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/get-customer-input-callback.png)

1. At the bottom of the block, choose **Add another condition**, and add options 1 and 2, as shown in the following image\.   
![\[Option 1 and option 2.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/options-1-and-2.png)

1. Add a [Store customer input](store-customer-input.md) block\.

1. Configure the block to prompt customers for their callback number, such as "Please enter your phone number\." The following image shows the **Properties** page of the **Store customer input **block\.  
![\[The text to speech box, contains the message Please enter your phone number.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/store-customer-input.png)

1. In the **Customer input** section, select **Phone number**, and then choose one of the following: 
   + **Local format**: Your customers are calling from phone numbers that are in the same country as the AWS Region where you created your Amazon Connect instance\.
   + **International format/Enforce E\.164**: Your customers are calling from phone numbers in countries or regions other than the one where you created your instance\.

1. Add a [Set callback number](set-callback-number.md) block to your flow\.

1. Configure the block to set **Type** to **System**, as shown in the following image\. For **Attribute**, choose **Store customer input**\. This attribute stores the customer's phone number\.  
![\[The Properties page of the set callback number block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-callback-number2.png)

1. Add a [Transfer to queue](transfer-to-queue.md) block\. 

1. In the **Transfer to queue** block, configure the **Transfer to callback queue** tab as shown in the following image\. Set **Initial delay** to 99\. Set **Max number of retries** to 2\. Set **Minimum time between attempts** to 10 minutes\.   
![\[The transfer to callback queue tab on the Properties page of the Transfer to queue block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/transfer-to-callback-queue-tab.png)

   The following properties are available:
   + **Initial delay**: Specify how much time has to pass between a callback contact being initiated in the flow, and the customer is put in queue for the next available agent\. In the previous example, the time is 99 seconds\.
   + **Maximum number of retries**: If this is set to 2, then Amazon Connect tries to call back the customer a maximum of three times: the initial callback, and two retries\. 

     A retry only happens if it rings but there's no answer\. If the callback goes to voicemail, it's considered connected and Amazon Connect does not retry again\.
**Tip**  
We strongly recommend that you double\-check the number entered in **Maximum number of retries**\. If you accidentally enter a high number, such as 20, it's going to result in unnecessary work for the agent and too many calls for the customer\.
   + **Minimum time between attempts**: If the customer doesn't answer the phone, this is how long to wait until trying again\. In the previous example, we wait 10 minutes between attempts\.

1. In the **Optional parameters** section, choose **Set working queue** if you want to transfer the contact to a queue that you set up specifically for callbacks\. This option is shown in the following image\.  
![\[The optional parameters, set a queue set to callback queue.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/transfer-to-callback-queue-tab-set-working-queue.png)

   Creating a queue just for callbacks lets you view in your real\-time metrics reports how many customers are waiting for callbacks\.

   If you don't set a working queue, Amazon Connect uses the queue that was set previously in the flow\.

1. To save and test this flow, configure the other branches and add error handling\. To see an example of how this is done, see [Sample queue configurations](sample-queue-configurations.md)\. For previous instances, see [Sample queued callback](sample-queued-callback.md)\. 

1. For information about how callbacks appear in real\-time metrics reports and contact records, see [About queued callbacks in metrics](about-queued-callbacks.md)\. 

## Learn more about queued callbacks<a name="queued-callback-no-agents-available"></a>

See the following topics to learn more about queued callbacks:
+ [About queued callbacks in metrics](about-queued-callbacks.md)
+ [How Initial delay affects Scheduled and In queue metrics](scheduled-vs-inqueue.md)
+ [What counts as a "Failed Callback Attempt"](failed-callback-attempt.md)
+ [Example: Metrics for a queued callback](queued-callback-example.md)