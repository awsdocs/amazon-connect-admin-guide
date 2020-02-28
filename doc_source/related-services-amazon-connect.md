# The Power of AWS with Amazon Connect<a name="related-services-amazon-connect"></a>

To help provide a better contact center, you can use Amazon Connect with the following AWS services\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/connect-overview2.png)

## Development<a name="development-services"></a>

You can use AWS Lambda functions to either look up or post data to sources outside of Amazon Connect\. For example, you can look up an inbound caller on Salesforce based on the customer’s phone number\. The function may return such results as the customer name, membership level \(for example, frequent flyer\), last order, and order status\. Then based on that information, the call can be routed to an Amazon Lex bot or an agent\. 

You can also use Lambda with AWS databases like DynamoDB to create dynamic routing abilities\. For example, you can retrieve a prompt in a specific language, based on input from the customer\.

API Gateway and Step Functions further enhance the abilities of Lambda\. 

For more information, see:
+ [Invoke AWS Lambda Functions](connect-lambda-functions.md)
+ Blog post: [Building a state\-aware workflow with Amazon Connect and AWS Step Functions](http://aws.amazon.com/blogs/contact-center/building-a-state-aware-workflow-with-amazon-connect-and-aws-step-functions/)

## Storage<a name="storage-services"></a>

Amazon Connect uses Amazon Simple Storage Service \(Amazon S3\) to store recorded conversations and exported reports\. When you set up Amazon Connect, it creates default buckets for these requirements, or you can point it to existing Amazon S3 infrastructure\. For more information, see [Step 4: Data Storage](amazon-connect-instances.md#get-started-data-storage) in [Create an Amazon Connect Instance](amazon-connect-instances.md)\.

VPC endpoints are not supported\. 

You can also manage the Amazon S3 policies to move data to Amazon S3 Glacier for less expensive long\-term storage\. However, it breaks the link in the contact trace record \(CTR\) in Amazon Connect\. To fix this, use a Lambda function to rename the S3 Glacier object to match the data in the CTR\. 

## Database<a name="database-services"></a>

You can use AWS databases with Amazon Connect for a variety of reasons\. For example, with DynamoDB, you can create quick tables of data\. 

You can also create tables of dynamic information for call routing\. For example, a Lambda function can write inbound calls to a DynamoDB table, then query the table to see if there are other matches for the phone number\. If so, a decision can be made to send the caller to the same queue as before, or to flag them as a repeat caller\. 

For more information, see:
+ Blog post: [Creating dynamic, personalized experiences in Amazon Connect](http://aws.amazon.com/blogs/contact-center/creating-dynamic-personalized-experiences-in-amazon-connect/)

## Analytics<a name="analytics-services"></a>

Amazon Connect tracks all interactions using [contact trace records \(CTRs\)](about-contact-states.md#ctr-events)\. CTRs are used for real\-time and historical metrics reports\. You can also use Amazon Kinesis to stream them to an AWS database like Amazon Redshift or Amazon Athena for BI analysis \(Amazon QuickSight, or a third party such as Tableau\)\. There are AWS CloudFormation templates available to set up this functionality for Amazon Redshift and Athena\. 

For more information, see:
+ [How to Access Kinesis Video Streams Data](access-media-stream-data.md)
+ Blog post: [Recovering abandoned calls with Amazon Connect](http://aws.amazon.com/blogs/contact-center/recovering-abandoned-calls-with-amazon-connect/)

## Machine Learning \(ML\) and Artificial Intelligence \(AI\)<a name="ai-services"></a>

Amazon Connect uses the following services for ML/AI: 
+ Amazon Lex—Lets you create a chatbot to use as Interactive Voice Response \(IVR\)\. For more information, see [Add an Amazon Lex Bot](amazon-lex.md)\. 
+ Amazon Polly—Provides text\-to\-speech in all contact flows\. For more information, see [Add Text\-to\-Speech to Prompts](text-to-speech.md) and the blog post [SSML in Amazon Connect Contact Flows](http://aws.amazon.com/blogs/contact-center/ssml-in-amazon-connect-contact-flows/)\.
+ Amazon Transcribe—Grabs conversation recordings from Amazon S3, and transcribes them to text so you can review them\. For more information, see [Set Up Recording Behavior](set-up-recordings.md) and [Review Recorded Conversations](review-recorded-conversations.md)\.
+ Amazon Comprehend—Takes the transcription of recordings, and applies speech analytics machine learning to the call to identify sentiment, keywords, adherence to company policies, and more\. For more information, see [Analyze Conversations using Contact Lens for Amazon Connect](analyze-conversations.md)\. 

## Messaging<a name="messaging-services"></a>

Amazon Connect uses the following services for messaging: 
+ Amazon Pinpoint—Use as an outbound messaging trigger for events; for example, bulk messaging \(such as outbound marketing campaigns\)\. For more information, see this blog post: [Using Amazon Pinpoint to send text messages in Amazon Connect](http://aws.amazon.com/blogs/contact-center/using-amazon-pinpoint-to-send-text-messages-in-amazon-connect/)\.
+ Amazon Simple Notification Service \(Amazon SNS\)—Use to send and receive SMS and other channel notifications\. Amazon SNS is particularly useful for sending alerts and validations\. 
+ Amazon Simple Email Service \(Amazon SES\)—Use to send validation e\-mails, such as a password reset bot sending a confirmation of the transaction\. 

## Security<a name="security-services"></a>

Amazon Connect uses the following services for added security: 
+ AWS Identity and Access Management \(IAM\)—Use to manage permissions for users\. Amazon Connect users require permission for services\. For more information, see [Identity and Access Management for Amazon Connect](security-iam.md)\.
+ AWS Directory Service—Amazon Connect supports user federation through the internal directory \(created in the Amazon Connect instance\), using Active Directory integration \(MAD, ADFS\) or SAML 2\.0\. 

  For more information, see:
  +  [Plan Your Identity Management in Amazon Connect](connect-identity-management.md)
  + Blog post: [Enabling federation with AWS Single Sign\-On and Amazon Connect](http://aws.amazon.com/blogs/contact-center/enabling-federation-with-aws-single-sign-on-and-amazon-connect/)

## Management<a name="management-services"></a>

Amazon Connect uses the following services for monitoring usage: 
+ Amazon CloudWatch—Collects logs, service metrics, performance metrics for Amazon Connect\. For more information, see [CloudWatch Metrics for Your Amazon Connect Instance](monitoring-cloudwatch.md)\. 
+ AWS CloudFormation—Amazon Connect does not support this directly for creating instances\. However, it does support AWS CloudFormation templates for associated services, like integrations, database export, and so on\.
+ AWS CloudTrail—Provides a record of Amazon Connect API calls\. This is especially useful for tracking who accessed recorded conversations\. For more information, see [Logging Amazon Connect API Calls with AWS CloudTrail](logging-using-cloudtrail.md)\.
