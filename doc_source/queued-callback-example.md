# Example: Metrics for a queued callback<a name="queued-callback-example"></a>

This topic shows an example queued callback flow and reviews how the contact records and times are set for it\. 

Assume we have set up the following flows:
+ **Inbound flow** \-\- Runs when the customer calls the customer service number\.
+ **Customer queue flow** – Runs when the customer is waiting in queue\. In this example, we build a flow that offers a callback to the customer\. If the customer selects yes, this flow executes the **Transfer to queue** block to transfer the contact to the callback queue named CallbackQueue, with an initial delay of 99 seconds, and then hangs up\.
+ **Outbound whisper flow** \-\- When a queued callback is placed, the customer hears this after they pick up and before they connect to the agent\. For example, "Hello, this is your scheduled callback\.\.\."
+ **Agent whisper flow** \-\- The agent hears this right after they accept the contact, before they are joined to the customer\. For example, "You are about to be connected to Customer John, who requested a refund for\.\.\."

In this example, John calls customer service\. Here's what happens:

1. Inbound flow creates contact record\-1:

   1. John calls customer service at 11:35\. The Inbound flow runs and puts him in queue at 11:35\. 

   1. The Customer queue flow runs\. At 11:37, John chooses to schedule a callback, so Amazon Connect initiates a callback contact at 11:37, before the inbound contact is disconnected\. 

1. Callback flow creates contact record\-2:

   1. The callback contact was initiated at 11:37\.

   1. Because the initial delay is 99 seconds, the callback contact is placed into CallbackQueue at 11:38:39, after the 99 seconds pass\. Now the callback contact is offered to an available agent\. 

   1. After 21 seconds, an agent available at 11:39:00 and accepts the contact\. The 10\-second agent whisper flow is played to the agent\. 

   1. After the agent whisper flow is complete, Amazon Connect calls John at 11:39:10\. John picks up, and listens to the 15\-second outbound whisper flow\. 

   1. When the outbound whisper flow is complete, John is connected to the agent at 11:39:25\. They talk until 11:45, and then John hangs up\. 

This scenario results in two contact records, which include the following metadata\.


| Contact record\-1 | Data | Notes | 
| --- | --- | --- | 
|  Initiation Method  | Inbound  |   | 
|  Initiation Timestamp  | 11:35  | The inbound contact is initiated in Amazon Connect\.  | 
|  ConnectedToSystem Timestamp  | 11:35  | Because this is an inbound contact, InitiationTimestamp = ConnectedToSystemTimestamp\.  | 
|  Next Contact Id   | points to contact record\-2  |   | 
|  Queue  | InboundQueue  |   | 
|  Enqueued Timestamp  | 11:35  | The inbound contact is put in queue\.  | 
|  Dequeued Timestamp  | 11:37  | Because no agent picked up, this is the same as DisconnectedTimestamp\.  | 
|  ConnectedToAgent Timestamp  | N/A  | John scheduled a callback before any agent could pick up\.  | 
|  Disconnected Timestamp  | 11:37:00  | John was disconnected by flow\.  | 


| contact record\-2 | Data | Notes | 
| --- | --- | --- | 
|  PreviousContactId  | points to contact record\-1  |   | 
|  Initiation Timestamp  | 11:37  | The callback contact is created in Amazon Connect\.  | 
|  Queue  | CallbackQueue  |   | 
|  Enqueued Timestamp  | 11:38:39  | The contact was put into the CallbackQueue, after the 99\-second initial delay completes\.  | 
|  Dequeued Timestamp  | 11:39:00  | After 21 seconds, an agent accepts the contact\.  | 
|  Queue Duration  | 120 seconds  | This is the initial delay \(99 seconds\), plus any additional time sitting in queue waiting for an agent to become available \(21 seconds\)\.  | 
|  ConnectedToSystem Timestamp  | 11:39:10  | John is called after the 10 second agent whisper flow completes\.  | 
|  ConnectedToAgent Timestamp  | 11:39:25  | John and the agent are connected, after the 15 second outbound whisper flow completes\.  | 
|  Disconnected Timestamp  | 11:45  | John hangs up\.  | 