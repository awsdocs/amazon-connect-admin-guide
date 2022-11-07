# Sample disconnect flow<a name="sample-disconnect"></a>

**Note**  
This topic explains a sample flow that is included with Amazon Connect\. For information about locating the sample flows in your instance, see [Sample flows](contact-flow-samples.md)\. 

Type: Flow \(inbound\)

This sample works with voice, chat, and task contacts\.

**Chat contacts**

1. The **Play prompt** block shows a text message that the agent has disconnected\.

1. A **Wait** block sets the timeout period for 15 minutes\. If the customer returns in 15 minutes, the customer is transferred to a queue to chat with another agent\. 

1. If the customer doesn't return, the timer expires and the chat disconnects\. 

**Voice contacts**

1. Sets a user\-defined attribute, DisconnectFlowRun\. If it = Y, disconnect\.

1. Gets customer input, whether they were happy with service\.

1. Terminates flow\.

**Task contacts**

1. Checks contact attributes, whether Agent ARN = NULL\.

1. Transfers to agent's queue\.

1. If at capacity, disconnects\.

For a list and description of all the disconnect reasons, see **DisconnectReason** in the [ContactTraceRecord](ctr-data-model.md#ctr-ContactTraceRecord)\. 