# Default contact flows<a name="contact-flow-default"></a>

Amazon Connect includes a set of default contact flows that have already been published\. It uses them to power your contact center\. 

For example, say you create a contact flow that includes putting the customer on hold, but you don't create a prompt for it\. The default contact flow, **Default agent hold**, will be played automatically\. This is a way to help you get started with your call center quickly\.

**Tip**  
If you want to change the behavior of a default contact flow, we recommend creating a new customized flow based on the default\. Then call the new flow intentionally in your contact flows rather than defaulting to it\. This gives you better control over how your contact flows work\.

To see the list of default flows in the Amazon Connect console, go to **Routing**, **Contact Flows**\. They all start with **Default** in their name\. 

**Topics**
+ [Change a default contact flow](change-default-contact-flow.md)
+ [Default agent hold](default-agent-hold.md)
+ [Default agent transfer](default-agent-transfer.md)
+ [Default customer queue](default-customer-queue.md)
+ [Default customer whisper](default-customer-whisper.md)
+ [Default agent whisper](default-agent-whisper.md)
+ [Default customer hold](default-customer-hold.md)
+ [Default outbound](default-outbound.md)
+ [Default queue transfer](default-queue-transfer.md)
+ [Default prompts from Amazon Lex](default-prompts-from-lex.md)