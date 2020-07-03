# Contact Block: Set Disconnect Flow<a name="set-disconnect-flow"></a>

## Contact flow types<a name="set-disconnect-flow-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ All flows

## Description<a name="set-disconnect-flow-description"></a>
+ Specifies which contact flow to run after a disconnect event during a conversation\. A disconnect event is when an agent disconnects\. When the disconnect event occurs, the corresponding content flow runs\. 
+ Here are examples of when you might use this block:
  + Run post\-call surveys\. For example, the agent asks the customer to remain on the line for a post\-call survey\. The agent hangs up and a disconnect flow is run\. In the disconnect flow, the customer is asked a set of questions using the [Get Customer Input](get-customer-input.md) block\. Their answers are uploaded using an [Invoke AWS Lambda Function](invoke-lambda-function-block.md) block to an external customer feedback database\. The customer is thanked and disconnected\.

    For more information about creating post\-call surveys, see this blog post by an AWS Solution Architect: [Create post call surveys in Amazon Connect](https://aws.amazon.com/blogs/contact-center/create-post-call-surveys-in-amazon-connect/)\.
  + In a chat scenario, if a customer stops responding to the chat, use this block to decide whether to run the disconnect flow and call a [Wait](wait.md) block, or end the conversation\.
+ When this block is used in a queued callback flow, the contact is routed down the **Success** branch\. No disconnect flow is run for those contacts\.

## Properties<a name="set-disconnect-flow-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-disconnect-flow-properties.png)

## Configured block<a name="set-disconnect-flow-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-disconnect-flow-configured.png)

## Sample flows<a name="set-disconnect-flow-samples"></a>

See these sample flows for scenarios that use this block:
+ [Sample inbound flow \(first contact experience\)](sample-inbound-flow.md)

## Scenarios<a name="set-disconnect-flow-scenarios"></a>

See these topics for scenarios that use this block:
+ [Example chat scenario](chat.md#example-chat-scenario)
+ [Create post call surveys in Amazon Connect](https://aws.amazon.com/blogs/contact-center/create-post-call-surveys-in-amazon-connect/)