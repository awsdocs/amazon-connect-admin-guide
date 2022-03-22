# Sample queue configurations<a name="sample-queue-configurations"></a>

**Note**  
This topic explains a sample contact flow that is included with Amazon Connect\. For information about locating the sample flows in your instance, see [Sample contact flows](contact-flow-samples.md)\. 

Type: Contact flow \(inbound\)

This contact flow shows different ways you can put a customer in queue: you can change the priority of the customer, determine the wait time in queue, and give them an option for a callback\. Here's how it works: 

1. The customer is put in the BasicQueue\.

1. After that, the **Default customer queue** flow is invoked\. This block runs a **Loop prompts** block that plays the following: 

   *Thank you for calling\. Your call is very important to us and will be answered in the order it was received\.*

1. The hours of operation are checked with a **Check hours of operation** block\.

1. The channel is checked with a **Check contact attributes** block:
   + If chat, we check the time in queue\. If it's less than 5 minutes, the customer is placed in queue for an agent\. If it's more, we check the channel again and if it's chat, put the customer in queue for an agent\. 
   + If voice, the customer is routed down the **No Match** branch, to a **Play prompt** block and then to a **Get customer input** block\. 

     In the **Get customer input** block, we give the customer the option to press 1 to move to the front of the queue or 2 to move to the end of the queue\. 

     The two **Change routing priority / age** blocks move the customer to the front or back of the queue\.

     You can see this path in the following image:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/sample-queue-configurations-priority.png)

1. Next we use a **Check queue status** block to check whether the time in queue is less than 300 seconds\. 

1. We use a **Play prompt** block to tell the customer the results\. 

1. We use a **Check contact attributes** block again to check the customer's channel: chat or voice/No Match\. 

These next steps apply to customers who were routed down the voice/**No Match** branch, as shown in the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/sample-queue-configurations.png)

1. In the **Get customer input** block, we prompt customers to *Press 1 to go into queue or 2 to enter a callback number\.* 

1. If customers press 2, they are routed down the **Pressed 2** branch to the **Store customer input** block\.

1. The **Store customer input** block prompts the customer for their phone number\.

1. The customer's phone number is stored in the **Stored customer input attribute**, by the **Set callback number** block\.

1. We use a **[Transfer to queue](transfer-to-queue.md)** block to put the customer in a callback queue\. 

1. The **[Transfer to queue](transfer-to-queue.md)** block is configured so Amazon Connect waits 5 seconds between the time the callback contact is initiated and the contact is enqueued, where it sits until it is offered to an available agent\. 

   If the initial callback doesn't reach the customer, Amazon Connect will attempt 1 callback\. If it were configured for 2 attempted callbacks, it would wait 10 minutes between each one\. 

   Also, no special callback queue is specified\. Rather, customers are in the BasicQueue, which was set at the beginning of the flow\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/sample-queue-configurations-transfer-to-queue-block.png)

For information about queued callbacks, see the following topics:
+ [Set up queued callback](setup-queued-callback.md) 
+ [Contact block: Transfer to queue](transfer-to-queue.md) 
+ [About queued callbacks in metrics](about-queued-callbacks.md) 