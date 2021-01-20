# Sample disconnect flow<a name="sample-disconnect"></a>

Type: Contact flow \(inbound\)

1. The **Play prompt** block shows a text message that the agent has disconnected\.

1. A **Wait** block sets the timeout period for 15 minutes\. If the customer returns in 15 minutes, the customer is transferred to a queue to chat with another agent\. 

1. If the customer doesn't return, the timer expires and the chat disconnects\. 