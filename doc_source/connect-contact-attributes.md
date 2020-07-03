# Use Amazon Connect contact attributes<a name="connect-contact-attributes"></a>

 In Amazon Connect, a contact is an interaction with a customer in your contact center\. The interaction can be a voice phone call, a chat, or an automated interaction using an Amazon Lex bot\. Contact attributes in Amazon Connect refer to key\-value pairs that contain data about a contact\.

Using contact attributes, you can customize and personalize the experience customers have when they interact with your contact center\. Contact attributes let you store customer input or data about a customer, and then use it later in a contact flow\. You can also check the values of contact attributes and use a condition to determine the branching behavior of the contact flow based on the value\.

Contact attributes let you pass data between Amazon Connect and other services, such as Amazon Lex and AWS Lambda\. Contact attributes can be both set and consumed by each service\. For example, you could use a Lambda function to look up customer information, such as their name or order number, and use contact attributes to store the values returned to Amazon Connect\. You could then reference those attributes to include the customer's name in messages using text to speech, or store their order number so they do not have to enter it again\.

**Topics**
+ [Contact attribute concepts](using-contact-attributes.md)
+ [Types of contact attributes](types-of-contact-attributes.md)
+ [How to use contact attributes to personalize the customer experience](use-attributes-cust-exp.md)
+ [Use Amazon Connect contact attributes with other services](attribs-external-references.md)
+ [Use contact attributes in the CCP](use-attribs-ccp.md)
+ [How to reference contact attributes](how-to-reference-attributes.md)
+ [How to use system metric attributes](attrib-system-metrics.md)
+ [How to use the Channel contact attribute](use-channel-contact-attribute.md)
+ [How to use Lex session attributes](how-to-use-session-attributes.md)
+ [How to use the same bot for voice and chat](one-bot-voice-chat.md)
+ [Contact attributes available in Amazon Connect](connect-attrib-list.md)