# Contact block definitions<a name="contact-block-definitions"></a>

You create contact flows in the contact flow designer using contact blocks\. Drag and drop contact blocks onto a canvas to arrange a contact flow\. 

The following table lists all available contact blocks that you can use\. Choose the links in the Block column for more information\. 


| Block | Description | 
| --- | --- | 
| [Track events in contact flowsStorage for contact flow logsCall phone number](call-phone-number.md)  | Initiates an outbound call from an outbound whisper flow\. | 
|  [Change routing priority / age](change-routing-priority.md)   |  Changes the priority of the contact in queue\. You may want to do this, for example, based on the contact's issue or other variable\.  | 
|  [Check contact attributes](check-contact-attributes.md)   |  Checks the values of contact attributes\.  | 
|   [Check hours of operation](check-hours-of-operation.md)  |  Checks whether the contact is occurring within or outside of the hours of operation defined for the queue\.  | 
|   [Check queue status](check-queue-status.md)   |  Checks the status of the queue based on specified conditions\.  | 
|   [Check staffing](check-staffing.md)   |  Checks the current working queue, or queue you specify in the block, for whether agents are available, staffed, or online\. Staffed availability could be on call, or after contact work status\.  | 
|  [Disconnect / hang up](disconnect-hang-up.md)  |  Terminates a customer contact\.  | 
|   [Distribute by percentage](distribute-by-percentage.md)   |  Routes customers randomly based on a percentage\.  | 
|   [End flow / Resume](end-flow-resume.md)   |  Ends the current flow without disconnecting the contact\.  | 
|   [Get customer input](get-customer-input.md)   |  Branches based on customer intent\.  | 
| [Get queue metrics](get-queue-metrics.md) | Retrieves real\-time metrics about queues and agents in your contact center and returns them as attributes\. | 
|  [Hold customer or agent](hold-customer-agent.md)  |  Places a customer or agent on or off hold\.  | 
|  [Invoke AWS Lambda function](invoke-lambda-function-block.md)  |  Calls AWS Lambda, optionally returns key\-value pairs\.  | 
|  [Loop](loop.md)  |  Loops through, or repeats, the **Looping** branch for the number of loops specified\.  | 
|  [Loop prompts](loop-prompts.md)  |  Loops a sequence of prompts while a customer or agent is on hold or in queue\.   | 
|   [Play prompt](play.md)  |  Plays an interruptible audio prompt, delivers a text\-to\-speech message, or delivers a chat response\.  | 
|   [Set callback number](set-callback-number.md)   |  Sets a callback number\.  | 
|   [Set contact attributes](set-contact-attributes.md)   |  Stores key\-value pairs as contact attributes\.  | 
|  [Set customer queue flow](set-customer-queue-flow.md)  |  Specifies the flow to invoke when a customer is transferred to a queue\.  | 
|   [Set disconnect flow](set-disconnect-flow.md)   |  Sets the flow to run when the agent disconnects from the chat\.  | 
|   [Set hold flow](set-hold-flow.md)   |  Links from one contact flow type to another\.  | 
|   [Set recording and analytics behavior ](set-recording-behavior.md)  |  Sets options for recording conversations\.  | 
|  [Set voice](set-voice.md)   |  Sets the text\-to\-speech \(TTS\) language and voice to be used in the contact flow\.  | 
|   [Set whisper flow](set-whisper-flow.md)  |  Overrides the default whisper by linking to a whisper flow\.  | 
|   [Set working queue](set-working-queue.md)   |  Specifies the queue to be used when **Transfer to queue** is invoked\.  | 
|  [Start media streaming](start-media-streaming.md)  | Starts capturing customer audio for a contact\. | 
|  [Stop media streaming](stop-media-streaming.md)  | Stops capturing customer audio after it is started with a **Start media streaming** block\. | 
|   [Store customer input](store-customer-input.md)   |  Stores numerical input to a contact attribute\.  | 
|   [Transfer to agent](transfer-to-agent-block.md)  |  Transfers the customer to an agent\.  | 
|   [Transfer to flow](transfer-to-flow.md)  |  Transfers the customer to another contact flow\.  | 
|   [Transfer to phone number](transfer-to-phone-number.md)  |  Transfers the customer to a phone number external to your instance\.  | 
|   [Transfer to queue](transfer-to-queue.md)   |  In most contact flows, this block ends the current contact flow and places the customer in queue\. When used in a customer queue flow, this block transfers a contact already in a queue to another queue\.  | 
|   [Wait](wait.md)  |  Pauses the contact flow\.  | 