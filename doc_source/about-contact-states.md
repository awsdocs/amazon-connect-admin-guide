# About Contact States<a name="about-contact-states"></a>

Contact states appear in two places: the real\-time metrics reports and the agent event stream\.

## Contact States in the Agent Event Stream<a name="contact-states-agent-event-stream"></a>

There are different events that can appear in the lifecycle of a contact\. Each of these events appear in the agent event stream as a **State**\. A contact can have the following states that appear in the agent event stream:
+ INCOMING \- This is specific to queued callbacks\. The agent is presented with a callback\.
+ PENDING \- This is specific to queued callbacks\.
+ CONNECTING \- The agent has accepted the contact\. Now the contact object is being connected to the customer\.
+ CONNECTED \- They are in a conversation with the agent\.
+ CONNECTED\_ONHOLD \- They are in a conversation with the agent, and the agent has put the customer on hold\.
+ MISSED \- The contact was missed by the agent\.
+ ERROR \- This appears when, for example, the customer abandons the call during outbound whisper\.  
+ ENDED \- The conversation has ended, and the agent has started doing ACW for that contact\.

Here's what the contact state looks like in the agent event stream:

```
 
"Contacts": [
  {
    "Channel": "VOICE",  //This shows the agent and contact were talking on the phone. 
    "ConnectedToAgentTimestamp": "2019-05-25T18:55:21.011Z",
    "ContactId": "ContactId-1",  //This shows the agent was working with a contact identified as "ContactId-1".
    "InitialContactId": null,
    "InitiationMethod": "OUTBOUND", //This shows the agent reached the customer by making an outbound call.
    "Queue": {
         "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
     },
    "QueueTimestamp": null,
    "State": "CONNECTED",  //Here's the contact state. In this case, it shows the contact was CONNECTED to the agent,
      instead of say, MISSED. 
    "StateStartTimestamp": "2019-05-25T18:55:21.011Z"  //This shows when the contact was connected to the agent.
   }
  ]
```

### Events in the Contact Trace Record \(CTR\)<a name="ctr-events"></a>

A contact trace record \(CTR\) captures events associated with the contact in your contact center\. For example, how long the contact lasted, when it started and stopped\. For a list of all data that's captured in the CTR, see [Contact Trace Records Data Model](ctr-data-model.md)\. 

A CTR is opened for a customer when they are connected to your contact center\. The CTR is completed when the interaction with the contact flow or agent ends\. This means it's possible for a customer to have multiple CTRs\.

The following diagram shows when a CTR is created for a contact\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ctr-diagram.png)

Each time a contact is connected to an agent, a new CTR is created\. The CTRs for a contact are linked together through the contactId fields: original, next, and previous\. 