# Flow block: Set working queue<a name="set-working-queue"></a>

## Description<a name="set-working-queue-description"></a>
+ This block specifies the queue to be used when **Transfer to queue** is invoked\.
+ A queue must be specified before invoking **Transfer to queue** except when used in a customer queue flow\. It's also the default queue for checking attributes, such as staffing, queue status, and hours of operation\.

## Supported channels<a name="set-working-queue-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | Yes | 
| Task | Yes | 

## Flow types<a name="set-working-queue-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Properties<a name="set-working-queue-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-working-queue-properties.png)

Note the following properties:
+ **By queue > Set dynamically**\. To set the queue dynamically, you must specify the Amazon Resource Name \(ARN\) for the queue rather than the queue name\. To find the ARN for a queue, open the queue in the queue editor\. The ARN is included as the last part of the URL displayed in the browser address bar after /queue\. For example, `.../queue/aaaaaaaa-bbbb-cccc-dddd-111111111111`\.

## Configured block<a name="set-working-queue-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-working-queue-configured.png)

## Sample flows<a name="set-working-queue-samples"></a>

See these sample flows for scenarios that use this block:
+ [Sample queue customer](sample-queue-customer.md)
+ [Sample queue configurations](sample-queue-configurations.md)

## Scenarios<a name="set-working-queue-scenarios"></a>

See these topics for scenarios that use this block:
+ [Set up agent\-to\-agent transfers](setup-agent-to-agent-transfers.md)
+ [Transfer contacts to a specific agent](transfer-to-agent.md)