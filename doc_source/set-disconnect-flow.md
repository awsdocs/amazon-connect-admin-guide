# Flow block: Set disconnect flow<a name="set-disconnect-flow"></a>

## Description<a name="set-disconnect-flow-description"></a>
+ Specifies which flow to run after a disconnect event during a contact\. 

  A disconnect event is when:
  + A call, chat, or task is disconnected\.
  + A call is disconnected by a customer, agent, third party, supervisor, flow, telecom problem, API, or any other reason\.
  + A task is disconnected as a result of a flow action\.
  + A task expires\. The task is automatically disconnected if it is not completed in 7 days\. 

  When the disconnect event occurs, the corresponding flow runs\. 
+ Here are examples of when you might use this block:
  + Run post\-contact surveys\. For example, the agent asks the customer to remain on the line for a post\-call survey\. The agent hangs up and a disconnect flow is run\. In the disconnect flow, the customer is asked a set of questions using the [Get customer input](get-customer-input.md) block\. Their answers are uploaded using an [Invoke AWS Lambda function](invoke-lambda-function-block.md) block to an external customer feedback database\. The customer is thanked and disconnected\.

    For more information about creating post\-contact surveys, see this blog: [Easily create and visualize post chat surveys with Amazon Connect and Amazon Lex](https://aws.amazon.com/blogs/contact-center/easily-create-and-visualize-post-chat-surveys-with-amazon-connect-and-amazon-lex/)\. And check out this workshop: [Building a contact survey solution for Amazon Connect](https://catalog.workshops.aws/amazon-connect-contact-survey/en-US)\.
  + In a chat scenario, if a customer stops responding to the chat, use this block to decide whether to run the disconnect flow and call a [Wait](wait.md) block, or end the conversation\.
  + In task scenarios where a task may not be completed in 7 days, use this block to run a disconnect flow to determine whether the task should be requeued, or completed/[disconnected](disconnect-hang-up.md) by a flow action\.

## Supported channels<a name="set-disconnect-flow-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | Yes | 
| Task | Yes | 

## Flow types<a name="set-disconnect-flow-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ All flows

## Properties<a name="set-disconnect-flow-properties"></a>

The following image shows the **Properties** page of the **Set disconnect flow** block\.

![\[The properties page of the set disconnect flow block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-disconnect-flow-properties.png)

## Configured block<a name="set-disconnect-flow-configured"></a>

The following image shows an example of what this block looks like when it is configured\. It has the following branches: **Success** and **Error**\.

![\[A configured set disconnect flow block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-disconnect-flow-configured.png)

## Sample flows<a name="set-disconnect-flow-samples"></a>

Amazon Connect includes a set of sample flows\. For instructions that explain how to access the sample flows in the flow designer, see [Sample flows](contact-flow-samples.md)\. Following are topics that describe the sample flows which include this block\.
+ [Sample inbound flow \(first contact experience\)](sample-inbound-flow.md)

## Scenarios<a name="set-disconnect-flow-scenarios"></a>

See these topics for scenarios that use this block:
+ [Example chat scenario](web-and-mobile-chat.md#example-chat-scenario)
+ [Easily create and visualize post chat surveys with Amazon Connect and Amazon Lex](https://aws.amazon.com/blogs/contact-center/easily-create-and-visualize-post-chat-surveys-with-amazon-connect-and-amazon-lex/)
+ [Building a contact survey solution for Amazon Connect](https://catalog.workshops.aws/amazon-connect-contact-survey/en-US)