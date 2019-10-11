# Sample Secure Input with No Agent<a name="sample-secure-input-with-noagent"></a>

Type: Contact flow \(inbound\)

This contact flow shows you how to capture sensitive customer data and encrypt it using a key\. Here's how it works:

1. The customer’s credit card number is stored using **Store customer input** block\. This block also encrypts the data using a signing key that must be uploaded in a \.pem format\. 

   In the **Set contact attributes** block, the encrypted card number is set as contact attribute\.

1. After the card number is successfully set as contact attribute, the customer is transferred back to the [](sample-inbound-flow.md)\. 