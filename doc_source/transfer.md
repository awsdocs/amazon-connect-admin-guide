# Set up contact transfers<a name="transfer"></a>

To make it easy for you to set up contact transfers, Amazon Connect provides you with several tools: 
+ Two contact flow types:
  + Transfer to agent: Enables transfers to another agent\. This works with voice contacts\. 
  + Transfer to queue: Enables transfers to a queue\. This works with both voice and chat contacts\.
+ Contact blocks:
  + [Transfer to queue](transfer-to-queue.md): Use to end the current contact flow and place the customer in a queue\. This block works for both voice and chat transfers\. 
  + [Transfer to phone number](transfer-to-phone-number.md): Use to transfer the customer to a phone number, such as an external number\. This block works for voice transfers\.
  + [Transfer to flow](transfer-to-flow.md): Use to end the current flow and transfer the customer to another contact flow\. This block works for voice transfers\.
+ Quick connects: Use to create common destinations for transfers\. Agents will see them as options in the CCP when they go to do a transfer\.

This topic explains how to create quick connects and use transfer contact blocks in specific scenarios\. 

## Overview of steps<a name="transfer-overview"></a>

**To set up call transfers and quick connects**

1. Choose a contact flow type based on what you want to do: Transfer to agent or Transfer to queue\. External transfers do not require a specific type of contact flow\.

1. Create and publish the contact flow\. 

1. Create a quick connect for the type of transfer to enable: **Agent**, **Queue**, or **External**\.

   When you create the **Agent** or **Queue** quick connect, select a contact flow that matches the type of transfer to enable\. **External** quick connects require only a phone number, and do not allow you to set a queue or contact flow\.

1. Add the quick connect that you created to any queue used in a contact flow for which to enable contact transfer, such as the queue used in the contact flow for incoming contacts\.

1. Make sure the queue is in a routing profile assigned to the agents who transfers contacts\. 