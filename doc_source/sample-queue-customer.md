# Sample queue customer<a name="sample-queue-customer"></a>

**Note**  
This topic explains a sample flow that is included with Amazon Connect\. For information about locating the sample flows in your instance, see [Sample flows](contact-flow-samples.md)\. 

Type: Flow \(inbound\)

This flow performs checks before placing customer into a queue\. Here's how it works:

1. The **Set working queue** block determines which queue to transfer the customer to\.

1. The **Check hours of operation** block perform checks to avoid the customer being queued during non\-working hours\.

1. The customer is transferred to the queue if it is within business hours, and the queue can handle this call\. Otherwise, the customer is played a message "We are not able to take your call right now\. Goodbye\." And then the customer is disconnected\.