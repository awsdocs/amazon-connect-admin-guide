# What is a contact attribute?<a name="what-is-a-contact-attribute"></a>

In Amazon Connect, each interaction with a customer is a **contact**\. The interaction can be a phone call \(voice\), a chat, or an automated interaction using an Amazon Lex bot\.

Each contact can have some data that is specific to a particular interaction\. This data can be accessed as a contact attribute\. For example:
+ The name of the customer
+ The name of the agent
+ The channel used for the contact, such as phone or chat
+ And more

A contact attribute represents this data as a key\-value pair\. You might think of it as a field name together with the data entered into that field\.

For example, here are a couple of key\-value pairs for the customer name:


| Key | Value | 
| --- | --- | 
| firstname  | Jane  | 
| lastname  | Doe  | 

The advantage of contact attributes is that they enable you to store temporary information about the contact so you can use it in the contact flow\.

For example, in your welcome messages, you can say their name or thank them for being a member\. To do this, you need a way of retrieving data about that specific customer and using it in a contact flow\.

## Common use cases<a name="contact-attribute-scenarios"></a>

Here are some common use cases for where contact attributes are used:
+ Use the customer phone number to schedule a queued callback\.
+ Identify which agent is interacting with a customer so that a post call survey can be associated with a contact\.
+ Identify the number of contacts in a queue to decide if the contact should be routed to a different queue\.
+ Get the corresponding media streaming ARN to store in a database\.
+ Use the customer phone number to identify the status of a customer \(for example, are they a member\), or the status of their order \(shipped, delayed, etc\.\) to route them to the appropriate queue\.
+ Based on a customer interaction with a bot, identify the slot \(for example, the type of flowers to order\) to be used in a flow\.

## Types of contact attributes<a name="types-of-contact-attributes"></a>

To make it faster for you to find and choose the attributes you want to use, attributes are grouped into **types**\. For each contact block, we only surface those types of attributes that work with it\. 

Another way to think about types of contact attributes is to categorize them based on where the value comes from\. The values for contact attributes have three sources: 
+ Amazon Connect provides the value, such as the agent's name, during the contact interaction\. This is known as providing the value at runtime\. 
+ An external process, such as Amazon Lex or AWS Lambda, provides the value\. 
+ [User\-defined](connect-attrib-list.md#user-defined-attributes)\. In the contact flow, you can specify the value for an attribute\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-attributes-types.png)

## Contact attributes in the contact record<a name="attributes-in-ctr"></a>

In contact records, contact attributes are shared across all contacts with the same InitialContactId\.

For example, while carrying out transfers, a contact attribute updated in the transfer flow updates the attribute's value in the contact attributes of both contact records \(that is, the Inbound and Transfer contact attributes\)\. 

## "$" is a special character<a name="dollar-sign-special"></a>

Amazon Connect treats the "$" character as a special character\. You can't use it in a key when setting an attribute\. 

 For example, let's say you're creating an interact block with text\-to\-speech\. You set an attribute like this: 

 ` {"$one":"please read this text"} ` 

When Amazon Connect reads this text, it reads "dollar sign one" to the contact instead of "please read this text\." Also, if you were to include $ in a key and try to reference the value later using Amazon Connect, it wouldn't retrieve the value\. 

Amazon Connect does log and pass the full key:value pair `({"_$one":"please read this text"})` to integrations such as Lambda\. 