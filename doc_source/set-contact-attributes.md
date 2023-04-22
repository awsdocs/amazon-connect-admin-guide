# Flow block: Set contact attributes<a name="set-contact-attributes"></a>

## Description<a name="set-contact-attributes-description"></a>
+ Stores key\-value pairs as contact attributes\.
+ Contact attributes are accessible by other areas of Amazon Connect, such as contact records\. 

  For more information about how to use contact attributes, see [Use Amazon Connect contact attributes](connect-contact-attributes.md)\. 

## Supported channels<a name="set-contact-attributes-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | Yes | 
| Task | Yes | 

## Flow types<a name="set-contact-attributes-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ All flows

## Properties<a name="set-contact-attributes-properties"></a>

The following image shows the **Properties** page of the **Set contact attributes** block\. It is configured to route a contact down the Success branch when the user\-defined attribute **greetingPlayed** equals **true**\.

![\[The properties page of the Set contact attributes block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-contact-attributes-properties.png)

## Configuration tips<a name="set-contact-attributes-tips"></a>
+ When using a user\-defined destination key, you can name it anything you want but don't include the **$** and **\.** \(period\) characters\. They are not allowed because they are both used in defining the attribute paths in JSONPath\.
+ You can use the **Set contact attribute** block to set the language attribute required for an Amazon Lex V2 bot\. \(Your language attribute in Amazon Connect must match the language model used to build your Amazon Lex V2 bot\.\) The following image shows a language attribute set to Spanish\.  
![\[The properties page for Set contact attributes, Value set to Spanish.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-contact-attributes-language.png)

  Or, you can use the [Set voice](set-voice.md) block to set the language required for an Amazon Lex V2 bot\. 

## Configured block<a name="set-contact-attributes-configured"></a>

The following image shows an example of what this block looks like when it is configured\. It has two branches: **Success** and **Error**\.

![\[A configured set contact attributes block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-contact-attributes-configured.png)

## Sample flows<a name="set-contact-attributes-samples"></a>

Amazon Connect includes a set of sample flows\. For instructions that explain how to access the sample flows in the flow designer, see [Sample flows](contact-flow-samples.md)\. Following are topics that describe the sample flows which include this block\.
+ [Sample inbound flow \(first contact experience\)](sample-inbound-flow.md)

## Scenarios<a name="set-contact-attributes-scenarios"></a>

See these topics for scenarios that use this block:
+ [How to reference contact attributes](how-to-reference-attributes.md)