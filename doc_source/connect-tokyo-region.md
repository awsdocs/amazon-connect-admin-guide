# Claim Phone Numbers for Amazon Connect in the Asia Pacific \(Tokyo\) Region<a name="connect-tokyo-region"></a>

The steps necessary to claim a phone number for an Amazon Connect instance you create in the Asia Pacific \(Tokyo\) Region are different than the steps to claim a phone number in other AWS Regions\. Use the information in this section to claim a phone number for your instance\. Amazon Connect does not support porting phone numbers in the Asia Pacific \(Tokyo\) Region at this time\.

## Port and Protocol Requirements for Using Amazon Connect in the Asia Pacific \(Tokyo\) Region<a name="tokyo-ports"></a>

If your agents use a softphone for Amazon Connect, you must allow traffic in both directions between the network on which the CCP is running and the Amazon Connect for the region in which you created your instance\. The required addresses for instances created in the Asia Pacific \(Tokyo\) Region Region include the following:


| Protocol | Port | Transport Layer | IP Range | 
| --- | --- | --- | --- | 
| HTTP | 80 | TCP | AWS EC2 and CLOUDFRONT ranges in [https://ip\-ranges\.amazonaws\.com/ip\-ranges\.json](https://ip-ranges.amazonaws.com/ip-ranges.json)\. | 
| HTTPS | 443 | TCP | AWS EC2 and CLOUDFRONT ranges in [https://ip\-ranges\.amazonaws\.com/ip\-ranges\.json](https://ip-ranges.amazonaws.com/ip-ranges.json)\. | 
| TURN/STUN | 3478 and 49152\-65535 | UDP | AMAZON\_CONNECT ranges in [https://ip\-ranges\.amazonaws\.com/ip\-ranges\.json](https://ip-ranges.amazonaws.com/ip-ranges.json)\. | 
| TURN relay media | 80 and 443 | UDP and TCP | AMAZON\_CONNECT ranges in [https://ip\-ranges\.amazonaws\.com/ip\-ranges\.json](https://ip-ranges.amazonaws.com/ip-ranges.json)\. | 

## Using Amazon Connect in the Asia Pacific \(Tokyo\) Region<a name="using-connect-tokyo"></a>

Amazon Connect supports the following phone numbers for instances created in the Asia Pacific \(Tokyo\) Region\.
+ **Direct Inward Dialing \(DID\) numbers**—DID numbers are also referred to as local numbers\.
  + 050 prefix numbers\.
  + 03 prefix for numbers in Tokyo\. Amazon Connect does not offer phone numbers for other cities in Japan at this time\.

    To claim a number with a 03 prefix, you must provide documentation to verify that you have a physical address in Tokyo\. See the next section for more information\.
+ **Toll Free numbers**
  + 0120 prefix numbers\.
  + 0800 prefix numbers\.

**Note**  
When you claim a toll free phone number for Amazon Connect, there is no corresponding DID number with a 03 prefix also assigned, as with other toll free numbers in Japan\. If you need to use a DID number, you can claim one in Amazon Connect\.

## How to Claim a Phone Number for Amazon Connect Instances in the Asia Pacific \(Tokyo\) Region<a name="claim-number-tokyo"></a>

You can claim a 050 prefix number directly within Amazon Connect\. If you plan to use a number with a 03 prefix from Tokyo, pursuant to Japanese regulatory requirements, you must submit an [Amazon Connect service limits increase form](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-connect) to request an number with a 03 prefix for your instance\. As part of the approval process, you must provide proof of address documentation to confirm that you have an address in Tokyo\. The documents required for address verification are described later in this topic\.

While you wait for the request to be processed, you can claim a number with a 050 prefix for your instance\. This helps you become familiar with how to configure and use Amazon Connect\. When your service limit increase for a 03 prefix number is approved, you can then follow step 6 to search for a “3” prefix number and claim it\. After the service limit increase is approved, you will be able to claim additional 03 prefix numbers in the **Claim phone number **page for that specific account moving forward without opening another support case\. 

Use these steps to claim a phone number for an instance you create in the Asia Pacific \(Tokyo\) Region\.

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

   You may need to sign in to your AWS account\. Confirm that the Region selected is Asia Pacific \(Tokyo\)\.

1. On the Amazon Connect console page, choose the **Access URL** for the instance for which to claim a phone number\.

1. Using an account that is assigned the Admin security profile in Amazon Connect, log in to the instance\.

1. On the Amazon Connect dashboard, if you have not yet claimed a phone number, follow step 5\. If you have already claimed a number, and are claiming an additional number, go to step 6\.

1. If you have not yet claimed a number for your instance, choose **Begin** and follow these steps\. If you have already claimed a number for your instance, and are claiming an additional number, skip to the next step\.

   1. On the **Claim phone number** page, choose the country from which to claim a phone number\.

      Note that only 050 prefix number are available to claim for instances in the Asia Pacific \(Tokyo\) Region\. To claim a 03 prefix number for Tokyo, you must submit a [Amazon Connect service limits increase form](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-connect)\.

   1. Choose the type of number to claim, **Direct Dial** or **Toll Free**\.

   1. Choose the phone number to use for your instance from the **Phone number** drop\-down menu\.

   1. Choose **Next**\.

      If you see the following message displayed, you must request approval to claim the number selected using the link provided\.

      *To claim a number in the selected country, please provide a valid business address in that country\. Numbers that are claimed without providing a valid local business address may be revoked\. To provide the address, please create a support case\. Click here to create a support case now\.*

   1. To place a test call to confirm that the number is working correctly with your instance, follow the guidance on the page, or choose **Skip for now**\. 

1. If you have already claimed a number for your instance, and are claiming an additional number, choose **View phone numbers** and then follow these steps\.

   1. On the **Manage Phone numbers** page, choose **Claim a number**\.

   1. On the **Claim Phone number** page, choose the tab for the type of number to claim, **Toll free** or **DID \(Direct Inward Dialing\)**\.

   1. Select the country from the drop\-down menu from which to claim a phone number\. Up to five numbers available in that country are displayed\. If you want to find a number from a specific prefix, type all or part of the prefix in the Prefix field\. If there are numbers with that prefix available, they are displayed on the page\.

   1. Choose the number to claim for your instance\.

   1. Optionally, enter a description for the number to help you identify it later\.

   1. To associate the number with a contact flow, choose the flow in the **Contact flow / IVR** drop\-down menu\. When you associate a number with a flow, the selected contact flow is invoked when a call comes in to your instance on that phone number\.

## Proof of Address Requirements for 03 Prefix Numbers<a name="proof-of-address-tokyo"></a>

When you submit a request to claim a 03 prefix number from Tokyo to use for your Amazon Connect instance, you must provide the following documentation as proof of address due to Japanese regulations as follows:
+ If the AWS account used to create the Amazon Connect instance is for an individual, the individual must provide a valid, government\-issued identification document, such as a national ID card, passport, or driver's license, with an address visible on the document that matches the city from which the phone number is assigned\.
+ If the AWS account used to create the instance is for an organization, a representative of the organization must provide the both of the following:
  + A valid, government\-issued identification document, such as a national ID card, passport, or driver's license\.
  + One of the following documents, with an address visible on the document that matches the city from which the number is assigned\. This can be a utility bill, a certificate of company registration from the Ministry of Justice, receipts of payments to a government entity, such as a national or local tax return, or a social security payment receipt\.

You can include copies of these documents with your support request for the number, or provide them when requested by AWS Support\. After you submit the request, AWS Support reviews it, and then resolves the ticket when address validation is confirmed or if more information is needed\. AWS Support will contact you with the results of your request when it is completed\. Once AWS Support resolves the ticket, and address validation is confirmed you can then follow step 6 above to claim a Tokyo 03 prefix number\.