# Phone Numbers for Your Contact Centers<a name="contact-center-phone-number"></a>

After you create an Amazon Connect instance, you can claim a phone number to use for your contact center\. After you claim a number, you can place a test call in to your contact center to confirm that it is working correctly\. If you want to keep a phone number you already have, you can port the phone number and use it with Amazon Connect\.

Calls are handled in the contact center using the Contact Control Panel \(CCP\)\. The CCP is built in to the Amazon Connect Contact Center Manager \(CCM\)\. For more information, see [Amazon Connect Contact Control Panel](amazon-connect-contact-control-panel.md)\.

**Topics**
+ [Claim a Phone Number](#claim-phone-number)
+ [Associate a Phone Number with a Contact Flow](#associate-phone-number)
+ [Port Your Current Phone Number](#port-phone-number)
+ [Phone Numbers for Asia Pacific \(Tokyo\)](connect-tokyo-region.md)

## Claim a Phone Number<a name="claim-phone-number"></a>

To place or receive calls in your instance, you need to claim a phone number\. If you did not claim a number when you created the instance, follow these steps to claim one now\.

**To claim a number for your contact center**

1. Log in to your contact center using your access URL \(https://*domain*\.awsapps\.com/connect/login\)\.

1. Choose **Routing**, **Phone numbers**\.

1. Choose **Claim a number**\. You can choose a toll free number or a Direct Inward Dialing \(DID\) number\.
**Note**  
If you select a country, but there are no numbers displayed for that country, you can request additional numbers for the country using the [Amazon Connect service limits increase form](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-connect)\.

1. Enter a description for the number and, if required, attach it to a contact flow in **Contact flow / IVR**\.

1. Choose **Save**\.

1. Repeat this process until you have claimed all your required phone numbers\.

There is a service limit of 10 phone numbers per Amazon Connect instance\. If you reach your limit, but want a different phone number, you can release one of previously claimed numbers\. You cannot claim the same phone number after releasing it\. If you need more than 10 phone numbers, you can request a service limit increase using the [Amazon Connect service limits increase form](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-connect)\.

## Associate a Phone Number with a Contact Flow<a name="associate-phone-number"></a>

You can attach contact flows to phone numbers\. You cannot assign a contact flow to a phone number until the contact flow is published\.

**To associate a phone number with a contact flow**

1. Log in to your contact center using your access URL \(https://*domain*\.awsapps\.com/connect/login\)\.

1. Choose **Routing**, **Phone numbers**\.

1. You can search for a specific number, filter your search by queue, or select a number from the list provided \(if applicable\)\.

1. Select the number to edit, expand **Contact flow / IVR**, and select the contact flow\.

1. Choose **Save**\.

## Port Your Current Phone Number<a name="port-phone-number"></a>

To continue to use your current United States phone number with Amazon Connect, you can submit a support ticket to port the number to Amazon Connect\. The Amazon Connect team processes your request and assists you with the number porting process\. 

Porting phone numbers typically takes between two to four weeks after you submit the required information\. The amount of time depends on the complexity of the request and your current carrier\. Porting toll\-free numbers, or requests to port a large quantity of numbers at one time, usually take longer than porting local, direct dial numbers\.

We recommend that you select a phone number for Amazon Connect so that you can become familiar with the service while waiting for your number to be ported\.

**To port your current phone number to Amazon Connect**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. Log in with the account used to create the Amazon Connect instance to which to port your current number\.

1. Choose **Support**, **Support Center**\.

1. On the **Support Center** page, choose **Create Case**\.

1. Fill in values for the following fields:
   + For **Regarding**, choose **Service Limit Increase**\.
   + For **Limit Type**, choose **Connect**\.
   + For **Region**, select the Region in which you created your Amazon Connect instance\.
   + For **Limit**, choose **Phone Number Porting**\.
   + For **New limit value**, enter the number of phone numbers to port\.
   + For **Use Case Description**, include as much information as possible about your request, including whether the numbers are Direct Inward Dial or toll\-free, your current carrier, and the contact information for the person authorized to make changes to your current phone service\. If you do not know all of these details, you may leave information out\.

1. Fill in the rest of the form, and choose **Submit**\.

### About Porting Phone Numbers<a name="about-porting"></a>

When you port your current phone number into Amazon Connect, we provide any possible assistance\. However, many of the steps are performed by telecommunications carriers\. 

We collect the information necessary to verify that you are authorized to port the numbers that you request\. We pass that information on to your existing carrier, and coordinate with the new carrier to get your number ported\. Each carrier has their own process and requirements for number porting\. Your number cannot be ported until your current carrier verifies that you own and are authorized to port the numbers requested\. Your current carrier must approve the request to port your number before the new carrier can provision the number\. After that is complete, the Amazon Connect team can start configuring your Amazon Connect instance to use the ported numbers\.

The steps in the porting process are as follows:

1. Submit a support ticket to port your number\.

1. Confirm number portability\. The Amazon Connect team confirms whether the numbers that you request can be ported from your current carrier\. We then contact you with next steps, or notify you that the requested numbers cannot be ported\.

1. Complete the Letter of Authorization/Agency \(LOA\)\. When you complete the LOA form, the information you provide must match the information on file with your current carrier\. If the information does not match, it may delay the porting of your number\. The LOA form authorizes your current carrier to release your number and allow it to be ported\. If your number can be ported, we provide you with an LOA form appropriate for the type of number to port\. There are different forms for local, Direct Inward Dial \(DID\), and toll\-free numbers\. If you are porting multiple numbers from different carriers, fill out a separate form for each carrier\.

   On the LOA form, include the following: 
   + The numbers to port
   + Information about your current carrier, such as a phone bill
   + Contact information for the person authorized to make changes to your phone service

1. To get the port started, the Amazon Connect team submits the LOA to the carrier for Amazon Connect on your behalf\. The new carrier works with your current carrier to move your current number over to their service\. This step typically takes 3–5 business days\.

   If your current carrier is able to validate and approve your request, they provide a date for the number to be ported to Amazon Connect\.

   If your current carrier rejects the request to port your number due to the LOA not having correct or complete information, the Amazon Connect team contacts you and requests a new LOA to submit to the carrier\.

When we receive a date from your current carrier, we start adding the numbers to your Amazon Connect instance about a day before the scheduled date\.