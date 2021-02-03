# Sample inbound flow \(first contact experience\)<a name="sample-inbound-flow"></a>

Type: Contact flow \(inbound\)

This sample flow is automatically assigned to the phone number that you claimed when you first set up contact flows\. For more information, see [Get started](amazon-connect-get-started.md)\. 

It uses **Check contact attributes** to determine if the customer is contacting you by phone or chat, and to route them accordingly\.
+ If the channel is chat, the customer is transferred to the **Set disconnect flow**\.
+ If the channel is voice, the customer is transferred to the other sample contact flows, based on their input\.