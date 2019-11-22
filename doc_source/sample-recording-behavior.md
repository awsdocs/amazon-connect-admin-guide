# Sample Recording Behavior<a name="sample-recording-behavior"></a>

Type: Contact flow \(inbound\)

This contact flow shows how you can change recording behavior based on user input\. It also shows that you can:
+ Configure the recording for the agent only\.
+ Configure the recording for the customer only\.
+ Configure the recording for both the customer and agent\.
+ Choose to not have a recording\.

It starts by checking the channel of the customer\. If the customer is using chat, they get a prompt that the **Set recording block** doesn't apply to chats\. [Learn more](set-up-recordings.md)\.

If the contact is using voice, a **Get customer input** block prompts them to enter the number for who they want to record\. Their entry triggers the **Set recording behavior** block with the appropriate configuration\.

It ends with the customer being transferred by to the [Sample Inbound Flow](sample-inbound-flow.md)\. 