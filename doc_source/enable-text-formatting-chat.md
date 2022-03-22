# Enable text formatting for your customer's chat experience<a name="enable-text-formatting-chat"></a>

With Amazon Connect message formatting, you can enable your customers and agents to quickly add structure and clarity to their chat messages\. 

You can provide the following types of formatting on both the chat user interface and the agent application using markdown:
+ Bold
+ Italic 
+ Bulleted list
+ Numbered list
+ Hyperlinks
+ Attachments\. To enable attachments, follow [Enable attachments to share files using chat](enable-attachments.md)\.

## How to enable message formatting<a name="how-to-enable-message-formatting"></a>

1. When you create a new [chat user interface](add-chat-to-website.md), rich text formatting is enabled out of the box\. No additional configuration is required\.

1. To add text formatting capabilities to an existing [chat user interface](add-chat-to-website.md), update the [chat widget code](add-chat-to-website.md) with the following code that is highlighted in bold: 

   ```
       (function(w, d, x, id){
           s=d.createElement('script');
           s.src='https://d3xxxx.cloudfront.net/amazon-connect-chat-interface-client.js';
           s.async=1;
           s.id=id;
           d.getElementsByTagName('head')[0].appendChild(s);
           w[x] =  w[x] || function() { (w[x].ac = w[x].ac || []).push(arguments) };
       })(window, document, 'amazon_connect', 'widget-id');
       amazon_connect('styles', { openChat: { color: 'white', backgroundColor: '#123456'}, closeChat: { color: 'white', backgroundColor: '#123456'} });
       amazon_connect('snippetId', 'snippet-id');
       amazon_connect('supportedMessagingContentTypes', [ 'text/plain', 'text/markdown' ]);
   ```

   The code that is highlighted in red is set to the correct values when you get the snippet from the Amazon Connect console\. The only content you choose to add or remove is the last line in bold for `supportedMessagingContentTypes`\. 

1. To add text formatting capabilities to your own custom chat user interface \(for example, [Chat Interface](https://github.com/amazon-connect/amazon-connect-chat-interface) or your own UI solution on top of [ChatJS](https://github.com/amazon-connect/amazon-connect-chatjs)\), follow these steps: 

   1. Call the [StartChatContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html) API\. When calling `StartChatContact`, add the `SupportedMessagingContentTypes` parameter as shown in bold in the following example:

      ```
      // Amazon Connect StartChatContact API
      {
          "Attributes": { 
              "string" : "string" 
          },
          "ClientToken": "string",
          "ContactFlowId": "your contact flow ID",
          "InitialMessage": { 
              "Content": "string",
              "ContentType": "string"
          },
          "InstanceId": "your instance ID",
          "ParticipantDetails": { 
              "DisplayName": "string"
          }
          
          // optional
         "SupportedMessagingContentTypes": [ "text/plain", "text/markdown" ]
      }
      ```

   1. Import `chatjs` as an object, as shown in the following example:

      ```
      import "amazon-connect-chatjs";
      
      this.session = connect.ChatSession.create({
            ...
          });
      
      this.session.sendMessage({
            message: "message-in-markdown-format",
            contentType: "text/markdown"
      });
      ```

      If you don't use ChatJs, see these topics for information about sending markdown text through Amazon Connect APIs: [StartChatContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html) and [SendMessage](https://docs.aws.amazon.com/connect-participant/latest/APIReference/API_SendMessage.html)\.

   1. Send messages with markdown\. See the previous code snippet for importing `chatjs` as an object for an example of how to send messages\. You can use simple markdown for formatting text in chats\. If you're already [using chatjs today to send plaintext messages](https://github.com/amazon-connect/amazon-connect-chatjs/blob/master/src/core/chatController.js#L66) you can modify your existing logic to call [SendMessage](https://docs.aws.amazon.com/connect-participant/latest/APIReference/API_SendMessage.html) with `text/markdown` as `contentType` instead of `text/plain` when you want to send markdown messages\. Be sure to update the `sendMessage` parameter to have the markdown format of your messages\. For more information, see [Markdown Guide Basic Syntax](https://www.markdownguide.org/basic-syntax/)\.

   1. Implement your own logic in the UI package to render markdown messages in the input area and chat transcript\. If you use React, you can use [react\-markdown](https://github.com/remarkjs/react-markdown) as a reference\.

**Note**  
Text formatting capabilities appear to your agent only if the feature has been enabled for your customer in the chat user interface\. If text formatting is not supported or enabled on the customer chat user interface, the agent will not have the ability to compose and send messages with text formatting\.