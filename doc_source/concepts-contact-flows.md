# Contact Flows<a name="concepts-contact-flows"></a>

A contact flow defines how a customer experiences your contact center from start to finish\. At the most basic level, contact flows enable you to customize your IVR \(interactive voice response\) system\. 

For example, you can give customers a set of menu options and route customers to agents based on what they enter on their phone\. Although with Amazon Connect, contact flows are significantly more powerful than that: you can create dynamic, personalized flows that interact with other AWS services\.

## Default Contact Flows<a name="concepts-default-flows"></a>

When you create an instance and claim a number, you automatically have a working contact center in just 5 minutes\. This is because Amazon Connect includes a set of default contact flows that have already been published\. It uses them to power your contact center\. 

When you customize your contact center and create new flows, you're replacing the default contact flows with your own\.

For example, say you create a contact flow that includes putting the customer on hold\.
+ You can create a prompt to play while the customer is on hold, such as "Do your holiday shopping early this year\. We're offering free shipping in November\." And then play some music\.
+ If you don't create a prompt, Amazon Connect will play the **Default customer hold** contact flow automatically\.

To see the list of default flows in the Amazon Connect console, go to **Routing**, **Contact Flows**\. They all start with **Default** in their name\. 

## Contact Flow Designer<a name="concepts-visual-editor"></a>

To customize your contact center, you use the contact flow designer\. It's a drag\-and\-drop interface that allows you to customize your contact center without any coding\.

### Contact Blocks<a name="concepts-contact-blocks"></a>

Contact blocks are the building blocks of your contact flows\. Each block is designed for a specific function a business might want in a contact center\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/sample-contact-flow.png)

The above contact flow uses five blocks:
+ **Set working queue**\. When the contact comes in, this block assigns it to the BasicQueue\.
+ **Check hours of operation**\. This block checks whether the contact has arrived when the queue is operating\.
+ **Transfer to queue**\. This block transfers the contact to the BasicQueue\.
+ **Play prompt**\. If the queue is not open for business, or there's an error or it's at capacity, this block plays a message "We are not able to take your call right now\."
+ **Disconnect/hang up**\. Every flow ends with this block\.

In the above example, what happens when the customer is transferred to queue, but no agents are available to take their call? The **Default customer queue** flow is triggered\. It plays music while the contact is waiting in queue\. 

For a list of the available contact blocks and descriptions about what they do, see [Contact Block Definitions](contact-blocks.md)\. 

### Sample Contact Flows<a name="concepts-sample-flows"></a>

To see how to put contact blocks together to create different flows, see [Sample Contact Flows](contact-flow-samples.md)\.