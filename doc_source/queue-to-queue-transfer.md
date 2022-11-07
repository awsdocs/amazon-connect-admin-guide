# Manage contacts in a queue<a name="queue-to-queue-transfer"></a>

For inbound contacts, you can define advanced routing decisions to minimize queue wait times, or route contacts to specific queues, using blocks in your flow\. For example: 
+ Use a **Check queue status** block to check staffing or agent availability for a queue before sending a contact to that queue\.
+ Or, use a **Get queue metrics** block to retrieve queue metrics\.
+ Then use a **Check contact attributes** block to check specific queue metric attributes, and define conditions to determine which queue to route the contact to based on attribute values\. For more information about using queue metrics, see [Route based on number of contacts in a queue](attrib-system-metrics.md)\.

After determining which queue to transfer the contact to, use a **Transfer to queue** block in a flow to transfer the contact to that queue\. When the **Transfer to queue** block runs, it checks the queue capacity to determine whether or not the queue is at capacity \(full\)\. This check for queue capacity compares the current number of contacts in the queue to the [Maximum contacts in queue](set-maximum-queue-limit.md) limit, if one is set for the queue\. If no limit is set, the queue is limited to the number of concurrent contacts set in the [service quota](amazon-connect-service-limits.md) for the instance\.

After the contact is placed in a queue, the contact remains there until an agent takes the contact, or until the contact is handled based on the routing decisions in your customer queue flow\. 

To change the queue associated with the call after it is already placed in a queue, use a **Loop prompts** block with a **Transfer to queue** block in a customer queue flow\. In the block choose which queue to transfer the call to, or use an attribute to set the queue\.

**To manage contacts in a queue using a Transfer to queue block**

1. In Amazon Connect, on the navigation menu choose **Routing**, **Flows**\.

1. Choose the down arrow next to **Create flow**, then choose **Create customer queue flow**\.

1. Under **Interact**, add a **Loop prompts** block to provide a message to the caller when the call is transferred, then every X seconds or minutes while the call is in the queue\.

1. Select the **Loop prompts** block to display the settings for the block\.

1. Choose **Add another prompt to the loop**\.

1. Under **Prompts**, do one of the following:
   + Choose **Audio recording** in the drop\-down menu, then select the audio recording to use as the prompt\.
   + Choose **Text to Speech** in the drop\-down menu, then enter text to use for the prompt in the **Enter text to be spoken** field\.

1. To set an interrupt, choose **Interrupt every**, enter a value for the interrupt interval, and then choose a unit, either **Minutes** or **Seconds**\. We recommend that you use an interval greater than 20 seconds to ensure that queued contacts that are being connected to an agent are not interrupted\.

1. Choose **Save**\.

1. Connect the block to the **Entry point** block in the contact flow\.

1. Under **Terminate/Transfer**, drag a **Transfer to queue** block onto the designer\.

1. Select the title of the block to display the settings for the block, then choose the **Transfer to queue** tab\.

1. Under **Queue to check**, choose **Select a queue**, then select the queue to transfer calls to\.

   Alternatively, choose **Set dynamically**, then reference an attribute to specify the queue\. If you use an attribute to set the queue, the value must be the queue ARN\.

1. Choose **Save**\.

1. Connect the **Loop prompt** block to the **Transfer to queue** block\.

1. Add additional blocks to complete the flow that you require, such as the blocks to check queue status or metrics, then choose **Save**\.

   The flow is not active until you publish it\.

**Important**  
To successfully complete the call transfer to another queue, you must include a block after the **Transfer to queue** block and connect the **Success** branch to it\. For example, use an **End flow / Resume** block to end the flow\. The flow does not end until the call is picked up by an agent\.