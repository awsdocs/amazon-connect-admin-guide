# Sample Customer Queue Priority<a name="sample-customer-queue-priority"></a>

Type: Contact flow \(inbound\)

This contact flow shows you two options for using the **Change routing priority/age ** block to adjust the priority of a customer in the queue\. You can change a customer's priority in the queue using priority or routing age\.

## Option 1: Raise the Priority<a name="option1-sample-customer-queue-priority"></a>

If the customer presses 1 in the **Get Customer Input **block, the following **Change routing priority/age** block changes the Queue priority value of the contact to 1\.

By default the priority for new contacts is 5\. Lower values raise the priority of the contact\. A contact assigned a priority of 1 is routed first\.

## Option 2: Change the Routing Age<a name="option2-sample-customer-queue-priority"></a>

If the customer presses 2 in the **Get Customer Input** block, the following **Change routing priority/age** block changes the routing age of the contact by increasing the routing age by 10 minutes\.

This change prioritizes the contact\. Because customers who have been queued longer are connected first, given that the contacts have the same queue priority value\.