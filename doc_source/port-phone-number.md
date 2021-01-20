# Port your current phone number<a name="port-phone-number"></a>

To continue using your current phone number with Amazon Connect, you can submit a support ticket to port the number to Amazon Connect\. The Amazon Connect team processes your request and assists you with the number porting process\. 

## How long does it take to port numbers?<a name="how-long-for-number-porting"></a>

We recommend opening porting requests well in advance of pending go\-live dates\.
+ Porting US or Canada phone numbers usually takes between two to four weeks after you submit the required information\.
+ Porting non\-US phone numbers takes more than two weeks and possibly up to three months, depending on the country\. For example, most European countries take about two weeks\.
+ The amount of time it takes to port numbers depends on the complexity of the request and your current carrier\. For example: 
  + Porting 100 numbers from one carrier is usually faster than porting three numbers from three different carriers\.
  + Porting local, direct dial numbers is usually faster than porting toll\-free numbers\.
+ After a number is ported to Amazon Connect, the Support team maps your number to your connect instance for you to map to required flow\. You can also request that the Amazon Connect Support team map the number to your contact flow for you\.

## How to port your numbers<a name="about-porting"></a>

When you port your current phone number into Amazon Connect, we provide any possible assistance\. Many of the steps, however, are performed by telecommunications carriers\. 

1. **Submit an Amazon Connect support ticket to port your number\.**
   + [Premium support plan instructions](#premium-support-plan)
   + [Basic support plan instructions](#basic-support-plan)

1. **The Amazon Connect team reviews your ticket\.** 

   We confirm whether the numbers that you request can be ported from your current carrier\. We then contact you with next steps, or notify you that the requested numbers cannot be ported\. For common reasons, see see [Why carriers reject port requests](#why-port-request-rejected)\.

1. **Complete the Letter of Authorization/Agency \(LOA\)\.** 

   If your number can be ported, we provide you with an LOA form appropriate for the type of number to port\. The LOA form authorizes your current carrier to release your number and allow it to be ported\. 
   +  If you are porting multiple numbers from different carriers, fill out a separate LOA form for each carrier\.
   + The name, address, and information you provide on the LOA form must match the information on file with your current carrier exactly\. One way you can help ensure the porting process goes smoothly is to include a copy of the Customer Service Record \(CSR\) from your carrier, which has your name and address on it\. Check that the information on your LOA form matches your CSR exactly\.

   A LOA form has the following information:
   + The numbers to port\.
   + Information about your current carrier, such as a phone bill\.
   + Contact information for the person authorized to make changes to your phone service\.
**Important**  
Your LOA form must meet the following criteria:   
It must be legible: clearly written or typed\. 
It must list your company name, the company address, and contact name\. This information must match what is on the current carrier's CSR\.
It must include a true signature\. Most carriers reject an electronic or printed signature\.
It must be dated within 30 days of when the Amazon Connect Support team submits the LOA to the carrier\.
It must include any toll\-free numbers you want to port\. Up to 10 toll\-free numbers can be listed on the LOA\. 
A spreadsheet is required if you are requesting more than 10 toll\-free numbers be ported\. The LOA should specify "See Attached" and the spreadsheet should be attached to the LOA\.
It must include only those toll\-free numbers that belong to the same current carrier\. If you have multiple current carriers, you need to submit multiple LOAs\.

1. **The Amazon Connect team submits the LOA** to the carrier for Amazon Connect on your behalf\. 

1. **The new carrier works with your current carrier** to move your current number over to their service\.
   + If your current carrier is able to validate and approve your request, they provide a date for the number to be ported to Amazon Connect\.
   + If your current carrier rejects the request to port your number due to the LOA not having correct or complete information, the Amazon Connect team contacts you and requests a new LOA to submit to the carrier\.

     Every time we resubmit an LOA, there is an additional 3\-5 business days of waiting time\. Unfortunately, we cannot expedite the LOA acceptance/rejection process\. We must wait for a response from your current carrier\.

     For more information, see [Why carriers reject port requests](#why-port-request-rejected)\. 

1. **Amazon Connect contacts you with your porting date**\. When we receive a date from your current carrier, we start adding the numbers to your Amazon Connect instance about a day before the scheduled date\.

## Submit a port request<a name="submit-port-request"></a>

### Premium support plan instructions<a name="premium-support-plan"></a>

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

1. The Amazon Connect team reviews your ticket, and gets back to you with next steps\.

### Basic support plan instructions<a name="basic-support-plan"></a>

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

1. The Amazon Connect team reviews your ticket, and gets back to you with next steps\.

## Why carriers reject port requests<a name="why-port-request-rejected"></a>

Following are the most common reasons a port request may be initially rejected by your current carrier:
+ Unsatisfactory business relationship\.

  This usually means that you have an unpaid balance or the carrier charges a port away fee\. After you pay the bill or fee to your carrier, we will resubmit the port request\.
+ Name or address mismatch

  The information you submitted on your Letter of Authorization \(LOA\) is different from what's on file with your carrier in their Customer Service Record \(CSR\)\. To fix, contact your carrier to update your CSR information\. 

  Let us know when they update your information and we will resubmit the port request\. Or, send us a new LOA with the correct information\. 
+ Number cannot be ported

  Some numbers can't be ported due to specific country or carrier limitations\. In these situations, consider claiming a new number from Amazon Connect\.

## Porting phone numbers in other countries<a name="porting-numbers-outside-of-usa"></a>

If you are trying to port a number outside of the United States, follow the same steps for porting numbers, however, the timeline to complete may vary\. If porting is not possible at all, AWS support will let you know that it's not available\. 

## Port phone numbers away from Amazon Connect<a name="port-away"></a>

To port your number\(s\) to a different carrier, please open a support case telling us that's what you're going to do\. Then make arrangements with your new carrier\. By letting us know, it will reduce the amount of back and forth between us and your new carrier, and it will make the process go faster\. 

1. [Create a case](https://console.aws.amazon.com/support/cases#/create)\.

1. Choose **Service limit increase**\.

1. In **Limit type** select **Amazon Connect**\.

1. In **Use case description**, let us know that you're porting your number away and the name of your new carrier\. 