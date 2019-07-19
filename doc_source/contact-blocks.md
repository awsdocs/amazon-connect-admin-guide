# Contact Block Definitions<a name="contact-blocks"></a>

Contact flows are created in the contact flow designer using action blocks, which you arrange by dragging and dropping them onto a canvas\. The contact flow configuration is grouped into blocks\. Each group represents a specific action, and each block has editable conditions related to the group’s action or behavior\.

**Note**  
When you set **User Defined** or **External** values in dynamic attribute fields, ensure that you use only alphanumeric characters \(A\-Z, 0–9\) and periods\. No other characters can be used\.

## Interact<a name="contact-interact"></a>


| Block | Action | Description | 
| --- | --- | --- | 
|  **Play prompt**  |  Plays a stored audio file, or delivers a Text\-to\-speech message\.  |  Prompts can be an audio file, stored in the prompt library, or text\-to\-speech, which can optionally be specified in a flow using a contact attribute\. If you use text\-to\-speech, you can use a maximum of 3,000 billed characters \(6,000 total characters\)\.  | 
|  **Get customer input**  |  Branches based on customer intent\.  |  Plays an interruptible audio prompt and branches based on DTMF or Amazon Lex intents\. If you use text\-to\-speech, you can use a maximum of 3,000 billed characters \(6,000 total characters\)\. Amazon Lex bots support both spoken utterances and keypad input when used in a contact flow\.  | 
|  **Store customer input**  |  Stores numerical input to contact attribute\.  |  Plays an interruptible audio prompt and stores digits via DTMF as a contact attribute\. To enable encryption, contact your system administrator to add a public signing key to the **Contact flow security keys** settings of your Amazon Connect instance\.  | 
|  **Loop prompts**  |  Loops a sequence of prompts while a customer or agent is on hold or in queue\.  |  When **Loop prompts** is used in a queue flow, audio playback can be interrupted with a flow at preset times\.  | 
|  **Hold customer or agent**  |  Places a customer or agent on or off hold\.  |  Settings: Agent on hold / customer on call Customer on hold / agent on call Agent and customer on call  | 
| **Call phone number** | Initiates an outbound call from an outbound whisper flow\. | Use the **Call phone number** block to place an outbound call\. This block is supported only in outbound whisper flows\. You can optionally set the phone number displayed as the caller ID number to a number from your instance, or to a number using an attribute\. The number must be in E\.164 format\. | 
| **Start media streaming** | Starts capturing customer audio for a contact\. | Captures customer audio during a contact\. You must enable Live media streaming to successfully capture customer audio\. Media streaming continues until a **Stop media streaming** block is used or the contact ends\. To learn more, see [Capture Customer Audio: Live Media Streaming](customer-voice-streams.md)\. | 
| **Stop media streaming** | Stops capturing customer audio after it is started with a **Start media streaming** block\. | Once started, media streaming continues, even when one contact flow transfer to another contact flow\. You must use a **Stop media streaming** block to stop media streaming\. | 

## Set<a name="contact-set"></a>


| Block | Action | Description | 
| --- | --- | --- | 
|  **Set working queue**  |  Specifies the queue to be used when **Transfer to queue** is invoked\.  |  A queue must be specified before invoking **Transfer to queue** except when used in a customer queue flow\. It’s also the default queue for checking attributes, such as staffing, queue status, and hours of operation\. To use a **Set working queue** block to set the queue dynamically, such as with contact attributes, you must specify the ARN for the queue rather than the queue name\. To find the ARN for a queue, open the queue in the queue editor\. The ARN is included as the last part of the URL displayed in the browser address bar after /queue\. For example, `.../queue/aaaaaaaa-bbbb-cccc-dddd-111111111111`\.   | 
|  **Set call recording behavior**  |  Sets options for recording conversations\.  |  Enables or disables recording of the agent, customer, or both\.  | 
|  **Set contact attributes**  |  Stores key\-value pairs as contact attributes\.  |  Contact attributes are accessible by other areas of Amazon Connect, such as the CTRs\.  | 
| Get queue metrics | Retrieves real\-time metrics about queues and agents in your contact center and returns them as attributes\. | Use a Check contact attributes block to check metric values and define routing logic based on them, such as number of contact in a queue, number of available agents, and oldest contact in a queue\. For more information, see [Using System Metric Attributes](connect-contact-attributes.md#attrib-system-metrics)\. | 
|  **Change routing priority / age**  |  Alters the priority of the contact in queue\.  |  Routing age alters the time in queue for the contact, which determines its priority in comparison to when other contacts are received\. Queue priority sets the contact to a high priority that can be compared to other contacts that have a priority set \(typically between 1 and 1000\)\.  | 
|  **Set hold flow**  |  Links from one contact flow type to another\.  |  Specifies the flow to invoke when a customer or agent is put on hold\.  | 
|  **Set whisper flow**  |  Overrides the default whisper by linking to a whisper flow\.  |  Specifies the whisper to be played to customer on an outbound call, or to the customer or agent when the call is joined\.  | 
|  **Set callback number**  |  Sets a callback number\.  |  Specifies the number to be used to call the customer back in the CCP, or when **Transfer to queue** is invoked with the callback option\. When specifying a phone number in Amazon Connect, the number must be in [E\.164 format](https://en.wikipedia.org/wiki/E.164)\. Numbers in E\.164 format do not include the leading zeroes you would dial for a local or regional call within the same country when dialing the number from a phone\. For example, if you usually dial 0400xxxxxx to place a call in Australia, the number in E\.164 format includes the country code of 61 and removes the leading zero for the number\. The number to use in Amazon Connect is **\+61400xxxxxx**\.  | 
|  **Set voice**  |  Sets the voice\.  |  Sets the voice to interact with the customer, and optionally the voice if using text\-to\-speech \(TTS\)\.  | 
|  **Set customer queue flow**  |  Set queue flow\.  |  Specifies the flow to invoke when a customer is transferred to a queue\.  | 

## Branch<a name="contact-branch"></a>


| Block | Action | Description | 
| --- | --- | --- | 
|  **Check queue status**  |  Checks the status of the queue based on specified conditions\.  |  Branches based on the comparison of **Time in Queue** or **Queue capacity**\. If no match is found, the **No Match** branch is followed\.  | 
|  **Check staffing**  |  Checks the current working queue, or queue you specify in the block, for whether agents are available, staffed \(on call, or after call work status\), or online\.  |  Branches based on whether agents are available, staffed \(available, on call, and after call work\), or online\.  You must set a queue before using a **Check staffing** block in your contact flow\. If a queue is not set, the block always proceeds through the error branch\. You can use a **Set working queue** block to set the queue\. When a contact is transferred from one flow to another, the queue that is set in a contact flow is passed from that flow to the next flow\.   | 
|  **Check hours of operation**  |  Checks to see whether the contact is occurring within or outside of the hours of operation defined for the queue\.  |  Branches based on specified hours of operation, either directly or as associated to a queue that is within open hours\.  Queues that are automatically created for each user in your instance do not include an Hours of operation\. If you use the block to check the Hours of operation for one of these queues, the check fails and the **Error** branch is followed\.   | 
|  **Check contact attributes**  |  Check the values of contact attributes\.  |  Branches based on a comparison to the value of a contact attribute\. Supported comparisons include: **Equals**, **Is Greater Than**, **Is Less Than**, **Starts With**, **Contains**\.  | 
|  **Distribute by percentage**  |  Routes customers randomly based on a percentage\.  |  Like flipping a coin, contacts are distributed randomly, which doesn’t guarantee exact percentage splits\.  | 
|  **Loop**  |   Loops through \(repeats\) the **Looping** branch for the number of loops specified\.  |   After the loops are completed, the **Complete** branch is followed\. If you enter 0 for the loop count, the **Complete** branch is followed the first time this block executes\.An example use of this block is to loop back to a **Get customer input** block to try to enter input, such as an account number, when an initial attempt does not succeed\.  | 

## Integrate<a name="contact-integrate"></a>


| Block | Action | Description | 
| --- | --- | --- | 
|  **Invoke AWS Lambda function**  |  Makes a call to AWS Lambda, and optionally returns key\-value pairs\.  |  The returned key\-value pairs can be used to set contact attributes\. To use an AWS Lambda function in a contact flow, first add the function to your instance\. For more information, see [Add an AWS Lambda function to your instance](https://docs.aws.amazon.com/connect/latest/adminguide/amazon-connect-instance.html#aws-lambda)\. After you add the function to your instance, you can select the function from the **Select a function** drop\-down list in the block to use it in the contact flow\.  | 

## Terminate / Transfer<a name="contact-terminate"></a>


| Block | Action | Description | 
| --- | --- | --- | 
|  **Disconnect / hang up**  |  Terminates a customer contact\.  |  Disconnects the customer’s call\.  | 
|  **Transfer to queue**  |  In most contact flows, this block ends the current contact flow and places the customer in queue\. When used in a customer queue flow, this block transfers a contact already in a queue to another queue\.  |  When used in most contact flows, a queue must be specified, using **Set working queue**, before invoking **Transfer to queue** except when used in a customer queue flow\. Optionally, the contact can be placed in queue to receive a callback, if a **Set customer callback number** block is used before this block in a flow\. When used in a customer queue flow, a **Loop prompts** block must be used prior to this block in the contact flow\.  | 
|  **Transfer to phone number**  |  Transfers the customer to a phone number external to your instance\.  |  Transfers the contact to the specified phone number\. You can choose to end the contact flow when the call is transferred, or choose to **Resume contact flow after disconnect**, which returns the caller to your instance and resume the contact flow after the transferred call ends\. If the country you want to select is not listed, you can submit a request to add countries you want to transfer calls to using the [Amazon Connect service limits increase form](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-connect)\.  | 
|  **Transfer to agent**  |  Transfers the customer to an agent\.  |  Ends the current contact flow and transfers the customer to an agent\. If the agent is on a call, the contact is disconnected\.  | 
|  **Transfer to flow**  |  Transfers the customer to another contact flow\.  |  Ends the current contact flow and transfers the customer to a different contact flow\. Available in transfer to agent and transfer to queue flows\.  | 
|  **End flow / Resume**  |  Ends the current flow without disconnecting the contact\.  |  This can be used to return to a Loop prompts block when it has been interrupted\. When **End flow / Resume** is invoked, the customer remains connected to the system\.  | 