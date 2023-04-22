# Flow block: Check contact attributes<a name="check-contact-attributes"></a>

## Description<a name="check-contact-attributes-description"></a>
+ Branches based on a comparison to the value of a contact attribute\.
+ Supported comparisons include: **Equals**, **Is Greater Than**, **Is Less Than**, **Starts With**, **Contains**\.

## Supported channels<a name="check-contact-attributes-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | Yes | 
| Task | Yes | 

## Flow types<a name="check-contact-attributes-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ All flows

## Properties<a name="check-contact-attributes-properties"></a>

The following image shows the **Properties** page of the **Check contact attributes** block\. In this example, the block is configured to check whether the contact is a **PremiumCustomer**, which is a [user\-defined attribute](connect-attrib-list.md#user-defined-attributes)\. 

![\[The properties page of the Check contact attributes block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-contact-attributes-properties.png)

### Conditions to check can be dynamic<a name="check-dynamic-attributes"></a>

You can check conditions like the following:
+ $\.Attributes\.verificationCode

To check for a NULL value, you need to use a Lambda\. 

### Amazon Lex attributes<a name="check-lex-attributes"></a>

You can set attributes that are **Type** = **Lex** as follows: 
+ **Alternative Intents**: Usually you configure flows to branch on the winning Lex intent\. However, in some situations, you might want to branch on an alternate intent\. That is, what the customer might have meant\. 

  For example, in the following image of the **Check contact attributes** properties page, it is configured so the alternative intent indicates that if Amazon Lex is more than 70% confident the customer meant *fraud*, the flow should branch accordingly\.  
![\[The properties page of the Check contact attributes block configured for an alternative intent.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-contact-attributes-alternate-intents.png)

  1. **Intent name** is the name of an alternate intent in Lex\. It's case sensitive and must match what's in Lex exactly\.

  1. **Intent Attribute** is what Amazon Connect is going to check\. In this example, it's going to check the **Intent Confidence Score**\.

  1. **Conditions to check**: If Lex is 70% certain the customer meant the alternate intent instead of the winning intent, branch\.
+ **Intent Confidence Score**: How confident is the bot that it understands the customer's intent\. For example, if the customer says "I want to update an appointment," *update* can mean *reschedule* or *cancel*\. Amazon Lex provides the confidence score on a scale of 0 to 1:
  + 0 = not at all confident
  + \.5 = 50% confident
  + 1 = 100% confident
+ **Intent Name**: The user intent returned by Amazon Lex\.
+ **Sentiment Label**: What is the winning sentiment, the one with the highest score\. You can branch on POSITIVE, NEGATIVE, MIXED, or NEUTRAL\.
+ **Sentiment Score**: Amazon Lex integrates with Amazon Comprehend to determine the sentiment expressed in an utterance:
  + Positive
  + Negative
  + Mixed: The utterance expresses both positive and negative sentiments\.
  + Neutral: The utterance does not express either positive or negative sentiments\.
+ **Session Attributes**: Map of key\-value pairs representing the session\-specific context information\.
+ **Slots**: Map of intent slots \(key/value pairs\) Amazon Lex detected from the user input during the interaction\.

## Configuration tips<a name="check-contact-attributes-tips"></a>
+ If you have multiple conditions to compare, Amazon Connect checks them in the order they are listed\. 

  For example, in the following image of the **Check contact attributes** properties page, it is configured so Amazon Connect compares the **greater than 60** condition first and compares **greater than 2** last\.   
![\[The properties page of the Check contact attributes block configured to compare multiple conditions.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-contact-attributes-tips-order-conditions-are-checked.png)
+ This block doesn't support case\-insensitive pattern matching\. For example, if you're trying to match against the word **green** and the customer types **Green**, it would fail\. You would have to include every permutation of upper and lower\-case letters\.

## Configured<a name="check-contact-attributes-configured"></a>

The following image shows an example of what this block looks like when it is configured\. It shows the block has four branches, one for each condition: greater or equal to 60, greater to equal to 10, greater or equal to 2, or **No match**\.

![\[A configured Check contact attributes block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-contact-attributes-configured.png)

## Sample flows<a name="check-contact-attributes-samples"></a>

Amazon Connect includes a set of sample flows\. For instructions that explain how to access the sample flows in the flow designer, see [Sample flows](contact-flow-samples.md)\. Following are topics that describe the sample flows which include this block\.
+ [Sample inbound flow \(first contact experience\)](sample-inbound-flow.md)
+  [Sample interruptible queue flow with callback](sample-interruptible-queue.md)

## Scenarios<a name="check-contact-attributes-scenarios"></a>

See these topics for scenarios that use this block:
+ [How to reference contact attributes](how-to-reference-attributes.md)
+ [Route based on contact's channel](use-channel-contact-attribute.md)