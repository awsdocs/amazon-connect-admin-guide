# Types of contact attributes<a name="types-of-contact-attributes"></a>

The following types of contact attributes are available in Amazon Connect\.

## System contact attributes<a name="system-contact-attributes"></a>

These are predefined attributes in Amazon Connect\. You can reference system attributes, but you cannot create them\. 

Some system attributes relate to contacts, and some relate to metrics\. Not all blocks in a contact flow support using System attributes\. For example, you cannot use a System attribute to store customer input\. Instead, use a user\-defined attribute to store the data input by a customer\.

## Agent contact attributes<a name="agent-contact-attributes"></a>

A subset of system attributes related to agents in your contact center\.

Agent attributes are available only in the following types of contact flows:
+ Agent whisper
+ Customer whisper
+ Agent hold
+ Customer whisper
+ Outbound whisper
+ Transfer to agent\. In this case, the Agent attributes reflect the target agent, not the one who initiated the transfer\.

Agent attributes are not available in the following contact flow types:
+ Customer queue
+ Transfer to queue
+ Inbound contact flow

## Queue metrics contact attributes<a name="queue-metrics-contact-attributes"></a>

These are System metric attributes returned when you use a **Get queue metrics** block in your contact flow\.

## User\-defined contact attributes<a name="user-defined-contact-attributes"></a>

These attributes are created when a contact flow runs using **Set contact attributes** blocks\. When you get data from an external source, you can copy key\-value pairs as user\-defined attributes to reference later in a contact flow\. You can also create user\-defined attributes through the Amazon Connect API\.

User\-defined attributes include all attributes set by using a **Set contact attributes** block in a contact flow\. User\-defined attributes are included in contact trace records \(CTRs\)\. They are available to Lambda functions that are invoked after the **Set contact attributes** block, and are created in the Attributes namespace\. They are also available to applications that integrate with the Contact Control Panel \(CCP\) for screenpop information, and can be referenced in contact flows\.

## External contact attributes<a name="external-contact-attributes"></a>

**External**—Attributes are created via a process external to Amazon Connect\. For example, when you use an **Invoke AWS Lambda function** block in a contact flow, or integrate with an Amazon Lex bot\.

External attributes are returned as key\-value pairs from the most recent invocation of an **Invoke AWS Lambda function** block\. External attributes are overwritten with each invocation of the Lambda function\. You can access external attributes in contact flows via $\.External\.AttributeName\. For more information about using attributes in Lambda functions, see [Using AWS Lambda Functions with Amazon Connect](https://docs.aws.amazon.com/connect/latest/adminguide/connect-lambda-functions.html)\.

These attributes are not included in CTRs, not passed to the next Lambda invocation, and not passed to the CCP for screenpop information\. However, they can be passed as Lambda function inputs on an **Invoke AWS Lambda function** block, or copied to user\-defined attributes via the **Set contact attributes** block\. When used in **Set contact attributes** blocks, the attributes that are copied are included in CTRs, and can be used in the CCP\.

## Lex slots contact attributes<a name="lex-slots-contact-attributes"></a>

External attributes for the slot name of an Amazon Lex bot\.

## Lex attributes<a name="lex-attributes"></a>

Session attributes from an Amazon Lex bot interaction\.