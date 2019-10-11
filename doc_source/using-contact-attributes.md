# Contact Attribute Concepts<a name="using-contact-attributes"></a>

When you create a contact flow, you can create user\-defined contact attributes using **Set contact attributes** blocks\. You can then reference them in other parts of a contact flow using any other block that supports dynamic attributes\. For example, you could use a **Check contact attributes** block to compare the value of an attribute to a condition you define, and then route the contact based on the results of the comparison\. You could also retrieve data from external sources, and then create user\-defined attributes from the external data so that you can reference them later in a contact flow, such as the status of an order or an expected shipping date\.

Personalize the customer experience by including the customer's name when you use text to speech text in a **Play prompt** or **Get customer input** block to speak messages to your customer\. Use contact attributes to store input provided by a customer during an interaction with an Amazon Lex bot to enable automated interactions\.

As a best practice, make attributes and attribute values case\-sensitive, and always match case in each context where they are used\.

The following types of contact attributes are available in Amazon Connect:
+ **System**—Predefined attributes in Amazon Connect\. You can reference system attributes, but you cannot create them\. Some system attributes relate to contacts, and some relate to metrics\. Not all blocks in a contact flow support using System attributes\. For example, you cannot use a System attribute to store customer input\. Instead, use a user\-defined attribute to store the data input by a customer\.
+ **Agent**—A subset of system attributes related to agents in your contact center\.
+ **Queue metrics**—System metric attributes returned when you use a **Get queue metrics** block in your contact flow\.
+ **User\-defined**—Attributes that are created when a contact flow executes using **Set contact attributes** blocks\. When you get data from an external source, you can copy key\-value pairs as user\-defined attributes to reference later in a contact flow\. You can also create user\-defined attributes through the Amazon Connect API\.

  User\-defined attributes include all attributes set by using a **Set contact attributes** block in a contact flow\. User\-defined attributes are included in contact trace records \(CTRs\)\. They are available to Lambda functions that are invoked after the **Set contact attributes** block, and are created in the Attributes namespace\. They are also available to applications that integrate with the Contact Control Panel \(CCP\) for screenpop information, and can be referenced in contact flows\.
+ **External**—Attributes are created via a process external to Amazon Connect\. For example, when you use an **Invoke AWS Lambda function** block in a contact flow, or integrate with an Amazon Lex bot\.

  External attributes are returned as key\-value pairs from the most recent invocation of an **Invoke AWS Lambda function** block\. External attributes are overwritten with each invocation of the Lambda function\. You can access external attributes in contact flows via $\.External\.AttributeName\. For more information about using attributes in Lambda functions, see [Using AWS Lambda Functions with Amazon Connect](https://docs.aws.amazon.com/connect/latest/adminguide/connect-lambda-functions.html)\.

  These attributes are not included in CTRs, not passed to the next Lambda invocation, and not passed to the CCP for screenpop information\. However, they can be passed as Lambda function inputs on an **Invoke AWS Lambda function** block, or copied to user\-defined attributes via the **Set contact attributes** block\. When used in **Set contact attributes** blocks, the attributes that are copied are included in CTRs, and can be used in the CCP\.
+ **Lex slots**—External attribute for the slot name of an Amazon Lex bot\.
+ **Lex attributes**—Session attributes from an Amazon Lex bot interaction\.