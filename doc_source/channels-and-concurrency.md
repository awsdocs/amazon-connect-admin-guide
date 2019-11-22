# Channels and Concurrency<a name="channels-and-concurrency"></a>

Agents can be available concurrently on voice and chat channels at the same time\. Here's how this works: 

Suppose an agent is configured in their routing profile for voice and up to 5 chats\. When the agent logs in, they can be routed a chat or a voice call\. However, once they are on a voice call, no more voice calls or chats are routed to them until they finish the call\. 

If the agent accepts a chat first, up to 5 chats will be routed to them, but no voice calls\. Once they are done with the chats, they're available for the next contact, which can be voice or chat\. To learn more, see [How Routing Works](about-routing.md)\.

To learn more about what the agent experiences in the Contact Control Panel when handling multiple chats, see [Chat with Contacts](work-with-chats.md)\.