# Determine how long an agent spends doing ACW<a name="determine-acw-time"></a>

There's no event in the agent event stream that tells you how long a contact is in the ACW state, and by extension how long an agent spends doing ACW\. However, there's other data in the agent event stream that you can use to figure this out\. 

First, identify when the contact entered ACW\. Here's how to do that: 

1. Identify when the conversation between the contact and agent `ENDED`\.

1. View the `StateStartTimeStamp` for the event\.

For example, in the following agent event stream output, the contact enters ACW state at "**StateStartTimestamp**": "2019\-05\-25T18:55:27\.017Z"\.

**Tip**  
In the agent event stream, events are listed in reverse chronological order\. We recommend reading through following examples by starting at the bottom of each example\.

```
{
    "AWSAccountId": "012345678901",
    "AgentARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/agent/agent-ARN",
    "CurrentAgentSnapshot": {
        "AgentStatus": {
            "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/agent-state/agent-state-ARN",
            "Name": "Available",  //This just refers to the status that the agent sets manually in the CCP. 
                It means they are ready to handle contacts, not say, on Break.  
            "StartTimestamp": "2019-05-25T18:43:59.049Z"
        },
        "Configuration": {
            "AgentHierarchyGroups": null,
            "FirstName": "(Removed)",
            "LastName": "(Removed)",
            "RoutingProfile": {
                "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/routing-profile/routing-profile-ARN",
                "DefaultOutboundQueue": {
                    "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                    "Name": "BasicQueue"
                },
                "InboundQueues": [
                    {
                        "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                        "Name": "BasicQueue"
                    },
                    {
                        "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-PrimaryQueue",
                        "Name": "PrimaryQueue"
                    }
                ],
                "Name": "Basic Routing Profile"
            },
            "Username": "(Removed)"
        },
        "Contacts": [
            {
                "Channel": "VOICE",
                "ConnectedToAgentTimestamp": "2019-05-25T18:55:21.011Z",
                "ContactId": "ContactId-1",  //This is the same contact the agent was working on when their state was CONNECTED (below). 
                    Since it's still the same contact but they aren't connected, we know the contact is now in ACW state.
                "InitialContactId": null,
                "InitiationMethod": "OUTBOUND",  //This indicates how the contact was initiated. OUTBOUND means the agent initiated contact with the customer. 
                    INBOUND means the customer initiated contact with your center.
                "Queue": {
                    "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                    "Name": "BasicQueue"
                },
                "QueueTimestamp": null,
                "State": "ENDED",  //This shows the conversation has ended. 
                "StateStartTimestamp": "2019-05-25T18:55:27.017Z"  //This is the timestamp for the ENDED event (above), 
                    which is when the contact entered ACW state.
            }
        ]
    },
    "EventId": "EventId-1",
    "EventTimestamp": "2019-05-25T18:55:27.017Z",
    "EventType": "STATE_CHANGE",  //This shows that the state of the contact has changed; above we can see the conversation ENDED. 
    "InstanceARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111",
    "PreviousAgentSnapshot": {
        "AgentStatus": {
            "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/agent-state/agent-state-ARN",
            "Name": "Available", //This just refers to the status that the agent sets manually in the CCP. 
                It means they were ready to handle contacts, not say, on Break.  
            "StartTimestamp": "2019-05-25T18:43:59.049Z"
        },
        "Configuration": {
            "AgentHierarchyGroups": null,
            "FirstName": "(Removed)",
            "LastName": "(Removed)",
            "RoutingProfile": {
                "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/routing-profile/routing-profile-ARN",
                "DefaultOutboundQueue": {
                    "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                    "Name": "BasicQueue"
                },
                "InboundQueues": [
                    {
                        "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                        "Name": "BasicQueue"
                    },
                    {
                        "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-PrimaryQueue",
                        "Name": "PrimaryQueue"
                    }
                ],
                "Name": "Basic Routing Profile"
            },
            "Username": "(Removed)"
        },
        "Contacts": [
            {
                "Channel": "VOICE",  //This shows the agent and contact were talking on the phone. 
                "ConnectedToAgentTimestamp": "2019-05-25T18:55:21.011Z",
                "ContactId": "ContactId-1",  //This shows the agent was working with a contact identified as "ContactId-1".
                "InitialContactId": null,
                "InitiationMethod": "OUTBOUND",
                "Queue": {
                    "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                    "Name": "BasicQueue"
                },
                "QueueTimestamp": null,
                "State": "CONNECTED",  //This shows the contact was CONNECTED to the agent, instead of say, MISSED. 
                "StateStartTimestamp": "2019-05-25T18:55:21.011Z"  //This shows when the contact was connected to the agent.
            }
        ]
    },
    "Version": "2019-05-25"
}
```

Next, determine when a contact left ACW\. Here's how to do that: 

1. Find where the `CurrentAgentSnapshot` has no contacts, and the state for the contact listed in the `PreviousAgentSnapshot` equals ENDED\.

   Because a STATE\_CHANGE event also occurs when the agent's configuration is changed, such as when they are assigned a different routing profile, this step confirms you have the right event\.

1. Find where the `EventType` = "STATE\_CHANGE"\.

1. View the `EventTimeStamp` for it\.

For example, in the following agent event stream file, the contact left ACW at "**EventTimestamp**": "2019\-05\-25T18:55:32\.022Z"\.

```
{
    "AWSAccountId": "012345678901",
    "AgentARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/agent/agent-ARN",
    "CurrentAgentSnapshot": {
        "AgentStatus": {
            "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/agent-state/agent-state-ARN",
            "Name": "Available",  //This just refers to the status that the agent sets manually in the CCP. It means they 
                are ready to handle contacts, not say, on Break. 
            "StartTimestamp": "2019-05-25T18:43:59.049Z"
        },
        "Configuration": {
            "AgentHierarchyGroups": null,
            "FirstName": "(Removed)",
            "LastName": "(Removed)",
            "RoutingProfile": {
                "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/routing-profile/routing-profile-ARN",
                "DefaultOutboundQueue": {
                    "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                    "Name": "BasicQueue"
                },
                "InboundQueues": [
                    {
                        "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                        "Name": "BasicQueue"
                    },
                    {
                        "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-PrimaryQueue",
                        "Name": "PrimaryQueue"
                    }
                ],
                "Name": "Basic Routing Profile"
            },
            "Username": "(Removed)"
        },
        "Contacts": []  //Since a contact isn't listed here, it means ACW for ContactId-1 (below)
            is finished, and the agent is ready for a new contact to be routed to them. 
    },
    "EventId": "477f2c4f-cd1a-4785-b1a8-97023dc1229d",
    "EventTimestamp": "2019-05-25T18:55:32.022Z",  //Here's the EventTimestamp for the STATE_CHANGE event. This is when
        the contact left ACW.
    "EventType": "STATE_CHANGE",  //Here's the STATE_CHANGE
    "InstanceARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111",
    "PreviousAgentSnapshot": {
        "AgentStatus": {
            "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/agent-state/agent-state-ARN",
            "Name": "Available",  //This just refers to the status that the agent sets manually in the CCP. 
                It means they were at work, not say, on Break. 
            "StartTimestamp": "2019-05-25T18:43:59.049Z"
        },
        "Configuration": {
            "AgentHierarchyGroups": null,
            "FirstName": "(Removed)",
            "LastName": "(Removed)",
            "RoutingProfile": {
                "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/routing-profile/routing-profile-ARN",
                "DefaultOutboundQueue": {
                    "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                    "Name": "BasicQueue"
                },
                "InboundQueues": [
                    {
                        "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                        "Name": "BasicQueue"
                    },
                    {
                        "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-PrimaryQueue",
                        "Name": "PrimaryQueue"
                    }
                ],
                "Name": "Basic Routing Profile"
            },
            "Username": "(Removed)"
        },
        "Contacts": [
            {
                "Channel": "VOICE",
                "ConnectedToAgentTimestamp": "2019-05-25T18:55:21.011Z",
                "ContactId": "ContactId-1",  //This is the ContactId of the customer the agent was working on previously. 
                "InitialContactId": null,
                "InitiationMethod": "OUTBOUND",
                "Queue": {
                    "ARN": "arn:aws:connect:us-east-1:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN-for-BasicQueue",
                    "Name": "BasicQueue"
                },
                "QueueTimestamp": null,
                "State": "ENDED", //The ACW for ContactId-1 has ended.  
                "StateStartTimestamp": "2019-05-25T18:55:27.017Z"
            }
        ]
    },
    "Version": "2019-05-25"
}
```

Finally, to calculate the amount of time the contact was in the ACW state, and thus how long the agent spent working on it:
+ Subtract the "**StateStartTimestamp**": "2019\-05\-25T18:55:27\.017Z" from the "**EventTimestamp**": "2019\-05\-25T18:55:32\.022Z"\. 

In this example, the agent spent 5\.005 seconds doing ACW for ContactId\-1\. 