# About contact states<a name="about-contact-states"></a>

Contact states appear in two places: the real\-time metrics reports and the agent event stream\.

## Contact states in the agent event stream<a name="contact-states-agent-event-stream"></a>

There are different events that can appear in the lifecycle of a contact\. Each of these events appear in the agent event stream as a **State**\. A contact can have the following states that appear in the agent event stream:
+ INCOMING \- This is specific to queued callbacks\. The agent is presented with a callback\.
+ PENDING \- This is specific to queued callbacks\.
+ CONNECTING \- An inbound contact is being offered to the agent \(it's ringing\)\. The agent has not yet taken any action to accept or reject the contact, and they haven't missed it\.
+ CONNECTED \- The agent has accepted the contact\. Now the customer is in a conversation with the agent\.
+ CONNECTED\_ONHOLD \- They are in a conversation with the agent, and the agent has put the customer on hold\.
+ MISSED \- The contact was missed by the agent\.
+ ERROR \- This appears when, for example, the customer abandons the call during outbound whisper\.  
+ ENDED \- The conversation has ended, and the agent has started doing ACW for that contact\.
+ REJECTED \- The contact was rejected by the agent or the customer abandoned the contact when it is connecting to the agent\. This applies to chat and tasks\. 

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

## Events in the contact record<a name="ctr-events"></a>

A contact record captures events associated with the contact in your contact center\. For example, how long the contact lasted, when it started and stopped\. For a list of all data that's captured in the contact record, see [Contact records data model](ctr-data-model.md)\. 

A contact record is opened for a customer when they are connected to your contact center\. The contact record is completed when the interaction with the flow or agent ends \(that is, the agent has completed the ACW and cleared the contact\)\. This means it's possible for a customer to have multiple contact records\.

The following diagram shows when a contact record is created for a contact\. It shows three contact records for a contact: 
+ The first record is created when the contact is connected to Agent 1\.
+ The second record is created when the contact is transferred to Agent 2\.
+ The third record is created when the contact is connected to Agent 3 during a callback\.

![\[Three boxes, one for each contact record that is created.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ctr-diagram.png)

Each time a contact is connected to an agent, a new contact record is created\. The contact records for a contact are linked together through the contactId fields: initial, next, and previous\. 

**Tip**  
A contact is considered connected when a contact record is created\. It's possible a contact record can be created before a call is finished ringing for the caller, due to network conditions and PSTN event propagation\.