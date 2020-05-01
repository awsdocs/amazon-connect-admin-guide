# How to Use System Metric Attributes<a name="attrib-system-metrics"></a>

Amazon Connect includes system metric attributes that can help you define routing conditions in your contact flows based on real\-time metrics about the queues and agents in your contact center\. When you include a **Get queue metrics** block in your contact flow, metrics are retrieved for the current working queue, or other queue that you specify, and returned as attributes that you can reference in blocks that occur after that block in the flow\.

You can reference the metric attributes returned to determine the optimal route for a contact\. Check the current queue metrics, such as the number of contacts or available agents in a queue, and how long the oldest contact has been in a queue\. You could even get metrics for multiple queues and use a **Set contact attributes** block to store the metric attributes for each queue\. You could then compare queue metric attributes using a **Check contact attributes** block, and route the contact to the queue with the fewest calls in it, or to a callback if all queues are busy\. To learn more about the metric attributes available, see [System Metrics Attributes](connect-attrib-list.md#attribs-system-metrics-table)\.

**To use system metrics attributes in a contact flow**

1. In Amazon Connect, choose **Routing**, **Contact flows**\.

1. Select an existing contact flow, or create a new one\.

1. Add a **Get queue metrics** block to the contact flow\.

1. Optionally, to specify a queue select the **Set queue** check box and do one of the following:
   + Select the queue to retrieve metrics for from the drop\-down list\.
   + Select **Use attribute**, then select the attribute to use\.

   If you do not select a queue, metrics are retrieved for the current working queue\.

1. Add a **Check contact attributes** block and connect the **Success** branch of the **Get queue metrics** block to it\.

1. Choose the title of the **Check contact attributes** block to display the properties for the block\.

1. Under **Attribute to check**, in the **Type** drop\-down menu, choose **Queue metrics**\. In the **Attribute** drop\-down menu, select the attribute to check\. 

1. To create a branching condition based on the value of the metric attribute, choose **Add another condition**\.

1. For the **Conditions to check**, choose the conditions to compare the attribute value to, and then enter a value in the **Value** field\.

1. Add additional blocks to the contact flow, connecting the branch of the **Check contact attributes** block to route the contact to the next block in the flow\.

1. Save and publish the contact flow to make it available in your contact center\.

## System Attributes for Contact Flows<a name="system-attributes"></a>

When creating a contact flow, use the following system attributes in Amazon Connect:
+ **Customer number**—The phone number of the customer\. When used in an outbound whisper flow, this is the number that the agents dialed to reach the customer\. When used in inbound flows, this is the number from which the customer placed the call\. This attribute is included in the CTRs and Lambda input object under CustomerEndpoint\.
+ **Dialed number**—The number that the customer dialed to reach your contact center\. This attribute is included in the CTRs and Lambda input under SystemEndpoint\.
+ **Customer callback number**—The number that the system uses to call the customer back, either for the **Transfer to callback** queue functionality, or for an agent dialing from the CCP\. The default value is the number that the customer used to call your contact center\. The value can be overwritten with the **Set callback number** block\. This attribute is not included in CTRs, and not accessible in Lambda input\. You can copy the attribute to a user\-defined attribute with the **Set contact attribute** block, which is included in CTRs\. You can also pass this attribute as a Lambda input parameter in an **Invoke AWS Lambda function** block, which is not included in CTRs\.
+ **Stored customer input**—The attribute values created from the most recent **Store customer input** block invocation\. This attribute is not included in CTRs, and is not accessible in Lambda input\. You can copy the attribute to a user\-defined attribute with the **Set contact attribute** block, which is included in CTRs\. You can also pass this attribute as a Lambda input parameter in an **Invoke AWS Lambda function** block, which is not included in CTRs\. This attribute value applies only to the most recent invocation of the Lambda function\. The value is overwritten with the next invocation of the function\.
+ **Queue name**—The name of the queue\.
+ **Queue ARN**—The ARN of the queue\.
+ **Queue outbound number**—The **Outbound caller ID number** selected for the queue\.
+ **Text to speech voice**—The Amazon Polly voice used for text to speech in a contact flow\.
+ **Contact id**—The unique identifier for the contact\.
+ **Initial contact id**—The unique identifier for the contact associated with the first interaction between the customer and your contact center\.
+ **Previous contact id**—The unique identifier for the leg of the contact that occurred before the current contact\.
+ **Channel**—The method used to contact your contact center, either VOICE or CHAT\. 
+ **Instance ARN**—The ARN for your Amazon Connect instance\.
+ **Initiation method**—Indicates how the contact was initiated\. Valid values include: INBOUND, OUTBOUND, TRANSFER, CALLBACK, API, and QUEUE\_TRANSFER\.