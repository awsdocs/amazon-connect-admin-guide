# What data is gathered in contact flow logs<a name="contact-flow-log-data"></a>

Log entries for contact flows include details about the block associated with the log entry, the contact ID, and the action taken after the steps in the block were completed\. Any contact interaction that occurs outside of the contact flow is not logged, such as time spent in a queue or interactions with an agent\. 

You can set the properties of the block to disable logging during the parts of your contact flow that interact with or capture sensitive data or customers’ personal information\.

If you use Amazon Lex or AWS Lambda in your contact flows, the logs show the entry and exit of the contact flow going to them, and include any information about the interaction that is sent or received during entry or exit\.

Because the logs also include the contact flow ID, and the contact flow ID stays the same when you change a contact flow, you can use the logs to compare the interactions with different versions of the contact flow\.

The following example log entry shows a **Set working queue** block of a customer queue flow\.

```
{
    "Timestamp": "2017-11-09T12:17.898Z",
    "ContactId": "f0b21968-952b-47ba-b764-f29a57bcf626",
    "ContactFlowId": "arn:aws:connect:us-east-2:0123456789012:instance/d-92673ef055/contact-flow/b1d791cf-1264-42e3-9a73-62cbcb3c9a45",
    "ContactFlowModuleType": "SetQueue",
    "Events": {
        "Queue": [
            "arn:aws:connect:us-east-2:670047220557:instance/d-92673ef044/queue/f0300e43-9547-477c-b8ba-0bb7a72f7fa1"
        ]
    }
}
```