# Sample agent event stream<a name="sample-agent-event-stream"></a>

In the following sample agent event stream, the agent is assigned to a routing profile that requires them to take both chats and calls\. They can take one call, and up to three chats at a time\. 

**Note**  
For how many chats and tasks an agent can take concurrently, see [Amazon Connect service quotas](amazon-connect-service-limits.md)\.

```
{
    "AWSAccountId": "012345678901",
    "AgentARN": "arn:aws:connect:us-west-2:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/agent/agent-ARN",
    "CurrentAgentSnapshot": 
      {
    "AgentStatus": {
            "ARN": "example-ARN", //The ARN for the agent's current agent status (not for the agent).
            "Name": "Available",  //This shows the agent status in the CCP is set to Available. 
            "StartTimestamp": "2019-08-13T20:52:30.704Z"
        },
     "NextAgentStatus": {
            "Name": "Lunch", //They set their next status, which pauses new contacts being routed to them while they finish their current contacts.
            "ARN": "example-ARN2",  //The ARN of the agent status that the agent has set as their next status. 
            "EnqueuedTimestamp": "2019-08-13T20:58:00.004Z",   //When the agent set their next status and paused routing of incoming contacts.
        }
      } ,
        "Configuration": {
            "AgentHierarchyGroups": null,
            "FirstName": "AgentEventStreamTest",
            "LastName": "Agent",
            "RoutingProfile": {
                "ARN": "arn:aws:connect:us-west-2:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/routing-profile/routing-profile-ARN",
                "Concurrency": [
                    {
                        "AvailableSlots": 3, //This shows the agent has 3 slots available. 
                                            //They aren't on any chats right now.
                        "Channel": "CHAT",
                        "MaximumSlots": 3  //The agent's routing profile allows them to take up to 3 chats.
                    },
                    {
                        "AvailableSlots": 1, //The agent has 1 slot available to take a call.
                        "Channel": "VOICE",
                        "MaximumSlots": 1  //The agent's routing profile allows them to take 1 call at a time.
                    }
                ],
                "DefaultOutboundQueue": {
                    "ARN": "arn:aws:connect:us-west-2:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN",
                    "Channels": [
                        "VOICE"  //This outbound queue only works for calls. 
                    ],
                    "Name": "OutboundQueue"  
                },
                "InboundQueues": [
                    {
                        "ARN": "arn:aws:connect:us-west-2:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/agent/agent-ARN",
                        "Channels": [
                            "VOICE",
                            "CHAT"
                        ],
                        "Name": null  //This queue has a name of "null" because it's an agent queue, 
                                      //and agent queues don't have names.
                    },
                    {
                        "ARN": "arn:aws:connect:us-west-2:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN",
                        "Channels": [
                            "CHAT",
                            "VOICE"
                        ],
                        "Name": "Omni-channel-queue" //This inbound queue takes both chats and calls. 
                    }
                ],
                "Name": "AgentEventStreamProfile"
            },
            "Username": "aestest"
        },
        "Contacts": [ ]
    },
    "EventId": "EventId-1",
    "EventTimestamp": "2019-08-13T20:58:44.031Z",
    "EventType": "HEART_BEAT",
    "InstanceARN": "arn:aws:connect:us-west-2:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111",
    "PreviousAgentSnapshot": {
        "AgentStatus": {
            "ARN": "arn:aws:connect:us-west-2:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/agent-state/agent-state-ARN",
            "Name": "Offline",
            "StartTimestamp": "2019-08-13T20:52:30.704Z"
        },
        "Configuration": {
            "AgentHierarchyGroups": null,
            "FirstName": "AgentEventStreamTest",
            "LastName": "Agent",
            "RoutingProfile": {
                "ARN": "arn:aws:connect:us-west-2:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/routing-profile/routing-profile-ARN",
                "Concurrency": [
                    {
                        "AvailableSlots": 3,
                        "Channel": "CHAT",
                        "MaximumSlots": 3
                    },
                    {
                        "AvailableSlots": 1,
                        "Channel": "VOICE",
                        "MaximumSlots": 1
                    }
                ],
                "DefaultOutboundQueue": {
                    "ARN": "arn:aws:connect:us-west-2:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN",
                    "Channels": [
                        "VOICE"
                    ],
                    "Name": "OutboundQueue"
                },
                "InboundQueues": [
                    {
                        "ARN": "arn:aws:connect:us-west-2:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/agent/agent-ARN",
                        "Channels": [
                            "VOICE",
                            "CHAT"
                        ],
                        "Name": null
                    },
                    {
                        "ARN": "arn:aws:connect:us-west-2:012345678901:instance/aaaaaaaa-bbbb-cccc-dddd-111111111111/queue/queue-ARN",
                        "Channels": [
                            "CHAT",
                            "VOICE"
                        ],
                        "Name": "Omni-channel-queue"
                    }
                ],
                "Name": "AgentEventStreamProfile"
            },
            "Username": "aestest"
        },
        "Contacts": [ ]
    },
    "Version": "2017-10-01"
}
```