# Amazon Connect Agent Event Streams<a name="agent-event-streams"></a>

Amazon Connect agent event streams are Amazon Kinesis data streams that provide you with near real\-time reporting of agent activity within your Amazon Connect instance\. The events published to the stream include these CCP events: 
+ Agent login
+ Agent logout
+ Agent connects with a contact
+ Agent status change, such as to Available to handle contacts, or on Break or at Training\. 

You can use the agent event streams to create dashboards that display agent information and events, integrate streams into workforce management \(WFM\) solutions, and configure alerting tools to trigger custom notifications of specific agent activity\. Agent event streams help you manage agent staffing and efficiency\.

**Topics**
+ [Enable Agent Event Streams](agent-event-streams-enable.md)
+ [Sample Agent Event Stream](sample-agent-event-stream.md)
+ [Determine How Long an Agent Spends Doing ACW](determine-acw-time.md)
+ [Agent Event Streams Data Model](agent-event-stream-model.md)