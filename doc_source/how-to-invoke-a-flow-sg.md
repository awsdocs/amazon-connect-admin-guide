# How to invoke a flow at the start of a contact \(Preview\)<a name="how-to-invoke-a-flow-sg"></a>


|  | 
| --- |
| This is prerelease documentation for a service in preview release\. It is subject to change\. | 

After you’ve created your flows, you will be able to dynamically determine which ones to surface when by setting the **DefaultFlowForAgentUI** as a custom attribute in your contact flows\. As long as this attribute is set before a contact gets routed to a queue, the agent UI will show this flow once the agent accepts the contact\.

For example, by checking the IVR responses, Queue Name, and Customer info you can create branching logic in flows that determines which flow id to set\. Just use the Check attribute block to set your conditional logic and the set attribute block to set the flow you want to send to your agent\.

*Example Flow Id*

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/example-flow-id-sq.png)