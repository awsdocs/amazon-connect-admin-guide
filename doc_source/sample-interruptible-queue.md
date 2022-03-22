# Sample interruptible queue flow with callback<a name="sample-interruptible-queue"></a>

**Note**  
This topic explains a sample contact flow that is included with Amazon Connect\. For information about locating the sample flows in your instance, see [Sample contact flows](contact-flow-samples.md)\. 

Type: Customer queue

This contact flow shows you how to manage what the customer experiences while in queue\. It uses **Check contact attributes** to determine if the customer is contacting you by phone or chat, and to route them accordingly\.

If the channel is chat, the customer is transferred to the **Loop prompts**\.

If the channel is voice, the customer hears a looping audio that interrupts every 30 seconds to give them two options from the **Get customer input** block:

1. The customer can press 1 to enter a callback number\. Then the **Get customer input** block prompts the customer for their phone number\. Then the flow ends\. 

1. Press 2 ends the flow, and the customer remains in the queue\.