# Pass contact attributes when a chat initializes<a name="pass-contact-attributes-chat"></a>

You can use [contact attributes](what-is-a-contact-attribute.md) to capture information about the contact who is using the chat widget\. Then, you can display that information to the agent through the Contact Control Panel \(CCP\), or use it elsewhere in the flow\.

For example, you can customize your contact flow to say the name of the customer in your welcome message\. Or, you can use attributes specific to your business, such as account/member IDs, customer identifiers like names and emails, or other metadata associated with a contact\.

## How to pass contact attributes into the chat widget<a name="how-to-contact-attributes-chatwidget"></a>

1. Enable security in the chat widget as described in [Add a chat user interface to your website](add-chat-to-website.md), if you haven't already:

   1. In Step 2, under **Add security for your chat widget**, choose **Yes**\.

   1. In Step 3, use the security key to generate JSON web tokens\.

1. Add the contact attributes to the payload of your JWT as an `attributes` claim\.

   Following is an example of how you might generate a JWT with contact attributes in Python:

   ```
   import jwt
   
   CONNECT_SECRET = "your-securely-stored-jwt-secret"
   
   payload = {
     'sub': 'widget-id',
     'iat': datetime.datetime.utcnow(),
     'exp': datetime.datetime.utcnow() + datetime.timedelta(seconds=500),
     'attributes': {"name": "Jane", "memberID": "123456789", "email": "Jane@example.com", "isPremiumUser": "true", "age": "45"}
   }
   
   header = {
     'typ': "JWT",
     'alg': 'HS256'
   }
   
   encoded_token = jwt.encode((payload), CONNECT_SECRET, algorithm="HS256", headers=header)
   });
   ```

   In the payload, you must create a string key `attributes` \(as\-is, all lowercase\), with an object as its value\. That object must have string\-to\-string key\-value pairs\. If anything other than a string is passed in any one of the attributes, the chat will fail to start\. 

   The contact attributes must follow the limitations set by the [StartChatConnect](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html#connect-StartChatContact-request-Attributes) API: 
   + Keys must have a minimum length of 1
   + Values can have a minimum length of 0

## Things you need to know<a name="contact-attributes-chatwidget-important-notes"></a>
+ The chat widget has a 6144 bytes limit for the entire encoded token\. Because JavaScript uses UTF\-16 encoding, 2 bytes are used per character, so the maximum size of the `encoded_token` should be around 3000 characters\.
+ The encoded\_token should be passed in to `callback(data)`\. The `authenticate` snippet does not need any additional changes\. For example:

  ```
  amazon_connect('authenticate', function(callback) {
    window.fetch('/token').then(res => {
      res.json().then(data => {
        callback(data.data);
      });
    });
  });
  ```
+ Using a JWT to pass contact attributes ensures the integrity of the data\. If you safeguard the shared secret and follow appropriate security practices, you can help ensure that the data cannot be manipulated by a bad actor\.
+ Contact attributes are only encoded in the JWT, not encrypted, so it's possible to decode and read the attributes\. Sensitive data should not be passed in the token\. 