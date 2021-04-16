# Sample recording behavior<a name="sample-recording-behavior"></a>

Type: Contact flow \(inbound\)

This contact flow starts by checking the channel of the customer:
+ If the customer is using chat, they get a prompt that the **Set recording block** enables managers to monitor chat conversations\. \(To *record* chats, you only need to specify an Amazon S3 bucket where the conversation will be stored\.\)

  To monitor chats, the **Set recording block** is configured to record both the **Agent and Customer**\.
+ If the contact is using voice, a **Get customer input** block prompts them to enter the number for who they want to record\. Their entry triggers the **Set recording behavior** block with the appropriate configuration\.

It ends with the customer being transferred by to the [Sample inbound flow](sample-inbound-flow.md)\. 

For more information, see the following topics:
+ [Set up recording behavior](set-up-recordings.md)
+ [Monitor live conversations](monitor-conversations.md)
+ [Review recorded conversations](review-recorded-conversations.md)