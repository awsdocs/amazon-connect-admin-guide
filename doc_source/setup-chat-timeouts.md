# Set up chat timeouts for chat participants<a name="setup-chat-timeouts"></a>

When a chat conversation between an agent and a customer has been inactive \(no messages sent\) for a certain amount of time, you may want to consider a chat participant to be idle, and you may even want to automatically disconnect an agent from the chat\.

To do this you can configure both idle timeouts and auto\-close timeouts using the [UpdateParticipantRoleConfig](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateParticipantRoleConfig.html) action\.

**Tip**  
You configure chat timeouts for when customers are interacting with Lex, in the [Flow block: Get customer input](get-customer-input.md) block\. See the [Configurable time\-outs for chat input during a Lex interaction](get-customer-input.md#get-customer-input-configurable-timeouts-chat) section\. 

**You can set four different types of timers\.**
+ You specify the amount of time that has to elapse before an action is taken\.
+ Any combination of timers can be used\.     
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/setup-chat-timeouts.html)

**Specify all timers in minutes\.**
+ Minimum: 2 minutes
+ Maximum: 480 minutes \(8 hours\)

**Timers apply to participant roles, and apply for life of the chat\.**
+ You configure timers for participant roles such as agent and customer, rather than individual participants\.
+  After you set the timers, they apply for the life of the chat\. If a chat is transferred, the timers apply to the new agent/customer interaction\.

## How chat timers work<a name="how-chat-timer-work"></a>

Timers behave as follows:
+ Timers run only when both an agent and a customer are connected to the chat\. 
+ Timers are first started when an agent joins the chat, and are stopped if the agent leaves the chat\.
+ Idle timers run before auto\-disconnect timers, if both are configured for a role\. For example, if both timers are configured, then the auto\-disconnect timer starts only after a participant is deemed idle\.
+ If only one type of timer is configured for a role, then that timer starts immediately\.
+ If at any time a participant sends a message, the timers for that participant are reset\. If they were considered idle, they will no longer be\.
+  The configuration that was set when the agent joined applies for as long as the agent remains on the chat\. If you update the timer configuration while an agent and customer are already connected to each other, the new configuration is stored but not applied until and unless a new agent connects to the chat\.
+ When an auto\-disconnect event occurs, all participants other than the customer \(such as the agent and any monitoring supervisor\) are disconnected\. If a [Set disconnect flow](set-disconnect-flow.md) block has been configured, the chat is routed to it\.

## Messages displayed to participants<a name="chat-timeouts-events"></a>

Messages are displayed to all participants when any one of the following events happen:
+ A participant becomes idle\.
+ An idle participant sends a message, and is no longer idle\.
+ An auto\-disconnect occurs\. Because the agent is disconnected, they won't be able to see the message\.

These events are not persisted to the transcripts, nor billed\.

The default messages \(in all supported languages\) are displayed to agents in the Contact Control Panel \(CCP\) for each of these events\. 

The following image show examples of default idleness messages that the agent would see in the CCP\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/chat-timeout-message.png)

## Recommended usage<a name="chat-timeouts-usage"></a>

To use the chat timeout feature, we recommend that you do the following:

1. Embed a call to the [UpdateParticipantRoleConfig](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateParticipantRoleConfig.html) action in a Lambda in a contact flow\.

1. Depending on your use case, place the Lambda either immediately after starting the chat \(at the beginning of the flow\) or right before routing the contact to a queue\.

## Customize the customer's chat user interface for a disconnect event<a name="chat-timeouts-ui"></a>

To customize your customer's chat user interface for a disconnect event, see the following methods in the [ChatJS](https://github.com/amazon-connect/amazon-connect-chatjs):
+ `onParticipantIdle(callback)`
+ `onParticipantReturned(callback)`
+ `onAutoDisconnection(callback)`

Use these methods to register callback handlers which are triggered when the new events arrive\.