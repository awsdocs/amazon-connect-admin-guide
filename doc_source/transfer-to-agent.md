# Transfer Contacts to a Specific Agent<a name="transfer-to-agent"></a>

Agent queues enable you to route contacts directly to a specific agent\. Following are a couple of scenarios where you might want to do this: 
+ Route contacts to the last agent the customer interacted with\. This provides a consistent customer experience\.
+ Route contacts to agents who have specific responsibilities\. For example, you might route all billing questions to Jane\.

**Note**  
A queue is created for all users in your Amazon Connect instance, but only users who are assigned permissions to use the Contact Control Panel \(CCP\) can use it to receive contacts\. The Agent and Admin security profiles are the only default security profiles that include permissions to use the CCP\. If you route a contact to someone who doesn't have these permissions, the contact can never be handled\.

**To route a contact directly to a specific agent**

1. In Amazon Connect, choose **Routing**, **Contact flows**\.

1. In the contact flow designer, open an existing contact flow, or create a new one\.

1. Add a block in which you can select a queue to transfer a contact to, such as a **Set working queue** block\.

1. Select the title of the block to open the block settings\.

1. Select **By agent**\.

1. Under **Select an agent**, enter the user name of the agent, or select the agent's user name from the drop\-down list\.

1. Choose **Save**\.

1. Connect the **Success** branch to the next block in your contact flow\.

You can also choose to use an attribute to select the queue created for the agent user account\. To do so, after you choose **By agent**, choose **Use attribute**\.

## Use Contact Attributes to Route Contacts to a Specific Agent<a name="use-attribs-agent-queue"></a>

When you use contact attributes in a contact flow to route calls to an agent, the attribute value must be either the agent's user name, or the agent's user ID\.

To determine the user ID for an agent so that you can use the value as an attribute, use the [ListUsers](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListUsers.html) operation to retrieve the users from your instance\. The agent's user ID is returned with the results from the operation as the value of the `Id` in the [UserSummary](https://docs.aws.amazon.com/connect/latest/APIReference/API_UserSummary.html) object\.

You can also find the user ID for an agent by using [Amazon Connect Agent Event Streams](agent-event-streams.md)\. The agent events, which are included in the agent event data stream, include the agent ARN\. The user ID is included in the agent ARN after **`agent/`**\. 

In the following agent event data, the agent ID is **87654321\-4321\-4321\-4321\-123456789012**\.

```
{
    "AWSAccountId": "123456789012",
    "AgentARN": "arn:aws:connect:us-west-2:123456789012:instance/12345678-1234-1234-1234-123456789012/agent/87654321-4321-4321-4321-123456789012",
    "CurrentAgentSnapshot": {
        "AgentStatus": {
            "ARN": "arn:aws:connect:us-west-2:123456789012:instance/12345678-1234-1234-1234-123456789012/agent-state/76543210-7654-6543-8765-765432109876",
            "Name": "Available",
            "StartTimestamp": "2019-01-02T19:16:11.011Z"
        },
        "Configuration": {
            "AgentHierarchyGroups": null,
            "FirstName": "IAM",
            "LastName": "IAM",
            "RoutingProfile": {
                "ARN": "arn:aws:connect:us-west-2:123456789012:instance/12345678-1234-1234-1234-123456789012/routing-profile/aaaaaaaa-bbbb-cccc-dddd-111111111111",
                "DefaultOutboundQueue": {
                    "ARN": "arn:aws:connect:us-west-2:123456789012:instance/12345678-1234-1234-1234-123456789012/queue/aaaaaaaa-bbbb-cccc-dddd-222222222222",
                    "Name": "BasicQueue"
                },
                "InboundQueues": [{
                    "ARN": "arn:aws:connect:us-west-2:123456789012:instance/12345678-1234-1234-1234-123456789012/queue/aaaaaaaa-bbbb-cccc-dddd-222222222222",
                    "Name": "BasicQueue"
                }],
                "Name": "Basic Routing Profile"
            },
            "Username": "agentUserName"
        },
        "Contacts": []
},
```