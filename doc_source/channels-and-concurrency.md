# Channels and concurrency<a name="channels-and-concurrency"></a>

Agents can be available concurrently on voice, chat, and tasks at the same time\. Here's how this works: 

Suppose an agent is configured in their routing profile for voice, up to 10 chats, and up to 10 tasks\. When the agent logs in, they can be routed a chat, task, or voice call\. However, once they are on a voice call, no more voice calls, chats, or tasks are routed to them until they finish the call\. 

If the agent accepts a chat first, up to 10 chats will be routed to them, but no voice calls or tasks\. Once they are done with the chats, they're available for the next contact, which can be voice, chat, or tasks\. To learn more, see [How routing works](about-routing.md)\.

To learn more about what the agent experiences in the Contact Control Panel when handling multiple chats, see [Chat with contacts](work-with-chats.md)\.