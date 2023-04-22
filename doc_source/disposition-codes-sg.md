# Disposition codes<a name="disposition-codes-sg"></a>

A simple use case of step\-by\-step guides is to have an agent enter a disposition code at the end of the contact\. To give your agents the ability to set disposition codes at the end of a contact or complete other post\-call work, create a flow that has one [Show view](show-view-block.md) block and one [Set contact attributes](set-contact-attributes.md) block\. 
+ Use the [Show view](show-view-block.md) block to create a **Form** view that gives the agents the required input field\.
+ Use the [Set contact attributes](set-contact-attributes.md) block to save the response as contact attributes\.

 In addition, you can also use an [Invoke AWS Lambda function](invoke-lambda-function-block.md) block to send the entered data to an external system\.

After you've created your flow, you will be able to dynamically determine which one to surface at the end of a contact by setting the **DisconnectFlowForAgentUI** as a custom attribute in your contact flows\. As long as this attribute is set before a contact ends, the agent UI will surface this form after a contact ends\.

The following image shows the properties page for a [Set contact attributes](set-contact-attributes.md)\. It is configured to save the response in a user\-defined attribute\.

![\[The properties page of the Set contact attributes block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/dispo-codes-sq.png)