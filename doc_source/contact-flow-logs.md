# Contact Flow Logs<a name="contact-flow-logs"></a>

Amazon Connect contact flow logs provide you with real\-time details about events in your contact flows as customers interact with them\. You can use contact flow logs to help debug your contact flows as you are creating them\. After you publish your contact flows, you can view the logs to gain insight into what happens during complex contact flows, and quickly identify errors that your customers encounter when they connect to your contact center\. If needed, you can always roll back to a previous version of a contact flow\.

Contact flow logs are stored in Amazon CloudWatch, in the same region as your Amazon Connect instance\. A log entry added as each block in your contact flow is triggered\. You can configure CloudWatch to send alerts when unexpected events occur during active contact flows\. As a contact center manager, you can aggregate data from contact flow logs to analyze performance of contact flows to optimize the experience you provide for your customers\. For more information about CloudWatch Logs, see the [Amazon CloudWatch Logs User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/)\.

## Enabling Contact Flow Logs<a name="contact-flow-log-entries"></a>

To start generating contact flow logs, enable contact flow logs for your Amazon Connect instance\. After you enable logs for your instance, logs are generated only for contact flows that include a **Set logging behavior** block with logging set to enabled\. You can control which flows, or parts of flows, logs are generated for by including multiple **Set logging behavior** blocks and setting logging to enabled or disabled as desired\. When you use a **Set logging behavior** block to enable or disable logging for a flow, logging is also enabled or disabled for any subsequent flow that a contact is transferred to, even if the flow does not include a **Set logging behavior** block\. To avoid having logging settings persist between flows, you should include a **Set logging behavior** block in the flow with logging enabled or disabled as desired for that specific flow\.

When you create a new Amazon Connect instance, you can enable Contact flow logs when you configure Data Storage settings\. If you already have an Amazon Connect instance, you can enable or disable Contact flow logs for your instance in the Amazon Connect console under **Contact flow** settings\. You are not charged for generating contact flow logs, but are charged for using CloudWatch for generating and storing the logs\. Free tier customers are charged only for usage that exceeds service quotas\. For details about Amazon CloudWatch pricing, see [Amazon CloudWatch Pricing](https://aws.amazon.com/cloudwatch/pricing/)\.

**To enable contact flow logs for your Amazon Connect instance**

1. Open the Amazon Connect console\.

1. Choose the instance alias for the instance for which to enable contact flow logs\.

1. Choose **Contact flows**\.

1. Select **Enable Contact flow logs** and choose **Apply**\.

After you enable contact flow logs for your instance, you can enable logging for a flow by adding a **Set logging behavior** block\.

**To enable or disable contact flow logs for a contact flow**

1. Add a **Set logging behavior** block and connect it to another block in the flow\.

1. Open the settings for the block, and under **Logging behavior** do one of the following:

   Select **Enable** to turn on logging for the flow\.

   Select **Disable** to turn off logging for the flow\.

1. Choose **Save**\.

1. If you add a **Set logging behavior** block to a contact flow that is already published, you must publish it again to start generating logs for it\.

## Data Captured in Contact Flow Logs<a name="contact-flow-log-data"></a>

Log entries for contact flows include details about the block associated with the log entry, the contact ID, and the action taken after the steps in the block were completed\. Any contact interaction that occurs outside of the contact flow is not logged, such as time spent in a queue or interactions with an agent\. You can control which data is captured in contact flow logs by including a **Set logging behavior** block in your contact flow\. You can set the properties of the block to disable logging during the parts of your contact flow that interact with or capture sensitive data or customers’ personal information\.

If you use Amazon Lex or AWS Lambda in your contact flows, the logs show the entry and exit of the contact flow going to them, and include any information about the interaction that is sent or received during entry or exit\.

Because the logs also include the contact flow ID, and the contact flow ID stays the same when you change a contact flow, you can use the logs to compare the interactions with different versions of the contact flow\.

The following example log entry shows a Set queue block of a customer queue flow\.

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

## Tracking Customers Between Contact Flows<a name="contact-flow-log-multiple-flows"></a>

In many cases, customers interact with multiple contact flows in your contact center, being passed from one contact flow to another to appropriately assist them with their specific issue\. Contact flow logs help you track customers between different contact flows, by including the ID of the contact in each log entry\. When a customer is transferred to a different contact flow, the ID for the contact associated with their interaction is included with the log for the new flow\. You can query the logs for the contact ID to trace the customer interaction through each contact flow\. In larger, high\-volume contact centers, there can be multiple streams for contact flow logs\. If a contact is transferred to a different contact flow, the log may be in a different stream\. To make sure that you are finding all of the log data for a specific contact, you should search for the contact ID in the entire CloudWatch log group instead of in a specific log stream\.

## Create Alerts for Contact Flow Log Events<a name="contact-flow-log-alerts"></a>

You can configure CloudWatch to define a filter pattern that looks for specific events in your contact flow logs and then creates an alert when an entry for that event is added to the log\. For example, you can set an alert for when a contact flow block goes down an error path as a customer interacts with the flow\. Log entries are typically available in CloudWatch within a short time, giving you near real\-time notification of events in contact flows\.

## Analyzing Contact Flow Logs with Amazon Kinesis<a name="contact-flow-log-kinesis"></a>

To perform analysis on your contact flow logs, you can set up an Amazon Kinesis stream to stream your contact flow log data from CloudWatch to a data warehouse service, such as Amazon Redshift\. You can combine the contact flow log data with other Amazon Connect data in your warehouse, or run queries to identify trends or common issues with a contact flow\.