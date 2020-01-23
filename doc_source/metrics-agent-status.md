# About Agent Status<a name="metrics-agent-status"></a>

Agents have a status\. It's manually set in the Contact Control Panel \(CCP\)\. 
+ When they're ready to handle contacts, they set their status in the CCP to **Available**\. This means inbound contacts can be routed to them\.
+ When agents want to stop taking inbound contacts, they set their status to a custom status that you create, such as **Break** or **Training**\. They can also change their status to **Offline**\.

It's possible for agents to make outbound calls when their status in the CCP is set to a custom status\. Technically, agents can make an outbound call when their CCP is set to **Offline**\. 

For example, an agent wants to make an outbound call to a contact\. Because they don't want contacts to be routed to them during this time, they set their status to a custom status\. So when you look at your metrics, you'll see the agent is simultaneously on **NPT** \(the metric that indicates a custom status\) and **On Call**, for example\.

## About ACW \(After Contact Work\)<a name="agent-status-acw"></a>

After a conversation between an agent and customer ends, the contact is moved into the ACW state, not the agent\. The agent's status in the CCP is still set to **Available**\. 

When the agent finishes doing ACW for the contact, they click **Clear** to clear that slot so another contact can be routed to them\.

Because we're tracking the contact state, if you want to identify how long an agent spent on ACW for a contact:
+ In the historical metrics report, **After contact work time** captures the amount of time each contact spent in ACW\.
+ In the agent event stream, you have to do some calculations\. For more information, see [Determine How Long an Agent Spends Doing ACW](determine-acw-time.md)\.

## How Do You Know When an Agent Can Handle Another Contact?<a name="w21aac42c15c15"></a>

The **Availability** metric tells you when agents are finished with a contact and ready to have another one routed to them\.

## What Appears in the Real\-Time Metrics Report?<a name="w21aac42c15c17"></a>

To find out what the agent status is in the real\-time metrics report, look at the **Status** metric\.

## What Appears in the Agent Event Stream?<a name="agent-status-in-agent-event-stream"></a>

In the agent event stream you'll see the **AgentStatus**, for example: 

```
{
 "AWSAccountId": "012345678901",
 "AgentARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/agent/agent-ARN",
  "CurrentAgentSnapshot": {
      "AgentStatus": {   //Here's the agent's status that they set in the CCP.  
          "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/agent-state/agent-state-ARN",
          "Name": "Available",  //When an agent sets their status to "Available" it means they are ready for
              inbound contacts to be routed to them, and not say, at Lunch.  
          "StartTimestamp": "2019-05-25T18:43:59.049Z"
      },
```