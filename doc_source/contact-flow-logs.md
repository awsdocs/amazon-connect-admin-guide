# Enable contact flow logs<a name="contact-flow-logs"></a>

## Step 1: Enable logging for your instance<a name="enable-contact-flow-logs"></a>

By default when you create a new Amazon Connect instance, Amazon Connect creates an Amazon S3 bucket for storing contact flow logs\. When a bucket is created, contact flow logging is enabled at the instance level\.

Use the following procedure to check that logging is enabled for your instance\.

1. Open the Amazon Connect console\.

1. Choose the instance alias for your instance\.

1. Choose **Contact flows**\.

1. Scroll to bottom of the page\. Select **Enable Contact flow logs** and choose **Apply**\.

## Step 2: Add the Set logging behavior block<a name="use-set-logging-behavior-block"></a>

Logs are generated only for contact flows that include a [Set logging behavior](set-logging-behavior.md) block with logging set to enabled\. 

You control which flows, or parts of flows, logs are generated for by including multiple **Set logging behavior** blocks and configuring them as needed\.

When you use a **Set logging behavior** block to enable or disable logging for a flow, logging is also enabled or disabled for any subsequent flow that a contact is transferred to, even if the flow does not include a **Set logging behavior** block\. To avoid logging that persists between flows, enable or disable a **Set logging behavior** block as needed for that specific flow\.

**To enable or disable contact flow logs for a contact flow**

1. Add a [Set logging behavior](set-logging-behavior.md) block and connect it to another block in the flow\.

1. Open the properties for the block\. Choose **Enable** or **Disable**\.

1. Choose **Save**\.

1. If you add a **Set logging behavior** block to a contact flow that is already published, you must publish it again to start generating logs for it\.