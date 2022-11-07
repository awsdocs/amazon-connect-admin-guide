# Amazon Connect Flows<a name="concepts-contact-flows"></a>

A *flow* defines how a customer experiences your contact center from start to finish\. At the most basic level, flows enable you to customize your IVR \(interactive voice response\) system\. 

For example, you can give customers a set of menu options and route customers to agents based on what they enter on their phone\. Although with Amazon Connect, flows are significantly more powerful than that: you can create dynamic, personalized flows that interact with other AWS services\.

## Default flows<a name="concepts-default-flows"></a>

When you create an instance and claim a number, you automatically have a working contact center in just 5 minutes\. This is because Amazon Connect includes a set of default flows that have already been published\. It uses them to power your contact center\. 

When you customize your contact center and create new flows, you're replacing the default flows with your own\.

For example, say you create a flow that includes putting the customer on hold\.
+ You can create a prompt to play while the customer is on hold, such as "Do your holiday shopping early this year\. We're offering free shipping in November\." And then play some music\.
+ If you don't create a prompt, Amazon Connect will play the **Default customer hold** flow automatically\.

To see the list of default flows in the Amazon Connect console, go to **Routing**, **Flows**\. They all start with **Default** in their name\. 

For a list of all the default flows and what they do, see [Default flows](contact-flow-default.md)\.

## Flow designer<a name="concepts-visual-editor"></a>

To customize your contact center, you use the flow designer\. It's a drag\-and\-drop interface that allows you to customize your contact center without any coding\.

### Flow blocks<a name="concepts-contact-blocks"></a>

Flow blocks are the building blocks of your flows\. Each block is designed for a specific function a business might want in a contact center\. 

You configure a flow block by accessing its **Properties** page, as shown in the following GIF\. 

![\[\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/Sidepanel.gif)

For a list of the available flow blocks and descriptions about what they do, see [Flow block definitions](contact-block-definitions.md)\. 

### Sample flows<a name="concepts-sample-flows"></a>

To see how to put flow blocks together to create different flows, see [Sample flows](contact-flow-samples.md)\.