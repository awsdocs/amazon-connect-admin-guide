# Add a chat user interface to your website<a name="add-chat-to-website"></a>

To support your customers through chat, you can add a chat widget to your website that is hosted by Amazon Connect\. You can configure the chat widget in the Amazon Connect console: customize the font and colors, and secure the widget so that it can be launched only from your website\. As a result, you will have a short code snippet that you add to your website\. 

Because Amazon Connect hosts the widget, it ensures that the latest version is always live on your website\. 

**Tip**  
Use of the chat widget is subject to default Service Quotas, such as the number of characters allowed per message\. Before launching your chat widget into production, make sure that your Service Quotas are set for your organization's needs\. For more information, see [Amazon Connect service quotas](amazon-connect-service-limits.md)\. 

## Supported browsers<a name="chat-widget-supported-browsers"></a>

The pre\-built chat widget supports the following browser versions and higher: 
+ Google Chrome 85\.0
+ Safari 13\.1
+ Microsoft Edge version 85
+ Mozilla Firefox 81\.0

## Step 1: Customize your chat widget<a name="customize-chat-widget"></a>

In this step, you customize the experience of the chat widget for your customers\.

1. Open the Amazon Connect dashboard, and choose **Customize chat widget**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/chatwidget-customize-chat-window-button.png)

1. On the **Customize chat widget** page, under **Global typeface**, use the dropdown to choose the font for the text that will appear in the chat widget\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/chatwidget-choose-font.png)

1. Under **Chat widget**, choose the colors for the widget header, chat message bubbles, and launch and minimize icons by entering hex values \([HTML color codes](https://htmlcolorcodes.com/)\) that align the chat widget with your website branding\. 

   As you choose colors, the chat preview updates automatically so that you can see what your widget will look like\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/chatwidget-choose-colors.png)

1. For **Minimize chat icon**, select the colors for the icon that customers will click or tap to minimize the chat widget\. 

1. For **Open chat icon**, select the colors for the icon that customers will click or tap to start a chat with your contact center\. 

1. Under **Select contact flow**, choose the inbound flow that initiates when a customer starts a chat\.

1. Choose **Next**\.

## Step 2: Specify the website domains where you expect to display the chat widget<a name="chat-widget-domains"></a>

1. Enter the website domains where you want to place the chat widget\. Chat loads only on websites that you select in this step\. 

   Choose **Add domain** to add up to five domains\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/chatwidget-add-domain.png)
**Important**  
Double\-check that your website URLs are valid and does not contain errors\. Include the full URL starting with https://\.
We recommend using https:// for your production websites and applications\.

1. Under **Add security for your chat widget**, we recommend choosing **Yes**, and working with your website administrator to set up your web servers to issue JSON Web Tokens \(JWTs\) for new chat requests\. This provides you more control when initiating new chats, including the ability to verify that chat requests sent to Amazon Connect are from authenticated users\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/chatwidget-choose-security.png)

   Choosing **Yes** results in the following:
   + Amazon Connect provides a 44\-character security key on the next page that you can use to create JWTs\.
   + Amazon Connect adds a callback function within the chat widget embed script that checks for a JWT when a chat is initiated\.

     You must implement the callback function in the embedded snippet, as shown in the following example\.

     ```
     amazon_connect('authenticate', function(callback) {
       window.fetch('/token').then(res => {
         res.json().then(data => {
           callback(data.data);
         });
       });
     });
     ```

   If you choose this option, in the next step you'll get a security key for all chat requests initiated on your websites\. Ask your website administrator to set up your web servers to issue JWTs using this security key\. 

1. Choose **Save**\.

## Step 3: Confirm and copy chat widget code and security keys<a name="confirm-and-copy-chat-widget-script"></a>

In this step, you confirm your selections and copy the code for the chat widget and embed it in your website\. If you chose to use JWTs in [Step 2](#chat-widget-domains), you can also copy the secret keys for creating them\. 

### Security key<a name="chat-widget-security-key"></a>

Use this 44\-character security key to generate JSON web tokens from your web server\. You can also update, or rotate, keys if you need to change them\. When you do this, Amazon Connect provides you with a new key and maintains the old key until you have a chance to replace it\. After you have the new key deployed, you can come back to Amazon Connect and delete the old key\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/chatwidget-security-key.png)

When your customers interact with the start chat icon on your website, the chat widget requests your web server for a JWT\. When this JWT is provided, the widget will then include it as part of the end customer’s chat request to Amazon Connect\. Amazon Connect then uses the secret key to decrypt the token\. If successful, this confirms that the JWT was issued by your web server and Amazon Connect routes the chat request to your contact center agents\.

#### JSON web token specifics<a name="jwt"></a>
+ Algorithm: **HS256**
+ Claims: 
  + **sub**: *widgetId*

    Replace `widgetId` with your own widgetId\. To find your widgetId, see the example [Chat widget script](#chat-widget-script)\.
  + **iat**: \*Issued At Time\.
  + **exp**: \*Expiration \(10 minute maximum\)\.

  \* For information about the date format, see the following Internet Engineering Task Force \(IETF\) document: [JSON Web Token \(JWT\)](https://tools.ietf.org/html/rfc7519), page 5\. 

The following code snippet shows an example of how to generate a JWT in Python:

```
payload = {
'sub': widgetId, // don't add single quotes, such as 'widgetId'
'iat': datetime.utcnow(),
'exp': datetime.utcnow() + timedelta(seconds=JWT_EXP_DELTA_SECONDS)
}

header = {
'typ': "JWT",
'alg': 'HS256'
}

encoded_token = jwt.encode((payload), CONNECT_SECRET, algorithm=JWT_ALGORITHM, headers=header) // CONNECT_SECRET is the security key provided by Amazon Connect
```

### Chat widget script<a name="chat-widget-script"></a>

The following image shows an example of the JavaScript that you embed on the websites where you want customers to chat with agents\. This script displays the widget in the bottom\-right corner of your website\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/chatwidget-code.png)

1. An example of where to find your widgetId\.

When your website loads, customers first see the **Start Chat** icon\. When they choose this icon, the chat widget opens and customers are able to send a message to your agents\.

To make changes to the chat widget at any time, choose **Edit**\.

**Note**  
Saved changes update the customer experience in a few minutes\. Confirm your widget configuration before saving it\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/chatwidget-edit.png)

To make changes to widget icons on the website, you will receive a new code snippet to update your website directly\.

### More customizations for your chat widget<a name="chat-widget-more-customizations"></a>

See the following topics for more you can do to customize the chat experience:
+ [Pass the customer display name when a chat initializes](pass-display-name-chat.md)
+ [Pass contact attributes when a chat initializes](pass-contact-attributes-chat.md)