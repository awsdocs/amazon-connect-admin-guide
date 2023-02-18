# Flow block: Show view \(Preview\)<a name="show-view-block"></a>


|  | 
| --- |
| This is prerelease documentation for a service in preview release\. It is subject to change\. | 

## Description<a name="show-view-block-description"></a>

This block is used to configure UI based workflows that you can surface to users in front end applications\. In particular, you can use this block to create [step\-by\-step guides](https://docs.aws.amazon.com/connect/latest/adminguide/step-by-step-guided-experiences.html) for your agents in the Amazon Connect agent workspace\.

To use this block, first select a View resource from a drop\-down menu and then map data to the different fields in the View’s schema\. With this block you can use the **Set JSON** mapping option which lets you pass in entire JSON objects\. For more details on the different available View templates, see [View resource \(Preview\)](https://docs.aws.amazon.com/connect/latest/adminguide/view-resources-sg.html)\.

## Supported channels<a name="show-view-flow"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | Yes | 
| Task | Yes | 

## Flow types<a name="show-view-block-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ All flow types

For the best building experience we recommend the *contact flow* type\.

## Properties<a name="show-view-block-properties"></a>

Properties are dynamically populated depending on the View resource that is selected\. Below is one example of the different properties\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/show-view-block-sq.png)

## Configured block<a name="show-view-block-configured"></a>

When this block is configured, it will look similar to the image below\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/show-view-block-sq-config.png)