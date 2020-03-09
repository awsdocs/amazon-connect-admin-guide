# Sample Secure Input with Agent<a name="sample-secure-input-with-agent"></a>

Type: Queue transfer

This contact flow shows you how to allow customers to input sensitive data while putting the agent on hold\. In a production environment, we recommend [using encryption](encrypt-data.md) instead of this solution\. 

Here's how it works: 

1. This flow begins with checking the customer's channel\. If they are using chat, they are put in a queue\.

1. If they are using voice, the agent and customer are put in a conference call\.

1. A **Play prompt** tells the customer that the agent will be put on hold while customer enters their credit card information\. 

1. When the prompt is finished playing, the agent is put on hold using a **Hold customer or agent** block\. If an error occurs, a prompt is played that agent was unable to put on hold, after which the contact flow is ended\.

1. The customer's input is stored using the **Store Customer Input** block\. This block encrypts the sensitive customer information using a signing key that must be uploaded in \.pem format\. For a detailed walkthrough that explains how to encrypt customer input, see [Creating a secure IVR solution with Amazon Connect](https://aws.amazon.com/blogs/contact-center/creating-a-secure-ivr-solution-with-amazon-connect/)\.

1. After the customer's data is collected, the agent and customer are put back on call using the **Conference All** option in another **Hold customer or agent** block\. 

1. The error branch runs if there's an error while capturing the customer's data\.