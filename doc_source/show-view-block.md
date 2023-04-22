# Flow block: Show view<a name="show-view-block"></a>

## Description<a name="show-view-block-description"></a>
+ Use this block configure UI based workflows that you can surface to users of front end applications\. You can use this block to create [step\-by\-step guides](https://docs.aws.amazon.com/connect/latest/adminguide/step-by-step-guided-experiences.html) for agents who are using the Amazon Connect agent workspace\.
+ To use this block, first select a View resource from a drop\-down menu and then map data to the different fields in the View's schema\. Yan use the **Set JSON** mapping option which lets you pass in entire JSON objects\. For details on the available View templates, see [View resource](https://docs.aws.amazon.com/connect/latest/adminguide/view-resources-sg.html)\.
+ When the block receives a response back from the client application, the output data can be referenced in flows using `$.Views.ViewResultData.FormData`\.
+ Check out our [library of samples and reusable modules](https://github.com/aws-samples/amazon-connect-step-by-step-guides-module-library) to help you get started with using the **Show view** block and creating step\-by\-step guides\. These modules show how you can configure the different types of **Show view** blocks and ways you can integrate step\-by\-step guides with other workflows and services\. They demonstrate good design patterns for common and complex use cases, and address the most common design concerns\.

  To load the samples into your Amazon Connect instance, use the [Import/export flows](contact-flow-import-export.md) feature to load the flow with the sample **Show view** block into your account\.

## Supported channels<a name="show-view-flow"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | No | 
| Chat | Yes | 
| Task | No | 

## Flow types<a name="show-view-block-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Contact Flow types

For the best building experience we recommend the *contact flow* type\.

## Properties<a name="show-view-block-properties"></a>

Properties are dynamically populated depending on which View resource you select\. The following image shows the **Properties** page of the **Show view** block\. It is set to the **Wizard** solution view\.

![\[The properties page of the Show view block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/show-view-block-sq.png)

## Configured block<a name="show-view-block-configured"></a>

The following image shows an example of what this block looks like when it is configured\. It has the following branches: **Back**, **Next**, **No Match**, **Error**, and **Timeout**\. 

![\[A configured Show view block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/show-view-block-sq-config.png)