# Call Back Customers<a name="call-back"></a>

You can create contact flows that provide the ability for customers to leave their phone number and get a call back\. \(For an example contact flow, see the Sample queued callback template\.\) When a customer leaves their number it's put in a queue and then routed to the next available agent\.

To see the number of customers waiting for call backs, view the Real\-time metrics page: in Amazon Connect choose **Metrics and quality** > **Real\-time metrics** > **Queues**\. 

By default, customers who are waiting for a call back are counted in the In Queue metric, which counts all customers who are in a queue for an agent\. To only see a count of the customers waiting for a call back, you need to create a queue that only takes callback contacts\. To learn how to do this, see [Amazon Connect Queues](connect-queues.md)\.