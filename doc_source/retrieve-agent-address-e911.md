# Retrieve an agent's address when they call 911<a name="retrieve-agent-address-e911"></a>

To retrieve an agent's validated address from the Amazon Connect, create an outbound whisper flow that calls a Lambda function\. Code the Lambda function to retrieve the address from the agent's customer profile, as shown in the following illustration:

![\[Amazon Connect E911 address retrieval process.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/e911-workflow-2.png)

1. Create an AWS Lambda function that uses the [SearchProfiles](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_SearchProfiles.html) API to retrieve the physical address for a given agent from Customer Profiles\.

1. [Create an outbound whisper flow that relays this physical address as part of the emergency out dial](#connect-detect-911-dial)\. 

1. [Add a task that sends notifications when an E911 call is placed](#connect-e911-notifications)\. 

## Create an outbound whisper flow that relays the physical address<a name="connect-detect-911-dial"></a>

For outbound voice calls within Amazon Connect, an [outbound whisper flow](create-contact-flow.md#contact-flow-types) usually specifies the whisper to be played to customer\. However, in this case you need to configure an [outbound whisper flow](create-contact-flow.md#contact-flow-types) to do the following:

1. Inspect the outbound call string from an agent\. 

1. If the string equals **911** \(or **933** in a test environment\), then retrieve the agent's stored location/physical address from Customer Profiles by using a Lambda function to call the [SearchProfiles](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_SearchProfiles.html) API \.

1. Attach the physical address to a contact attribute and proceed with the 911 \(or 933\) outbound call\. 

The following illustration shows an example [outbound whisper flow](create-contact-flow.md#contact-flow-types)\. It is configured to inspect the outbound call string from an agent, and retrieve the stored physical address for that agent by using a Lambda function\. It includes the following blocks in sequence: [Invoke AWS Lambda function](invoke-lambda-function-block.md), [Set contact attributes](set-contact-attributes.md), and [Call phone number](call-phone-number.md)\.

![\[An outbound whisper flow to detect a 911 or 933 call.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/e911-example-outbound-whisper.png)
+ Step 1: Call a Lambda function that retrieves the location for an agent \(Input parameter = Agent User Name\)\. The following image shows how to configure an [Invoke AWS Lambda function](invoke-lambda-function-block.md) block is so the agent **username** is passed to the Lambda function\.  
![\[The properties page of an Invoke AWS Lambda function block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/e911-invoke-lambda-block.png)
+ Step 2: Attach the location received to a contact attribute \(see [Format a physical address for E911](connect-format-physical-address-e911.md) for the required format\)\.
+ Step 3: Update the call origination to the agent's phone number and continue with the outbound call\. 
**Note**  
The origination number is the caller ID that is passed along with the 911 outbound call\. If the origination phone number supports inbound calls, emergency responders will be able to call back the agent in case the initial phone call was disconnected\.  
The 911 call is specific to United States\. As a result, the origination phone number must be a valid US phone number\.   
For example, when an agent places an outbound call, if an invalid US phone number is passed to the carrier network, the carrier can reject the call\. To avoid this situation, if the agent uses an invalid number from Amazon Connect, Amazon Connect defaults to the Caller ID that is assigned to the queue in the agent's routing profile\.
The capability does not place any other rules on this number\. For example, the origination number can the phone number of the security front desk\.

## Add a task that sends notifications when an E911 call is placed<a name="connect-e911-notifications"></a>

When an agent calls 911 it is important to notify in real time the appropriate people in your organization, such as corporate security or a human resources administrator, that someone from the contact center has placed an E911 call\. To do this, create an Amazon Connect task in the [outbound whisper flow](create-contact-flow.md#contact-flow-types)\. Then add custom notification logic to the task\. 

The following image shows an example of a [Create task](create-task-block.md) block in an [outbound whisper flow](create-contact-flow.md#contact-flow-types)\. It is located after the **Set contact attributes** block and before the **Call phone number** block\.

![\[C create task block in an outbound whisper flow.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/e911-create-task-flow.png)

The following image shows the **Properties** page for a [Create task](create-task-block.md) block\. It is configured to notify corporate security that an agent from the contact center has placed an E911 call\. 

![\[The properties page of a create task block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/e911-create-task-config.png)