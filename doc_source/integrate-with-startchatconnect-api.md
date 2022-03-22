# Start chats using your own applications<a name="integrate-with-startchatconnect-api"></a>

You can use Amazon Connect APIs to start chats in your own applications\.

The [StartChatConnect ](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html) API is used to start the chat\.

When you explore the chat experience for the first time, you'll notice that chats aren't counted in the **Contacts Incoming** metric in your historical metrics report\. This is because the initiation method for the chat in the contact record is **API**\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ctr-api.png)

After a chat is transferred to an agent, the **Contacts Incoming** metric is incremented\. The contact record for the transfer no longer increments the API, but it does increment **Contacts Incoming**\. 