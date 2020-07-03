# Use contact attributes in the CCP<a name="use-attribs-ccp"></a>

Contact attributes also let you capture information and then present that information in a screenpop to an agent in the Contact Control Panel \(CCP\)\. Use contact attributes to customize the agent experience when using the CCP integrated with a customer relationship management \(CRM\) application\. Also use them when integrating Amazon Connect with a custom application using the Amazon Connect Streams API or Amazon Connect API\. You can use all user\-defined attributes, in addition to the customer number and the dialed number, in the CCP using the Amazon Connect Streams JavaScript library\. For more information, see [Amazon Connect Streams API](https://github.com/aws/amazon-connect-streams) or Amazon Connect API\.

When you use the Amazon Connect Streams API, you can access user\-defined attributes by invoking contact\.getAttributes\(\)\. You can access endpoints via contact\.getConnections\(\), where a connection has a getEndpoint\(\) invocation on it\.

To access the attribute directly from a Lambda function, use $\.External\.AttributeName\. If the attribute is stored to a user\-defined attribute from a **Set contact attributes** block, use $\.Attributes\.AttributeName\.

For example, included with your Amazon Connect instance, there is a contact flow named “Sample note for screenpop\.” In this contact flow, a **Set contact attributes** block is used to create an attribute from a text string\. The text, as an attribute, can be passed to the CCP to display a note to an agent\.