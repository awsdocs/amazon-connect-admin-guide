# How to invoke a flow at the start of a contact<a name="how-to-invoke-a-flow-sg"></a>

After you've created your flows, you will be able to dynamically determine which ones to surface when by setting the **DefaultFlowForAgentUI** as a custom attribute in your contact flows\. As long as this attribute is set before a contact gets routed to a queue, the agent UI will show this flow after the agent accepts the contact\.

For example, by checking the IVR responses, Queue Name, and Customer info you can create branching logic in flows that determines which flow ID to set\. Use the **Check attribute** block to set your conditional logic and the set attribute block to set the flow you want to send to your agent\.

The following image shows the **Properties** page for the **Set contact attributes** block\. **Namespace** is set to **User defined**, **Value** is set to **DefaultFlowForAgentUI**\. The **Set manually** option is selected\.

![\[The properties page of the Set contact attributes block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/example-flow-id-sq.png)