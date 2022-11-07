# Flow block: Create task<a name="create-task-block"></a>

## Description<a name="create-task-description"></a>

Creates a new task, sets the tasks attributes, and initiates a flow to start the task immediately or schedule it for a future date and time\. For more information about Amazon Connect Tasks, see [Tasks](tasks.md)\. 

**Note**  
If your Amazon Connect instance was created on or before October 2018, the contact is routed down the error branch\. For the contact to be routed down the success path, create an IAM policy with the following permission and attach it to the Amazon Connect service role\. You can find the Amazon Connect service role on the **Account overview** page for your Amazon Connect instance\.  

```
{
     "Effect": "Allow",
     "Action": "connect:StartTaskContact",
     "Resource": "*"
}
```

## Supported channels<a name="create-task-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | Yes | 
| Task | Yes | 

## Flow types<a name="create-task-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ All flows

## Properties<a name="create-task-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/create-task-properties1.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/create-task-properties2.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/create-task-properties3.png)

## Configuration tips<a name="create-task-tips"></a>
+ The **Create task** block branches based on whether the task was successfully created:
  + **Success** if task was created\. It responds with the contact ID of the newly created task\.
  + **Error** if task wasn't created\.
+ The newly created task runs the flow that you specified in the **Flow** section of the block\. You can reference the contact ID of the newly created task in subsequent blocks\. 

  For example, you might want to reference the task contact ID in the **Play prompt** block\. You can specify the task contact ID dynamically by using the following attribute:
  + **Type: System**
  + **Attribute: Task Contact id**
+ To create a scheduled task, we recommend that in the **Schedule task** section, you use **Set a delay**\. Provide a value that is persistently valid and doesn't become outdated\. 

  You can **Set a delay** manually or use attributes\.

  If there are cases where **Set date and time using attribute** is needed, you specify an actual date and time in Epoch seconds\. When the date and time have passed, contacts are always routed down the **Error** branch\. To avoid the **Error** branch, be sure to keep the Epoch seconds updated to a valid date and time in the future\.
+ Be sure to check the [service quotas](amazon-connect-service-limits.md) for tasks and API throttling, and request increases, if needed\. The quotas apply when this block creates tasks\.

## Configured block<a name="create-task-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/create-task-configured.png)

## Sample flows<a name="create-task-samples"></a>

See these sample flows for scenarios that use this block:
+ [Sample inbound flow \(first contact experience\)](sample-inbound-flow.md)