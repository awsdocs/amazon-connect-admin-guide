# Amazon Connect agent event streams<a name="agent-event-streams"></a>

Amazon Connect agent event streams are Amazon Kinesis data streams that provide you with near real\-time reporting of agent activity within your Amazon Connect instance\. The events published to the stream include these CCP events: 
+ Agent login
+ Agent logout
+ Agent connects with a contact
+ Agent status change, such as to Available to handle contacts, or on Break or at Training\. 

You can use the agent event streams to create dashboards that display agent information and events, integrate streams into workforce management \(WFM\) solutions, and configure alerting tools to trigger custom notifications of specific agent activity\. Agent event streams help you manage agent staffing and efficiency\.

**Topics**
+ [Enable agent event streams](agent-event-streams-enable.md)
+ [Sample agent event stream](sample-agent-event-stream.md)
+ [Determine how long an agent spends doing ACW](determine-acw-time.md)
+ [Agent event streams data model](agent-event-stream-model.md)