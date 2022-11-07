# Sample AB test<a name="sample-ab-test"></a>

**Note**  
This topic explains a sample flow that is included with Amazon Connect\. For information about locating the sample flows in your instance, see [Sample flows](contact-flow-samples.md)\. 

Type: Flow \(inbound\)

This flow shows how to perform an A/B call distribution based on a percentage\. Here's how it works: 

1. The **Play prompt** block uses Amazon Polly, the text\-to\-speech service, to say "Amazon Connect will now simulate rolling dice by using the Distribute randomly block\. Now rolling\."

1. The contact reaches the **Distribute by percentage** block, which routes the customer randomly based on a percentage\.

   **Distribute by percentage** simulates a dice roll, resulting in a values between 2 to 12 with different percentages\. For example, there is 3 percent chance for the "2" option, 6 percent chance for the "3" option, and so on\. 

1. After the contact gets routed, the **Play prompt** tells the customer which number the dice rolled\.

1. At the end of the sample, the **Transfer to flow** block transfers the customer back to the [Sample inbound flow](sample-inbound-flow.md)\.