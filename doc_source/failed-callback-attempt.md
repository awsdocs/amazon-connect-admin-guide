# What counts as a "Failed Callback Attempt"<a name="failed-callback-attempt"></a>

If an agent doesn't accept an offered callback, it doesn't count as an failed callback attempt\. Rather, the routing engine offers the callback to the next available agent, until an agent accepts\. 

A failed callback attempt would be along the lines of: an agent accepts a callback but then something goes wrong between then and the agent being joined to the customer\.

The contact is considered to be in the callback queue until an agent accepts the offered callback contact\.

Amazon Connect removes the callback from the queue when it's connected to the agent\. At that time, Amazon Connect starts dialing the customer\. The following image shows what this looks like in a contact record:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ctr-enqueue-and-dequeue.png)

The enqueued time on the contact record for a particular callback leg corresponds to the amount of time that the contact was in queue before that particular callback attempt was made\. This is not the total enqueued time across all contact records\. 

For example, an inbound call could be in queue for 5 minutes before a callback is scheduled\. Then, after an initial delay of 10 seconds, the callback contact could be in a callback queue for 10 seconds before an agent accepts it\. In this case, you would see two contact records:

1. The first contact record, with InitiationMethod=INBOUND, would have an enqueued time of 5 minutes\.

1. The second contact record, with InitiationMethod=CALLBACK, would have an enqueued time of 10 seconds\.