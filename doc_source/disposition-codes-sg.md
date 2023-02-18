# Disposition codes \(Preview\)<a name="disposition-codes-sg"></a>


|  | 
| --- |
| This is prerelease documentation for a service in preview release\. It is subject to change\. | 

A simple use case of step\-by\-step guides is to have an agent enter a disposition code at the end of the contact\. To give your agents the ability to set disposition codes at the end of a contact or complete other post\-call work, you can create a flow that has one Show View block and one Set Attributes block\. You can use the Show View block to create a **Form** view that gives the agents the required input field, and then you can use the **Set contact attributes** block to save the response as contact attributes\. In addition, you can also use a Lambda flow block to send the entered data to an external system\.

After you’ve created your flow, you will be able to dynamically determine which one to surface at the end of a contact by setting the **DisconnectFlowForAgentUI** as a custom attribute in your contact flows\. As long as this attribute is set before a contact ends, the agent UI will surface this form once a contact ends\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/dispo-codes-sq.png)