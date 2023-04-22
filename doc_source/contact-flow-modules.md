# Flow modules for reusable functions<a name="contact-flow-modules"></a>

Flow modules are reusable sections of a flow\. You can create them to extract repeatable logic across your flows, and create common functions\. For example:

1. You can create a module that sends SMS text messages to customers\.

1. You can invoke the module in flows that handle situations where customers want to reset their passwords, check their bank balances, or receive a one\-time password\.

Following are the benefits of using modules:
+ Simplify managing common functionality across flows\. For example, an SMS module could validate the format of phone number, confirm SMS opt\-in preferences, and integrate with an SMS service, such as Amazon Pinpoint\.
+ Makes it more efficient to maintain flows\. For example, you can quickly propagate changes across all flows that invoke a flow module\.
+ Helps separate flow designer responsibilities\. For example, you can have both technical module designers and non\-technical flow designers\.

## Where you can use modules<a name="where-to-use-modules"></a>

You can use modules in any flow that is [type](create-contact-flow.md#contact-flow-types) **Inbound flow**\. 

The following types of flows do not support modules: **Customer queue**, **Customer hold**, **Customer whisper**, **Outbound whisper**, **Agent hold**, **Agent whisper**, **Transfer to agent**, ** Transfer to queue**\. 

## Limitations<a name="modules-limits"></a>
+ Modules do not allow overriding flow local data of the invoking flow\. This means you can't use the following with modules:
  + External attributes
  + Amazon Lex attributes
  + Customer Profiles attributes
  + Wisdom attributes
  + Queue metrics
  + Stored customer input
+ Modules do not allow invoking another module\.

To pass any data to a module, or to get any data from a module, you need to pass and retrieve attributes\.

For example, you want data that is written from Lambda \(an External attribute\) and pass it to the module so you can make a decision\. Your Lambda identifies whether the customer is a VIP member\. You need that information inside the module because if they are a VIP member, you want to play a prompt thanking them for their membership\. Since default Lambda is not available inside a module, you use attributes to pass and retrieve data\.  

## Security profile permissions for modules<a name="module-permissions"></a>

Before you can add modules to Inbound flows, you must have permissions in your security profile\. By default, the **Admin** and **CallCenterManager** security profiles have these permissions\.

## Create a module<a name="use-modules"></a>

For information about the number of modules that you can create for each Amazon Connect instance, see [Amazon Connect service quotas](amazon-connect-service-limits.md)\.

1. Log in to the Amazon Connect console with an account assigned to a security profile that has permissions to create modules\.

1. On the navigation menu, choose **Routing**, **Contact flows**\.

1. Choose **Modules**, **Create flow module**\. 

1. Add the blocks that you want to your module\. When finished, choose **Publish**\. This makes the module available to use in other flows\.

## Add a module to a flow<a name="add-modules"></a>

1. Log in to the Amazon Connect console with an account assigned to a security profile that has permissions to create flows\. You don't need permissions to create modules\.

1. On the navigation menu, choose **Routing**, **Contact flows**\.

1. Choose **Create flow** or select an existing contact flow that is an **Inbound** type\. 

1. To add a module, go to the **Integrate** section, and choose **Invoke flow module**\. 

1. When you're finished creating your flow, choose **Publish**\. 

## Example module<a name="example-module"></a>

This module shows how to get a random fun fact by invoking a Lambda function\. The module uses a contact attribute \(`$.Attributes.FunFact`\) to retrieve the fun fact\. Flows that invoke this module can play a FunFact to customers, depending on their incoming contact type\. 

The inbound flows in your instance can invoke this common module and get the fun fact\.

Following is an image of the FunFact module:

![\[The funfact module in the flow designer.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/module-example1.png)

Following is an image of the FunFactSampleFlow that invokes the module:

![\[The funfactsampleflow in the flow designer.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/module-example2.png)