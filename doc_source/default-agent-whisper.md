# Default agent whisper: name of the queue<a name="default-agent-whisper"></a>

This contact flow plays for the agent immediately before the call is connected with the customer\. This type of flow can be used to play a prompt for the agent\. 

The name of the queue is played to the agent\. It identifies for the agent the queue that the customer was in\. The name of the queue is retrieved from the system variable `$.Queue.Name`\. 

For more information about system variables, see [Contact flow system attributes](connect-attrib-list.md#attribs-system-table)\.

For instructions about how to override and change a default contact flow, see [Change a default contact flow](change-default-contact-flow.md)\.