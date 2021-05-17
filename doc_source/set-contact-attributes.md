# Contact block: Set contact attributes<a name="set-contact-attributes"></a>

## Description<a name="set-contact-attributes-description"></a>
+ Stores key\-value pairs as contact attributes\.
+ Contact attributes are accessible by other areas of Amazon Connect, such as the CTRs\. 

  For more information about how to use contact attributes, see [Use Amazon Connect contact attributes](connect-contact-attributes.md)\. 

## Contact flow types<a name="set-contact-attributes-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ All flows

## Properties<a name="set-contact-attributes-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-contact-attributes-properties.png)

**Tip**  
When using a user\-defined destination key, you can name it anything you want but don't include the **$** and **\.** \(period\) characters\. They are not allowed because they are both used in defining the attribute paths in JSONPath\.

## Configured block<a name="set-contact-attributes-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-contact-attributes-configured.png)

## Sample flows<a name="set-contact-attributes-samples"></a>

See these sample flows for scenarios that use this block:
+ [Sample inbound flow \(first contact experience\)](sample-inbound-flow.md)

## Scenarios<a name="set-contact-attributes-scenarios"></a>

See these topics for scenarios that use this block:
+ [How to reference contact attributes](how-to-reference-attributes.md)