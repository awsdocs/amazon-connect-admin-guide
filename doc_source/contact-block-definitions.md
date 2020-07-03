# Contact Block Definitions<a name="contact-block-definitions"></a>

You create contact flows in the contact flow designer using contact blocks\. Drag and drop contact blocks onto a canvas to arrange a contact flow\. 

The following table lists all available contact blocks that you can use\. Choose the links in the Block column for more information\. 


| Block | Description | 
| --- | --- | 
| [Track events in contact flowsStorage for contact flow logsCall Phone Number](call-phone-number.md)  | Initiates an outbound call from an outbound whisper flow\. | 
|  [Change Routing Priority / Age](change-routing-priority.md)   |  Changes the priority of the contact in queue\. You may want to do this, for example, based on the contact's issue or other variable\.  | 
|  [Check Contact Attributes](check-contact-attributes.md)   |  Checks the values of contact attributes\.  | 
|   [Check Hours of Operation](check-hours-of-operation.md)  |  Checks whether the contact is occurring within or outside of the hours of operation defined for the queue\.  | 
|   [Check Queue Status](check-queue-status.md)   |  Checks the status of the queue based on specified conditions\.  | 
|   [Check Staffing](check-staffing.md)   |  Checks the current working queue, or queue you specify in the block, for whether agents are available, staffed, or online\. Staffed availability could be on call, or after contact work status\.  | 
|  [Disconnect / Hang Up](disconnect-hang-up.md)  |  Terminates a customer contact\.  | 
|   [Distribute by Percentage](distribute-by-percentage.md)   |  Routes customers randomly based on a percentage\.  | 
|   [End Flow / Resume](end-flow-resume.md)   |  Ends the current flow without disconnecting the contact\.  | 
|   [Get Customer Input](get-customer-input.md)   |  Branches based on customer intent\.  | 
| [Get Queue Metrics](get-queue-metrics.md) | Retrieves real\-time metrics about queues and agents in your contact center and returns them as attributes\. | 
|  [Hold Customer or Agent](hold-customer-agent.md)  |  Places a customer or agent on or off hold\.  | 
|  [Invoke AWS Lambda Function](invoke-lambda-function-block.md)  |  Calls AWS Lambda, optionally returns key\-value pairs\.  | 
|  [Loop](loop.md)  |  Loops through, or repeats, the **Looping** branch for the number of loops specified\.  | 
|  [Loop Prompts](loop-prompts.md)  |  Loops a sequence of prompts while a customer or agent is on hold or in queue\.   | 
|   [Play Prompt](play.md)  |  Plays an interruptible audio prompt, delivers a text\-to\-speech message, or delivers a chat response\.  | 
|   [Set Callback Number](set-callback-number.md)   |  Sets a callback number\.  | 
|   [Set Contact Attributes](set-contact-attributes.md)   |  Stores key\-value pairs as contact attributes\.  | 
|  [Set Customer Queue Flow](set-customer-queue-flow.md)  |  Specifies the flow to invoke when a customer is transferred to a queue\.  | 
|   [Set Disconnect Flow](set-disconnect-flow.md)   |  Sets the flow to run when the agent disconnects from the chat\.  | 
|   [Set Hold Flow](set-hold-flow.md)   |  Links from one contact flow type to another\.  | 
|   [Set Recording Behavior](set-recording-behavior.md)  |  Sets options for recording conversations\.  | 
|  [Set Voice](set-voice.md)   |  Sets the text\-to\-speech \(TTS\) language and voice to be used in the contact flow\.  | 
|   [Set Whisper Flow](set-whisper-flow.md)  |  Overrides the default whisper by linking to a whisper flow\.  | 
|   [Set Working Queue](set-working-queue.md)   |  Specifies the queue to be used when **Transfer to queue** is invoked\.  | 
|  [Start Media Streaming](start-media-streaming.md)  | Starts capturing customer audio for a contact\. | 
|  [Stop Media Streaming](stop-media-streaming.md)  | Stops capturing customer audio after it is started with a **Start media streaming** block\. | 
|   [Store Customer Input](store-customer-input.md)   |  Stores numerical input to a contact attribute\.  | 
|   [Transfer to Agent](transfer-to-agent-block.md)  |  Transfers the customer to an agent\.  | 
|   [Transfer to Flow](transfer-to-flow.md)  |  Transfers the customer to another contact flow\.  | 
|   [Transfer to Phone Number](transfer-to-phone-number.md)  |  Transfers the customer to a phone number external to your instance\.  | 
|   [Transfer to Queue](transfer-to-queue.md)   |  In most contact flows, this block ends the current contact flow and places the customer in queue\. When used in a customer queue flow, this block transfers a contact already in a queue to another queue\.  | 
|   [Wait](wait.md)  |  Pauses the contact flow\.  | 