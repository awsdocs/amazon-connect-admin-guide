# How to use Lex alternate intent attributes<a name="alternate-intent-attributes"></a>

Usually you configure flows to branch on the winning Lex intent\. However, in some situations, you might want to branch on an alternate intent\. That is, what the customer might have meant\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/check-contact-attributes-alternate-intents.png)

1. **Intent name** is the name of an alternate intent in Lex\. It's case sensitive and must match what's in Lex exactly\.

1. **Intent Attribute** is what Amazon Connect is going to check\. In this example, it's going to check the **Intent Confidence Score**\.

1. **Conditions to check**: If Lex is 70% certain the customer meant the alternate intent instead of the winning intent, branch\.