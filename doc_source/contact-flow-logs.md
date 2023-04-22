# Enable flow logs<a name="contact-flow-logs"></a>

**Tip**  
Amazon Connect delivers flow logs at least once\. They may be delivered again for multiple reasons\. For example, a service retry due to an unavoidable failure\.

## Step 1: Enable logging for your instance<a name="enable-contact-flow-logs"></a>

By default when you create a new Amazon Connect instance, an Amazon CloudWatch log group is created automatically to store the logs for your instance\. 

Use the following procedure to check that logging is enabled for your instance\.

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. On the instances page, choose the instance alias\. The instance alias is also your **instance name**, which appears in your Amazon Connect URL\. The following image shows the **Amazon Connect virtual contact center instances** page, with a box a box around the instance alias\.  
![\[The Amazon Connect virtual contact center instances page, the instance alias.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/instance.png)

1. In the navigation pane, choose **Flows**\.

1. Select **Enable Flow logs** and choose **Save**\.

## Step 2: Add the Set logging behavior block<a name="use-set-logging-behavior-block"></a>

Logs are generated only for flows that include a [Set logging behavior](set-logging-behavior.md) block with logging set to enabled\. 

You control which flows, or parts of flows, logs are generated for by including multiple **Set logging behavior** blocks and configuring them as needed\.

When you use a **Set logging behavior** block to enable or disable logging for a flow, logging is also enabled or disabled for any subsequent flow that a contact is transferred to, even if the flow does not include a **Set logging behavior** block\. To avoid logging that persists between flows, enable or disable a **Set logging behavior** block as needed for that specific flow\.

**To enable or disable flow logs for a flow**

1. In the flow designer, add a [Set logging behavior](set-logging-behavior.md) block and connect it to another block in the flow\.

1. Open the properties for the block\. Choose **Enable** or **Disable**\.

1. Choose **Save**\.

1. If you add a **Set logging behavior** block to a flow that is already published, you must publish it again to start generating logs for it\.