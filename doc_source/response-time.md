# Investigate response time during chats<a name="response-time"></a>

Use the response time metric to understand the responsiveness of the agent or customer during a chat contact\.

Contact Lens calculates the following metrics:
+ **Agent greeting time**\. This is the first response time for the agent, which is how fast the agent engaged with the customer after the agent joined the chat\. A long first response time may explain, for example, if a customer has a negative sentiment in the beginning of conversation\.
+ **Avg agent response time** and **Avg customer response time**\. The agent response time helps you check an agent's performance against your organization's base line\.
+ **Max agent response time** and **Max customer response time**\.

  The customer's max response time may explain an agent's response time\. For example, if a customer didn't reply for five minutes and then sent a message, it's possible the agent took longer than usual to respond because they were handling other chats at the same time\. 

We recommend examining the response time metrics in conjunction with the interactions graph that shows gaps in conversation and participant sentiment\.

You can choose \(or click\) or tap the longest response time value on the graph to be directed to the associated message in the transcript\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contactlens-contactdetails-chat1b.png)

For more information, see [Search by response time for chat conversations](search-conversations.md#response-time-search)\.