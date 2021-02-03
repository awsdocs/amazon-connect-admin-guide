# Sample secure input with no agent<a name="sample-secure-input-with-noagent"></a>

Type: Contact flow \(inbound\)

This contact flow shows you how to capture sensitive customer data and encrypt it using a key\. Here's how it works:

1. It begins by checking the contact's channel\. If they are using chat, a prompt is played that this doesn't work with chat, and they are transferred to [Sample inbound flow](sample-inbound-flow.md)\.

1. If they are using voice, the **Store customer input** block prompts them to enter their credit card number\. The block stores and also encrypts the data using a signing key that must be uploaded in a \.pem format\. 

   In the **Set contact attributes** block, the encrypted card number is set as contact attribute\.

1. After the card number is successfully set as contact attribute, the customer is transferred back to the [Sample inbound flow](sample-inbound-flow.md)\. 