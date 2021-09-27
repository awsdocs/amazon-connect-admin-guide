# Contact block: Set contact attributes<a name="set-contact-attributes"></a>

## Description<a name="set-contact-attributes-description"></a>
+ Stores key\-value pairs as contact attributes\.
+ Contact attributes are accessible by other areas of Amazon Connect, such as Contact Trace Records \(CTRs\)\. 

  For more information about how to use contact attributes, see [Use Amazon Connect contact attributes](connect-contact-attributes.md)\. 

## Supported channels<a name="set-contact-attributes-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | Yes | 
| Task | Yes | 

## Contact flow types<a name="set-contact-attributes-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ All flows

## Properties<a name="set-contact-attributes-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-contact-attributes-properties.png)

## Configuration tips<a name="set-contact-attributes-tips"></a>
+ When using a user\-defined destination key, you can name it anything you want but don't include the **$** and **\.** \(period\) characters\. They are not allowed because they are both used in defining the attribute paths in JSONPath\.
+ You can use the **Set contact attribute** block to set the language attribute required for an Amazon Lex V2 bot\. \(Your language attribute in Amazon Connect must match the language model used to build your Amazon Lex V2 bot\.\)  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-contact-attributes-language.png)

  Or, you can use the [Set voice](set-voice.md) block to set the language required for an Amazon Lex V2 bot\. 

## Configured block<a name="set-contact-attributes-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-contact-attributes-configured.png)

## Sample flows<a name="set-contact-attributes-samples"></a>

See these sample flows for scenarios that use this block:
+ [Sample inbound flow \(first contact experience\)](sample-inbound-flow.md)

## Scenarios<a name="set-contact-attributes-scenarios"></a>

See these topics for scenarios that use this block:
+ [How to reference contact attributes](how-to-reference-attributes.md)