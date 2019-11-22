# Sample Queue Configurations<a name="sample-queue-configurations"></a>

Type: Contact flow \(inbound\)

This contact flow shows different ways you can put a customer in queue: you can change the priority of the customer, determine the wait time in queue, and give them an option for a callback\. Here's how it works: 

1. The customer is put in a basic queue\.

1. After that, the **Default customer queue** flow is invoked\.

1. The hours of operation are checked\.

1. The channel is checked:
   + If chat, we check the time in queue\. If it's less than 5 minutes, the customer is placed in queue for an agent\. If it's more, we check the channel again and if it's chat, put the customer in queue for an agent\. 
   + If voice, we give the customer the option to press 1 to move to the front of the queue or 2 to move to the end of the queue\. This is so you can see how to use the **Change routing priority / age** block to move a contact to the front or back\. 

1. Next, we check the time in queue again, and then check the channel\. If the customer is using voice, we use the **Get customer input** block to ask if they want a callback or wait in queue\. 

1. We use a **Store customer input** block to get the customer's phone number, and a **Set callback number** block to store it\.