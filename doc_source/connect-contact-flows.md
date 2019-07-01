# Amazon Connect Contact Flows<a name="connect-contact-flows"></a>

A *contact flow* defines the customer experience with a contact center from start to finish\. You can configure your contact flows using the AWS Management Console\. You can use the contact flow templates provided or create your own contact flows from scratch\.

**Topics**
+ [Contact Flow Templates](#contact-flow-templates)
+ [Add Security Keys](#contact-flow-keys)
+ [Create a Contact Flow](#create-contact-flow)
+ [Create Prompts](#prompts)
+ [Add Text\-to\-Speech](#text-to-speech)
+ [Create Quick Connects](#quick-connects)
+ [Add an Amazon Lex Bot](#amazon-lex)
+ [Resume a Contact Flow After Transfer](#contact-flow-resume)
+ [Initiate an Outbound Call](#using-call-number-block)
+ [Manage Calls in a Queue](#queue-to-queue-transfer)
+ [Transfer Calls Directly to a Specific Agent](#transfer-to-agent)
+ [Contact Block Definitions](contact-blocks.md)
+ [Lambda Functions](connect-lambda-functions.md)
+ [Live Media Streaming](customer-voice-streams.md)
+ [Contact Attributes](connect-contact-attributes.md)
+ [Contact Flow Import/Export](contact-flow-import-export.md)

## Contact Flow Templates<a name="contact-flow-templates"></a>

The following contact flow templates are available:
+ **Customer queue flow**—Manages what the customer experiences while in queue, before being joined to an agent\. Customer queue flows are interruptible and can include actions such as an audio clip apologizing for a delay and offering an option to receive a callback, leveraging the **Transfer to queue** block\.
+ **Customer hold flow**—Manages what the customer experiences while the customer is on hold\. With this flow, one or more audio prompts can be played to a customer using the **Loop prompts** block while waiting on hold\.
+ **Customer whisper flow**—Manages what the customer experiences as part of an inbound call immediately before being joined with an agent\. The agent and customer whispers are played to completion, then the two are joined\.
+ **Outbound whisper flow**—Manages what the customer experiences as part of an outbound call before being connected with an agent\. In this flow, the customer whisper is played to completion, then the two are joined\. For example, this flow can be used to enable call recordings for outbound calls with the **Set call recording behavior** block\.
+ **Agent hold flow**—Manages what the agent experiences when on hold with a customer\. With this flow, one or more audio prompts can be played to an agent using the **Loop prompts** block while the customer is on hold\.
+ **Agent whisper flow**—Manages what the agent experiences as part of an inbound call immediately before being joined with a customer\. The agent and customer whispers are played to completion, then the two are joined\.
+ **Transfer to agent flow**—Manages what the agent experiences when transferring to another agent\. This type of flow is associated with transfer to agent quick connects, and often plays messaging, then completes the transfer using the **Transfer to agent** block\.
+ **Transfer to queue flow**—Manages what the agent experiences when transferring to another queue\. This type of flow is associated with transfer to queue quick connects, and often plays messaging, then completes the transfer using the **Transfer to queue** block\.

## Add Security Keys<a name="contact-flow-keys"></a>

Amazon Connect can encrypt sensitive data collected by contact flows using public\-key cryptography\. Provide an X\.509 certificate within your contact flow to encrypt data captured using the stored customer input system attribute\. You must upload a signing key in `.pem` format in order to use this feature\. The signing key is used to verify the signature of the certificate used within the contact flow\.

**Note**  
You can have up to two signing keys active at one time to facilitate rotation\.

Data that is encrypted within a contact flow is made available through the stored customer input system attribute\. The AWS Encryption SDK can be used to decrypt this data within your system\. For more information, see the [AWS Encryption SDK Developer Guide](https://docs.aws.amazon.com/encryption-sdk/latest/developer-guide/)\.

**To add a security key**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. Choose the name of the instance from the **Instance Alias** column\.

1. In the navigation pane, choose **Contact flows**\.

1. Choose **Add key**\.

1. Paste the contents of your public key in **Public key contents** and choose **Add**\.

## Create a Contact Flow<a name="create-contact-flow"></a>

You can create a variety of contact flows in Amazon Connect, such as transfer flows\. The starting point for all contact flows is the contact flow designer\. You can make your contact flows as simple or complex as needed\.

**To create a contact flow using the contact flow designer**

1. In the navigation pane, choose **Routing**, **Contact flows**\.

1. Choose **Create contact flow**\.

1. Type a name and a description for your contact flow\.

1. Search for a block using the **Search** bar, or expand the relevant group to locate the block\. For more information, see [Contact Block Definitions](contact-blocks.md)\.

1. Drag and drop blocks onto the canvas\. You can add blocks in any order or sequence, as connections between elements aren't required to be strictly linear\.

1. Select the block title to access the settings and editing menu\.

**To create connections between blocks**

1. Select the originating group\.

1. Select the circle for the action to perform\.

1. Drag the arrow to the connector of the group that performs the next action\. For groups that support multiple branches, drag the connector to the appropriate action\.

1. Repeat the steps to create a contact flow that meets your requirements\.

1. Choose **Save** to save a draft of the flow\. Choose **Publish** to activate the flow immediately\.
**Note**  
All connectors must be connected to a block in order to successfully publish your contact flow\.

**To generate logs for your contact flows**  
After your contact flow is published live, you can use contact flow logs to help analyze contact flows and quickly find errors your customers encounter\. If needed, you can roll back to a previous version of the contact flow\. 

For more information about enabling and using contact flow logs, see [Contact Flow Logs](contact-flow-logs.md)\. <a name="rollback"></a>

**To roll back a contact flow**

1. In the contact flow designer, open the contact flow you want to roll back\.

1. Use the dropdown to choose the version of the contact flow you want to roll back to\. If you choose **Latest**, it reverts the flow to the most recent published version\. If there isn't a published version, it reverts to the most recent saved version\. 
**Note**  
To see a consolidated view of all changes across all flows, click the **View historical changes** link at the bottom of the Contact flows page\. You can filter to a specific flow by date or user name\.

1. Choose **Publish** to push that version into production\. 

## Create Prompts<a name="prompts"></a>

Prompts are audio files played in call flows\. Only 8 KHz \.wav files that are less than 50 MB are supported for prompts\. You can upload a pre\-recorded \.wav file to use for your prompt, or record one in the web application\. Prompts and routing policies should be aligned with each other to ensure a smooth call flow for customers\.

**To create a prompt**

1. Choose **Routing**, **Prompts**\.

1. On the **Manage voice prompts** screen, choose **\+Create new prompt**\.

1. You can choose the following actions:
   + **Upload**—Choose the file to upload\.
   + **Record**—Choose the red circle to begin recording\. Use the red square to stop\. You can choose **Crop** to cut the recorded prompt or **Discard** to record a new prompt\.

1. For **Step 2: Input basic information**, enter the name of the file, and then choose **Create**\.

**To manage recorded prompts**

1. Choose **Routing**, **Prompts**\.

1. On the **Manage voice prompts** screen, select the appropriate prompt\.

1. You can choose **Play**, **Download**, **Edit**, or **Delete**\.

1. Choose **Save**\.

## Add Text\-to\-Speech<a name="text-to-speech"></a>

Amazon Connect supports text\-to\-speech, including SSML or plaintext with \(or without\) dynamic attributes\. You can enter text\-to\-speech prompts in any of the contact flow blocks that support prompt entry, such as **Play prompt** and **Get customer input**\. The text\-to\-speech voice is selected in the **Set voice** contact block\. You can also use SSML in Amazon Lex bots to modify the voice used by a chat bot when interacting with your customers\. For more information about using SSML in Amazon Lex bots, see [Managing Messages](https://docs.aws.amazon.com/lex/latest/dg//howitworks-manage-prompts.html#msg-prompts-response) and [Managing Conversation Context](https://docs.aws.amazon.com/lex/latest/dg//context-mgmt.html#special-response) in the Amazon Lex Developer Guide\.

Amazon Connect uses Amazon Polly, a service that converts text into lifelike speech using Speech Synthesis Markup Language \(SSML\)\. For more information, see [Using SSML](https://docs.aws.amazon.com/polly/latest/dg/ssml.html) in the Amazon Polly Developer Guide\.

SSML\-enhanced input text gives you more control over how Amazon Connect generates speech from the text you provide\. You can customize and control aspects of speech such as pronunciation, volume, and speed\. Amazon Polly provides this level of control using a subset of the SSML markup tags as defined by [Speech Synthesis Markup Language \(SSML\) Version 1\.1, W3C Recommendation](https://www.w3.org/TR/2010/REC-speech-synthesis11-20100907/)\.

### Modify a Prompt using SSML<a name="ssml-prompt"></a>

When you add a prompt to a contact flow, you can use SSML tags to provide a more personalized experience for your customers\. The default setting in a contact flow block for interpreting text to speech is **Text**\. To use SSML for text to speech in your contact flow blocks, set the **Interpret as** field to **SSML** as shown in the following image\.

![\[Image of the settings for a contact flow block showing the Text to speech Interpret as field set to SSML.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/connect-interpret-as-ssml.png)

The following SSML tags are supported in Amazon Connect:
+ speak
+ break
+ lang
+ mark
+ p
+ phoneme
+ prosody
+ s
+ say\-as
+ sub
+ w
+ amazon:effect name="whispered"

If you use an unsupported tag in your input text it is automatically ignored when it is processed\. To learn more about the SSML tags, see [SSML Tags in Amazon Polly](https://docs.aws.amazon.com/polly/latest/dg/supported-ssml.html)\.

## Create Quick Connects<a name="quick-connects"></a>

Calls can be transferred to an agent, a queue, or an external number\.
+ **External**—Calls are transferred to an external number \(such as an on\-call pager\)\. 
+ **Agent**—Calls are transferred to a specific agent as part of a contact flow\.
+ **Queue**—Calls are transferred to a queue as part of a contact flow\.

**To add a quick connect**

1. Choose **Routing**, **Quick connects**, **Add a new destination**\.

1. Enter a name for the item, and select a type, destination, contact flow \(if applicable\), and description\.
**Important**  
A description is required when you create a quick connect\. An error is returned if you do not add a description\.

1. To add more rows, choose **Add a new destination**\.

1. Choose **Save**\.

To see your quick connects in the contact list in CCP, add them to **Queues**\. Agent and queue quick connects only appear when an agent transfers a call\.

## Add an Amazon Lex Bot<a name="amazon-lex"></a>

With Amazon Lex, you can build conversational interactions \(bots\) that feel natural to your customers, giving you access to the same speech recognition and natural language understanding technology that powers Alexa\. After you create an Amazon Lex bot, you can add it to your instance and then integrate it into your contact flows\. You can add bots from the same Region as your Amazon Connect instance, or from a different Region\.

**Add an Amazon Lex bot to your instance**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. Choose the name of the instance from the **Instance Alias** column\.

1. In the navigation pane, choose **Contact flows**\.

1. Under **Amazon Lex**, in the **Region** drop\-down list, choose the Region in which you created your Amazon Lex bot\.

   If there are bots associated with your AWS account in the chosen Region, the bots are displayed in the **Bot** drop\-down list\. If no bots are found in the Region, or when there are no additional bots to add from that Region, the drop\-down menu is disabled\. A message indicates that there are no bots available to choose in that Region\.

1. In the **Bots** drop\-down menu, choose your bot, then choose **\+ Add Lex bot**\.

To create a new bot, choose **Create a new Lex bot** to open the Amazon Lex console\. You may need to select a Region where Amazon Lex is available\.

To remove a bot from your instance, choose **Remove** next to the bot to remove\.

## Resume a Contact Flow After Transfer<a name="contact-flow-resume"></a>

Use the **Transfer to phone number** block to transfer customers to a phone number outside of your Amazon Connect instance, and then optionally resume the contact flow when the call with the external number ends\. This lets you integrate interactions with external or third party organizations into your contact flow\. For example, you can use a **Transfer to phone number** block to transfer the caller to a shipping provider to check the status of their delivery, and then return the caller to an agent if they need further assistance\. Or, you could send the caller to another department in your organization that is not using Amazon Connect, and return the caller to the Amazon Connect contact flow to speak with an agent\.

### Using Resume After Transfer in a Contact Flow<a name="use-call-bridging"></a>

You can use the **Transfer to phone number** block to transfer customers to a number outside of your Amazon Connect instance, and then optionally resume the contact flow after the caller disconnects from the external number\. You can use the resume after transfer functionality to enable the following scenarios:
+ Transfer a caller to a number outside of your instance and end the contact flow\. For example, asking the customer for an order number, and then transferring the customer to the delivery company that can provide their shipping status\.
+ Transfer the customer to a number outside of your instance, and then return the customer to the contact flow to request a survey, or to speak to an agent\. For example, when the delivery company could not resolve the issue for the customer\.
+ For advanced automation, send tracking information as DTMF digits when the call is transferred, so that the shipment information is retrieved with the transferred call prior to the customer being connected\.

To resume a contact after a transfer to an external number, add a **Transfer to phone number** block to your contact flow\. In the **Transfer to phone number** block, enter the phone number to transfer the call to, and then connect it to the rest of your contact flow\. When the block executes, the call is transferred to the external number, and then, optionally, returned to the contact flow when the conversation with the external party ends\. The contact then follows the **Success** branch from the block to continue the flow\. If the call is not successfully transferred, one of the other branches is followed: **Call failed**, **Timeout**, or **Error**, depending on the reason the caller did not return to the flow\.

### Transfer to Phone Number Block Settings<a name="transfer-to-number-settings"></a>

The **Transfer to phone number** block includes the following settings:
+ **Transfer to**
  + **Phone number**—Sets the phone number to transfer the call to\.
  + **Use attribute**—Specify a contact attribute to set the phone number to transfer the call to\.
+ **Set timeout**
  + **Timeout \(in seconds\)**—The number of seconds to wait for the recipient to answer the transferred call\.
+ **Use attribute**—Specify a contact attribute to use to set the **Timeout** duration\.
+ **Resume contact flow after disconnect**—When you select this option, after the call is transferred, the caller is returned to the contact flow when the call with the third party ends\. Additional branches for **Success**, **Call failed**, and **Timeout** are added to the block when you select this option so that you can appropriately route contacts when there is an issue with the transfer\.
+ **Optional parameters**
  + **Send DTMF**—Select **Send DTMF** to include up to 50 Dual\-Tone Multi\-frequency \(DTMF\) characters with the transferred call\. You can enter the characters to include, or use an attribute\. Use the DTMF characters to navigate an automated IVR system that answers the call\.
  + **Caller ID number**—Specify the caller ID number used for transferred call\. You can select a number from your instance, or use an attribute to set the number\.
  + **Caller ID name**—Specify the caller ID name used for the transferred call\. You can enter a name, or use an attribute to set the name\.

    In some cases, the caller ID information is provided by the carrier of the party you are calling\. The information may not be up\-to\-date with that carrier, or the number may get passed differently between systems because of hardware or configuration differences\. If that is the case, the person you call may not see the phone number, or may see the name of a previously registered owner of the number, instead of the name you specify in the block\.

## Initiate an Outbound Call<a name="using-call-number-block"></a>

Use the **Call phone number** block in an outbound whisper flow to initiate an outbound call to a customer and, optionally, specify a custom caller ID number that is displayed to call recipients\. This is useful when you have multiple telephone numbers used to make outbound calls, but want to consistently display the same company phone number for the caller ID for calls made from your contact center\. You can also use the block to display a phone number for a specific line of business, or for displaying different numbers to customers based on their account type\.

When an outbound call is placed from your contact center, the number used to place the outbound call is the number selected as the **Outbound caller ID number** for the queue with which the outbound whisper flow is associated\. The caller ID number displayed to the call recipient is the number used to place the call\. In some cases, you may want to display a different number as the caller ID number for your organization\. For example, if you have customers in multiple geographic locations, you may want to display a number local to the area where your customers are\. Perhaps your organization has multiple lines of business serviced by a single set of agents, and want to display a different number from your instance for each line of business so that customers have the correct number to call back\.

When you use a **Call phone number** block in an outbound whisper flow, you can optionally set the caller ID number for outbound calls\. You can select any phone number from your instance, or use an attribute to set the number dynamically during the contact flow\. The attribute can be a user\-defined attribute you create using a **Set contact attributes** block in the contact flow, or an external attribute returned from an AWS Lambda function\. When you use an attribute to set the number, the value of the attribute must be a phone number from your instance in E\.164 format\. If the number is not in E\.164 format, the number from the queue associated with the outbound whisper flow is used for the caller ID number\. If no number is set for the outbound caller ID number for the queue, the call attempt will fail\.

For more information about E\.164, see [Use E\.164 Format for Telephone Numbers](amazon-connect-contact-control-panel.md#international-calls-ccp)\.

The **Call phone number** block is supported only in outbound whisper flow contact flows\. Only published contact flows can be selected as the outbound whisper flow for a queue\.

### How it Works<a name="call-number-block-how-it-works"></a>

Outbound whisper flows execute in Amazon Connect immediately after an agent accepts the call during direct dial and callback scenarios\. When the contact flow executes, the caller ID number is set if one is specified in the **Call phone number** block\. If no caller ID is specified in the **Call phone number** block, the caller ID number defined for the queue is used when the call is placed\. When there is an error with a call that is initiated by the **Call phone number** block, the call is disconnected and the agent is placed in ACW status\.

### Specify a custom caller ID number using a **Call phone number** block

1. In Amazon Connect choose **Routing**, **Contact flows**\.

1. Choose the down arrow next to **Create contact flow**, and then choose **Create outbound whisper flow**\.

1. Add a **Call phone number** block to the flow, and connect the **Entry point** block to it\.

   The **Call phone number** block must be placed before a **Play prompt** block if one is included in your contact flow\.

1. Select the **Call phone number** block, and then select **Caller ID number to display**\.

1. Do one of the following:
   + To use a number from your instance, choose **Select a number from your instance**, and then search for or select the number to use from the drop\-down\.
   + Choose **Use attribute** to use a contact attribute to provide the value for the caller ID number\. You can use either a **User Defined** attribute you create using a **Set contact attributes** block, or an **External** attribute returned from an AWS Lambda function\. The value of any attribute you use must be a phone number claimed for your instance and be in E\.164 format\. If the number used from an attribute is not in E\.164 format, the number set for the **Outbound caller ID number** for the queue is used\.

1. Add any additional blocks to complete your contact flow, and connect the **Success** branch of the **Call phone number** block to the next block in the flow\. Note that there is no error branch for the block\. If a call is not successfully initiated, the contact flow ends and the agent is placed in ACW state\.

## Manage Calls in a Queue<a name="queue-to-queue-transfer"></a>

For calls coming into your contact center, you can define advanced routing decisions to minimize queue wait times, or route calls to specific queues, using blocks in your contact flow\. For example, use a **Check queue status** block to check staffing or agent availability for a queue before sending a call to that queue, or use a **Get queue metrics** block to retrieve queue metrics\. Then use a **Check contact attributes** block to check specific queue metric attributes, and define conditions in the block to determine which queue to route the call to based on attribute values\. For more information about using queue metrics, see [Using System Metric Attributes](connect-contact-attributes.md#attrib-system-metrics)\.

After determining which queue to transfer the call to, use a **Transfer to queue** block in a contact flow to transfer the call to that queue\. When the **Transfer to queue** block runs, it checks the queue capacity to determine whether or not the queue is at capacity \(full\)\. This check for queue capacity compares the current number of calls in the queue to the **Maximum contacts in queue** limit, if one is set for the queue\. If no limit is set, the queue is limited to the number of concurrent active calls set in the service limit for the instance\.

After the call is placed in a queue, the call remains there until an agent takes the call, or until the call is handled based on the routing decisions in your customer queue flow\. To change the queue associated with the call after it is already placed in a queue, use a **Loop prompts** block with a **Transfer to queue** block in a customer queue flow\. In the block choose which queue to transfer the call to, or use an attribute to set the queue\.

In the **Transfer to queue** block, there are two outputs to route calls through: the **Success** branch or the **At capacity** branch\. When a call is successfully transferred to a queue and follows the **Success** branch, the call remains associated with the current customer queue flow after being transferred\. When the call is not successfully transferred to a queue and follows the **At capacity** branch because the queue is at capacity, the call remains in the current working queue\.

**To manage calls in a queue using a Transfer to queue block**

1. In Amazon Connect, choose **Routing**, **Contact flows**\.

1. Choose the down arrow next to **Create contact flow**, then choose **Create customer queue flow**\.

1. Under **Interact**, add a **Loop prompts** block to provide a message to the caller when the call is transferred, then every X seconds or minutes while the call is in the queue\.

1. Select the **Loop prompts** block to display the settings for the block\.

1. Choose **Add another prompt to the loop**\.

1. Under **Prompts**, do one of the following:
   + Choose **Audio recording** in the drop\-down menu, then select the audio recording to use as the prompt\.
   + Choose **Text to Speech** in the drop\-down menu, then enter text to use for the prompt in the **Enter text to be spoken** field\.

1. To set an interrupt, choose **Interrupt every**, enter a value for the interrupt interval, and then choose a unit, either **Minutes** or **Seconds**\. We recommend that you use an interval greater than 20 seconds to ensure that queued contacts that are being connected to an agent are not interrupted\.

1. Choose **Save**\.

1. Connect the block to the **Entry point** block in the contact flow\.

1. Under **Terminate/Transfer**, drag a **Transfer to queue** block onto the designer\.

1. Select the title of the block to display the settings for the block, then choose the **Transfer to queue** tab\.

1. Under **Queue to check**, choose **Select a queue**, then select the queue to transfer calls to\.

   Alternatively, choose **Use attribute**, then reference an attribute to specify the queue\. If you use an attribute to set the queue, the value must be the queue ARN\.

1. Choose **Save**\.

1. Connect the **Loop prompt** block to the **Transfer to queue** block\.

1. Add additional blocks to complete the contact flow that you require, such as the blocks to check queue status or metrics, then choose **Save**\.

   The contact flow is not active until you publish it\.

**Important**  
To successfully complete the call transfer to another queue, you must include a block after the **Transfer to queue** block and connect the **Success** branch to it\. For example, use an **End flow / Resume** block to end the contact flow\. The flow does not end until the call is picked up by an agent\.

## Transfer Calls Directly to a Specific Agent<a name="transfer-to-agent"></a>

With agent queues, you can route calls directly to a specific agent\. This can allow you to provide a consistent customer experience for your customers by letting you route calls directly to the agent the customer last interacted with if that agent is available\. In each block that supports transferring the contact to a queue, such as the **Transfer to queue** block, there is a **By agent** radio button under **Queue** \(or **Queue to check \(optional\)** or **By queue** depending on the block\)\. When you select **By agent**, a drop\-down list that includes all of the users in your instance is displayed\. When you select a user name, the contact is transferred to the queue for that user\.

Contact flow blocks in which you can specify a queue include: **Set working queue**, **Get queue metrics**, **Check queue status**, **Check staffing**, and **Transfer to queue** when used in a customer queue flow\.

**Note**  
A queue is created for all users in your Amazon Connect instance, but only users assigned permissions to use the Contact Control Panel \(CCP\) can use the CCP to receive calls\. The Agent or Admin security profiles are the only default security profiles that include permissions to use the CCP\. If you route a call to a user that cannot access the CCP, the contact can never be answered\.

**To route a call directly to a specific agent**

1. In Amazon Connect, choose **Routing**, **Contact flows**\.

1. In the contact flow designer, open an existing contact flow, or create a new one\.

1. Add a block in which you can select a queue to transfer a contact to, such as a **Set working queue** block\.

1. Select the title of the block to open the block settings\.

1. Select **By agent**\.

1. Under **Select an agent**, enter the user name of the agent, or select the agent's user name from the drop\-down list\.

1. Choose **Save**\.

1. Connect the **Success** branch to the next block in your contact flow\.

You can also choose to use an attribute to select the queue created for the agent user account\. To do so, after you choose **By agent**, choose **Use attribute**\.

### Using Contact Attributes to Route Contacts to a Specific Agent<a name="use-attribs-agent-queue"></a>

When you use contact attributes in a contact flow to route calls to an agent, the attribute value must be either the agent's user name, or the agent's user ID\.

To determine the user ID for an agent so that you can use the value as an attribute, use the [ListUsers](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListUsers.html) operation to retrieve the users from your instance\. The agent's user ID is returned with the results from the operation as the value of the `Id` in the [UserSummary](https://docs.aws.amazon.com/connect/latest/APIReference/API_UserSummary.html) object\.

You can also find the user ID for an agent by using [Amazon Connect Agent Event Streams](agent-event-streams.md)\. The agent events, which are included in the agent event data stream, include the agent ARN\. The user ID is included in the agent ARN after `agent/`\. In the following example, agent event data, the agent ID is **87654321\-4321\-4321\-4321\-123456789012**\.

```
{
    "AWSAccountId": "123456789012",
    "AgentARN": "arn:aws:connect:us-west-2:123456789012:instance/12345678-1234-1234-1234-123456789012/agent/87654321-4321-4321-4321-123456789012",
    "CurrentAgentSnapshot": {
        "AgentStatus": {
            "ARN": "arn:aws:connect:us-west-2:123456789012:instance/12345678-1234-1234-1234-123456789012/agent-state/76543210-7654-6543-8765-765432109876",
            "Name": "Available",
            "StartTimestamp": "2019-01-02T19:16:11.011Z"
        },
        "Configuration": {
            "AgentHierarchyGroups": null,
            "FirstName": "IAM",
            "LastName": "IAM",
            "RoutingProfile": {
                "ARN": "arn:aws:connect:us-west-2:123456789012:instance/12345678-1234-1234-1234-123456789012/routing-profile/aaaaaaaa-bbbb-cccc-dddd-111111111111",
                "DefaultOutboundQueue": {
                    "ARN": "arn:aws:connect:us-west-2:123456789012:instance/12345678-1234-1234-1234-123456789012/queue/aaaaaaaa-bbbb-cccc-dddd-222222222222",
                    "Name": "BasicQueue"
                },
                "InboundQueues": [{
                    "ARN": "arn:aws:connect:us-west-2:123456789012:instance/12345678-1234-1234-1234-123456789012/queue/aaaaaaaa-bbbb-cccc-dddd-222222222222",
                    "Name": "BasicQueue"
                }],
                "Name": "Basic Routing Profile"
            },
            "Username": "agentUserName"
        },
        "Contacts": []
},
```