# Default agent whisper: name of the queue<a name="default-agent-whisper"></a>

This flow uses a [Set whisper flow](set-whisper-flow.md) block to play a message for the agent when the customer and agent are joined\. 

The name of the queue is played to the agent\. It identifies the queue that the customer was in\. The name of the queue is retrieved from the system variable `$.Queue.Name`\. 

Use the [Set whisper flow](set-whisper-flow.md) block to override the default agent whisper in a voice conversation\.

**Important**  
For chat conversations, you need to include a [Set whisper flow](set-whisper-flow.md) for default agent or customer whispers to play\. For instructions, see [Set the default whisper flow for a chat conversation](set-default-whisper-flow-for-chat.md)\.

For more information about system variables, see [System attributes](connect-attrib-list.md#attribs-system-table)\.

**Tip**  
Wondering if a default flow has been changed? Use [flow version control](flow-version-control.md) to view the original version of the flow\. 