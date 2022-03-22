# Sample disconnect flow<a name="sample-disconnect"></a>

**Note**  
This topic explains a sample contact flow that is included with Amazon Connect\. For information about locating the sample flows in your instance, see [Sample contact flows](contact-flow-samples.md)\. 

Type: Contact flow \(inbound\)

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