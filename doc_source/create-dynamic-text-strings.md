# Create dynamic text strings in prompts<a name="create-dynamic-text-strings"></a>

Use a **Play prompt** block to use an audio file to play as a greeting or message to callers\. You can also use contact attributes to specify the greeting or message delivered to callers\. To use the values of a contact attribute to personalize a message for a customer, include references to stored or external contact attributes in the text\-to\-speech message\. For example, if you retrieved the customer’s name from a Lambda function, and it returns values from your customer database for FirstName and LastName, you could use these attributes to say the customer’s name in the text\-to\-speech block by including text similar to the following:

Hello $\.External\.FirstName $\.External\.LastName, thank you for calling\.

Alternatively, you could store the attributes returned from the Lambda function using a **Set contact attributes** block, and then reference the user\-defined attribute created in the text to speech string\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/play-prompt-attribute.png)