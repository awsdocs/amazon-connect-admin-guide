# Port your current phone number<a name="port-phone-number"></a>

To continue to use your current United States phone number with Amazon Connect, you can submit a support ticket to port the number to Amazon Connect\. The Amazon Connect team processes your request and assists you with the number porting process\. After a number is ported to Amazon Connect, it automatically appears in the list of available numbers to be assigned to contact flows\.

Porting phone numbers typically takes between two to four weeks after you submit the required information\. The amount of time depends on the complexity of the request and your current carrier\. Porting toll\-free numbers, or requests to port a large quantity of numbers at one time, usually take longer than porting local, direct dial numbers\.

We recommend that you select a phone number from Amazon Connect so you can become familiar with the service while waiting for your number to be ported\.

## Premium support plan instructions<a name="premium-support-plan"></a>

**To port your current phone number to Amazon Connect**

1. Log in to the [AWS Management Console](https://console.aws.amazon.com/console) \(https://console\.aws\.amazon\.com/console\) using your AWS account\. 

1. In the upper right corner of the page, choose **Support**, **Support Center**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/support-dropdown.png)

1. On the **AWS Support Center** page, choose **Create case**\.

1. Choose **Technical Support**\.

1. Under **Case classification**, do the following:

   1. Choose service as **Connect \(Contact center\)**\.

   1. Choose category as **Phone Number Porting**\.

   1. Choose the required severity\.

   1. For **Contact Center Instance ARN**, enter the instance ARN \(also called the instance ID\)\. For instructions on how to find your instance ARN, see [Find your Amazon Connect instance ID/ARN](find-instance-arn.md)\. 

   1. Enter the subject\.

   1. Under **Case description**, **Use case description**, include as much information as possible about your request, including phone number\(s\) to be ported, your current carrier, and the contact information for the person authorized to make changes to your current phone service\. If you don't know all of these details, you can leave information out\.

1. Expand **Contact options**, and then choose your **Preferred contact language** and **Contact methods**\.

1. Choose **Submit**\.

**Tip**  
After a phone number is ported to Amazon Connect, it appears in the list of available phone numbers for you to assign to contact flows\. 

## Basic support plan instructions<a name="basic-support-plan"></a>

**To port your current phone number to Amazon Connect**

1. Log in to the [AWS Management Console](https://console.aws.amazon.com/console) \(https://console\.aws\.amazon\.com/console\) using your AWS account\. 

1. In the upper right corner of the page, choose **Support**, **Support Center**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/support-dropdown.png)

1. On the **AWS Support Center** page, choose **Create case**\.

1. Choose **Service limit increase**\.

1. Under **Case details**, do the following:

   1. For **Limit type**, choose **Amazon Connect**\.

   1. For **Contact Center Instance ARN \- optional**, enter the instance ARN \(also called the instance ID\)\. For instructions on how to find your instance ARN, see [Find your Amazon Connect instance ID/ARN](find-instance-arn.md)\.

1. Under **Requests**, **Request 1** do the following:

   1. For **Region**, select the Region in which you created your Amazon Connect instance\.

   1. For **Limit**, choose **Phone Number Porting**\.

   1. For **New limit value**, enter the number of phone numbers to port\.

1. \(Optional\) If you want to port more phone numbers, choose **Add another request**, and then repeat step 6 for each additional request\.

1. Under **Case description**, **Use case description**, include as much information as possible about your request, including whether the numbers are Direct Inward Dial or toll\-free, your current carrier, and the contact information for the person authorized to make changes to your current phone service\. If you don't know all of these details, you may leave information out\.

1. Expand **Contact options**, and then choose your **Preferred contact language** and **Contact methods**\.

1. Choose **Submit**\.

**Tip**  
After a phone number is ported to Amazon Connect, it appears in the list of available phone numbers for you to assign to contact flows\. 

## Porting phone numbers in other countries<a name="porting-numbers-outside-of-usa"></a>

If you are trying to port a number outside of the United States, follow the same steps for porting numbers, however, the timeline to complete may vary\. If porting is not possible at all, AWS support will let you know that it's not available\. 

## About porting phone numbers<a name="about-porting"></a>

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

## Port phone numbers away from Amazon Connect<a name="port-away"></a>

To port your number\(s\) to a different carrier, please open a support case telling us that's what you're going to do\. Then make arrangements with your new carrier\. By letting us know, it will reduce the amount of back and forth between us and your new carrier, and it will make the process go faster\. 

1. [Create a case](https://console.aws.amazon.com/support/cases#/create)\.

1. Choose **Service limit increase**\.

1. In **Limit type** select **Amazon Connect**\.

1. In **Use case description**, let us know that you're porting your number away and the name of your new carrier\. 