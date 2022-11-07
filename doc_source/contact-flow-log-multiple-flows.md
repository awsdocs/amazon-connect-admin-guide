# Track customers between flows<a name="contact-flow-log-multiple-flows"></a>

In many cases, customers interact with multiple flows in your contact center, being passed from one flow to another to appropriately assist them with their specific issue\. Flow logs help you track customers between different flows, by including the ID of the contact in each log entry\. 

When a customer is transferred to a different flow, the ID for the contact associated with their interaction is included with the log for the new flow\. You can query the logs for the contact ID to trace the customer interaction through each flow\. 

In larger, high\-volume contact centers, there can be multiple streams for flow logs\. If a contact is transferred to a different flow, the log may be in a different stream\. To make sure that you are finding all of the log data for a specific contact, you should search for the contact ID in the entire CloudWatch log group instead of in a specific log stream\.