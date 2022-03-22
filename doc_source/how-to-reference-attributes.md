# How to reference contact attributes<a name="how-to-reference-attributes"></a>

The way you reference contact attributes depends on how they were created and how you are accessing them\. 
+ To reference attributes that contain spaces in their name, such as user defined attributes, place brackets and single quotations around the attribute name\. For example: ` $.Attributes.['user attribute name']`\. 
+ To reference attributes in the same namespace, such as a system attribute, you use the attribute name, or the name you specified as the **Destination key**\.
+ To reference values in a different namespace, such as referencing an external attribute, you specify the JSONPath syntax to the attribute\.
+ To use contact attributes to access other resources, set a user\-defined attribute in your contact flow and use the Amazon Resource Name \(ARN\) of the resource you want to access as the value for the attribute\. 

## Lambda examples<a name="lambda-examples"></a>
+ To reference a customer name from a Lambda function lookup, use $\.External\.AttributeKey, replacing AttributeKey with the key \(or name\) of the attribute returned from the Lambda function\.
+ To use an Amazon Connect prompt in a Lambda function, set a user\-defined attribute to the ARN for the prompt, and then access that attribute from the Lambda function\.

## Amazon Lex examples<a name="lex-examples"></a>
+ To reference an attribute from an Amazon Lex bot, you use the format $\.Lex\. and then include the part of the Amazon Lex bot to reference, such as $\.Lex\.IntentName\.
+ To reference the customer input to an Amazon Lex bot slot, use $\.Lex\.Slots\.*slotName*, replacing *slotName* with the name of the slot in the bot\.

## Set contact attribute example<a name="set-contact-attribute-example"></a>

Use a [Set contact attributes](set-contact-attributes.md) block to set a value that is later referenced in a contact flow\. For example, create a personalized greeting for customers routed to a queue based on the type of customer account\. You could also define an attribute for a company name or line of business to include in the text to speech strings said to a customer\. The **Set contact attributes** block is useful for copying attributes retrieved from external sources to user\-defined attributes\.

**To set a contact attribute with a [Set contact attributes](set-contact-attributes.md) block**

1. In Amazon Connect, choose **Routing**, **Contact flows**\.

1. Select an existing contact flow, or create a new one\.

1. Add a **Set contact attributes** block\.

1. Edit the **Set contact attributes** block, and choose **Use text**\.

1. For the **Destination key**, provide a name for the attribute, such as *Company*\. This is the value you use for the **Attribute** field when using or referencing attributes in other blocks\. For the **Value**, use your company name\.

   You can also choose to use an existing attribute as the basis for creating the new attribute\.