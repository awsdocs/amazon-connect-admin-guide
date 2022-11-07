# What data is gathered in flow logs<a name="contact-flow-log-data"></a>

Log entries for flows include details about the block associated with the log entry, the contact ID, and the action taken after the steps in the block were completed\. Any contact interaction that occurs outside of the flow is not logged, such as time spent in a queue or interactions with an agent\. 

You can set the properties of the block to disable logging during the parts of your flow that interact with or capture sensitive data or customers’ personal information\.

If you use Amazon Lex or AWS Lambda in your flows, the logs show the entry and exit of the flow going to them, and include any information about the interaction that is sent or received during entry or exit\.

Because the logs also include the flow ID, and the flow ID stays the same when you change a flow, you can use the logs to compare the interactions with different versions of the flow\.

The following example log entry shows a **Set working queue** block of an inbound flow\.

```
{
    "ContactId": "11111111-2222-3333-4444-555555555555",
    "ContactFlowId": "arn:aws:connect:us-west-2:0123456789012:instance/nnnnnnnnnnn-3333-4444-5555-111111111111/contact-flow/123456789000-aaaa-bbbbbbbbb-cccccccccccc",
    "ContactFlowModuleType": "SetQueue",
    "Timestamp": "2021-04-13T00:14:31.581Z",
    "Parameters": {
        "Queue": "arn:aws:connect:us-west-2:0123456789012:instance/nnnnnnnnnnn-3333-4444-5555-111111111111/queue/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"
    }
}
```