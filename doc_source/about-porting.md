# How to port your numbers to Amazon Connect<a name="about-porting"></a>

The following steps are for a typical porting request\. This process requires timely communication to make progress\. If you take longer than 30 days to respond to requests for information, your porting request may be cancelled, rescheduled, or restarted from the beginning\. For a list of country\-specific requirements for porting numbers, see [Region requirements for ordering and porting phone numbers](phone-number-requirements.md)\. 

## Step 1: Submit an Amazon Connect support ticket<a name="step1-porting"></a>

Submit an Amazon Connect support ticket to verify if your phone number can be ported to Amazon Connect\. 

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

## Step 2: Complete Letter of Authorization \(LOA\)<a name="step2-porting"></a>

If the phone number qualifies for porting, the Amazon Connect team will provide you a Letter of Authorization \(LOA\) to be completed by you\. Complete all mandatory fields and sign the LOA\.

 Along with the LOA, Telecom regulations in many countries require additional documents to register a number, such as proof of business, proof of address, and proof of ID\. For a list of country\-specific requirements for porting numbers, see [Region requirements for ordering and porting phone numbers](phone-number-requirements.md)\. 

### How to complete an LOA<a name="how-to-complete-loa"></a>

All portings require the completion of a Letter of Authorization \(LOA\)\. The LOA authorizes your current carrier to release your number and allow it to be ported\. 
+ If you are porting multiple numbers from different carriers and countries, submit separate tickets for each set of phone numbers to be ported from different carriers and different countries to streamline communications, tracking, and the LOA process\.
+ A separate LOA is required for numbers from each losing carrier\.

To complete an LOA, provide the following information:
+ The numbers to port\.
+ Information about your current carrier, such as their business name and contact information\.
+ Contact information for the person authorized to make changes to your phone service\. The name, address, and information you provide on the LOA must match the information on file with your current carrier exactly\. To help ensure the porting process goes smoothly, include a copy of the Customer Service Record \(CSR\) or latest phone bill from your carrier\. This will have your name, address, and related telephone numbers on it\. Check that the information on your LOA matches your CSR **exactly**\. 
+ If you have any questions regarding specific details about your current service, consult with your current carrier to ensure the data is accurate\. This will minimize the risk that the LOA is rejected\.

**Important**  
Your LOA form must meet the following criteria:   
It must be legible: clearly written or typed\. 
It must list your company name, the company address, and contact name\. This information must match what is on the current carrier's CSR\.
It must include a true signature\. Most carriers will reject an electronic or printed signature\.
It must be dated within the last 15 days\.
It must include any toll\-free numbers you want to port\. Up to 10 toll\-free numbers can be listed on the LOA\. If you are requesting more than 10 phone numbers be ported, a spreadsheet is required to be attached\. Specify "See Attached" on the LOA where the phone numbers would be listed\. 
It must include only those telephony numbers that belong to the same current carrier and in the same country\. If you have multiple current carriers and countries, you will need to submit multiple LOAs\. 
To further minimize the risk of having your LOA rejected, see [Common reasons why carriers reject an LOA](porting-documentation-requirements.md#why-port-request-rejected)\.

## Step 3: The porting request goes to the Amazon Connect carrier<a name="step3-porting"></a>

After you have submitted all required documentation, the Amazon Connect team submits the porting request on your behalf to the winning carrier\. 
+ The losing and winning carrier follow an industry standard process to validate the contents of the LOA and submitted documentation\.
+ If the LOA contains discrepancies, it will be rejected and you will need to fix the discrepancies and submit a new LOA\. 
+ After the carriers successfully validate the LOA, they will either confirm your requested date or provide an available date for the actual porting\. This is known as the "mutually agreed date\." 

**Note**  
Most carriers require that portings are completed during normal business hours\. For country\-specific business hours, see [Region requirements for ordering and porting phone numbers](phone-number-requirements.md)\. 

## Step 4: Assign the phone number to the contact flow, request service quota increases<a name="step4-porting"></a>

About 3\-4 days before the mutually agreed date and time, the Amazon Connect support team loads the phone number that will be ported into the instance ARN you have provided, and then notifies you\. Now it's time for you to perform the following steps:

1. [Associate the phone number to the desired contact flow](associate-phone-number.md) so the phone number will be ready to receive phone calls after the porting is completed\. If you require assistance assigning multiple phone numbers to contact flows, let us know in your support request\. 
**Important**  
If you do not assign the phone number to the contact flow, calls will not arrive successfully to your Amazon Connect contact center\. 

1. [Submit a service quota request](amazon-connect-service-limits.md) at least five days in advance of the mutually agreed date for any changes to your service quotas required to support your use case\. For example, you may need to increase the number of concurrent calls per instance, or enable countries for outbound calling\. 

## Step 5: Checklist of activities on your porting date<a name="step5-porting"></a>

The action of porting a number can be disruptive: the process involves updating the routing of phone numbers between carriers across a country or Region, including carriers not involved in the actual porting\. In rare cases it can take several hours before all routes across all Telecom carriers are fully updated\.

### Steps you perform to minimize disruption to your phone services<a name="step5a-porting"></a>

On the mutually agreed port date, perform the following steps: 
+ Double\-check that the activities listed in [Step 4](#step4-porting) have been completed: 

  1. Verify that you have assigned the number being ported into your Amazon Connect instance to the appropriate contact flow\.

  1. Verify that any required service quota increases or changes for your Amazon Connect instance were implemented\. For example, increase the number of concurrent calls per instance, or enable countries for outbound calling\.
+ Monitor call traffic from your existing contact center to confirm that incoming traffic has stopped\.
+ Place test calls to your Amazon Connect instance to verify calls are being routed to the correct contact flows\.
+ Ensure agents are logged in to the Contact Control Panel \(CCP\) and can answer calls as they are received\.
+ Monitor call traffic to your Amazon Connect instance to confirm that you are receiving the expected levels of traffic\.

### Steps the Amazon Connect team performs to ensure a smooth transition<a name="step5b-porting"></a>

1. After the Amazon Connect team receives confirmation that the porting has been completed, we will perform final testing to confirm that the porting was successful and the phone number is receiving calls to Amazon Connect\. 

1. After we have completed our testing, we will notify you and ask you to verify the successful completion of the porting\.