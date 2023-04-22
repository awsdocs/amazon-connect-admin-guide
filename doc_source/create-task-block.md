# Flow block: Create task<a name="create-task-block"></a>

## Description<a name="create-task-description"></a>
+ Creates a new task manually or by leveraging a [task template](task-templates.md)\. 
+ Sets the tasks attributes\.
+ Initiates a flow to start the task immediately or schedules it for a future date and time\.

For more information about Amazon Connect Tasks, see [Concepts: Tasks in Amazon Connect](tasks.md)\. 

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

When you configure a **Create task** block, you choose either **Create manually** or **Use template**\. Your choice dictates which fields you'll need to complete on the rest of **Properties** page\. Following is more information about these two options\.

### Option 1: Create manually<a name="create-manually"></a>

The following image shows the **Properties** page when **Create manually** is selected\. All settings on the page can be specified manually or dynamically\.

![\[The properties page of the Create task block, the Create manually option.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/create-task-properties-manually.png)

If you choose **Use template** at bottom of the page, the entire page switches to that option\. If needed, you can toggle back to **Create manually** and continue with your manual settings\.

### Option 2: Use template<a name="use-template"></a>

After you [create a template](task-templates.md), it's available for you to specify it in **Create task** block\.

The following image shows the **Properties** page when **Use template** is selected\. In this example, the name of the template is **Test Template**\. Notice that **Test Template** does not include a flow\. 
+ If the selected template does not include a flow, you must specify the flow that you want the task to run\.
+ You cannot overwrite the settings of any fields on the page that are populated by the template\.

![\[The Properties page, the Use template option.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/create-task-properties-template.png)

## Configuration tips<a name="create-task-tips"></a>
+ The **Create task** block branches based on whether the task was successfully created:
  + **Success** if task was created\. It responds with the contact ID of the newly created task\.
  + **Error** if task wasn't created\.
+ **Referencing a task contact ID**: The newly created task runs the flow that you specified in the **Flow** section of the block, or it runs the flow configured by the task template that you selected\. You can reference the contact ID of the newly created task in subsequent blocks\. 

  For example, you might want to reference the task contact ID in the **Play prompt** block\. You can specify the task contact ID dynamically by using the following attribute:
  + **Namespace: System**
  + **Value: Task Contact id**
+ **Scheduling a task**: When you **Set date and time using attribute**: Values for date fields must be in Unix timestamp \(Epoch seconds\)\. Because of this, it's most likely that you'll choose a **User\-defined** attribute for the **Namespace**\. 

  For example, your flow might have a **Set contact attributes** block that sets a user\-defined attribute with key named *scheduledTaskTime*\. Then, in the **Create task** block, you would select **User\-defined**, and the key would be *scheduledTaskTime*\.

  To continue with this example, the value in *scheduledTaskTime* must be specified Unix timestamp\. For example, 1679609303 is the Unix timestamp that corresponds to Thursday, March 23, 2023 10:08:23 PM UTC\.

  When the date and time have passed, contacts are always routed down the **Error** branch\. To avoid the **Error** branch, be sure to keep the Epoch seconds updated to a valid date and time in the future\. 
+ Be sure to check the [service quotas](amazon-connect-service-limits.md) for tasks and API throttling, and request increases, if needed\. The quotas apply when this block creates tasks\.

## Configured block<a name="create-task-configured"></a>

The following image shows an example of what this block looks like when it is configured\. It has two branches: **Success** and **Error**\. 

![\[A configured Create task block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/create-task-configured.png)

## Sample flows<a name="create-task-samples"></a>

Amazon Connect includes a set of sample flows\. For instructions that explain how to access the sample flows in the flow designer, see [Sample flows](contact-flow-samples.md)\. Following are topics that describe the sample flows which include this block\.
+ [Sample inbound flow \(first contact experience\)](sample-inbound-flow.md)