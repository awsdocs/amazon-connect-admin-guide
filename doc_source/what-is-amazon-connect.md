# What Is Amazon Connect?<a name="what-is-amazon-connect"></a>

Amazon Connect is a cloud\-based contact center solution\. Amazon Connect makes it easy to set up and manage a customer contact center and provide reliable customer engagement at any scale\. You can set up a contact center in just a few steps, add agents from anywhere, and start to engage with your customers right away\.

Amazon Connect provides rich metrics and real\-time reporting that allow you to optimize contact routing to decrease wait times\. You can also resolve customer issues more efficiently by putting customers in touch with the right agents\. Amazon Connect integrates with your existing systems and business applications to provide visibility and insight into all of your customer interactions\. Amazon Connect requires no long\-term contracts, and you pay only for what you use\.

## Amazon Connect Instances<a name="amazon-connect-fundamentals"></a>

To create an Amazon Connect contact center, you create an Amazon Connect instance\. Each instance contains all of the resources and settings related to your contact center\. You can manage settings for your instance from the Amazon Connect console\. You can manage settings for your contact center from within your contact center\. You can create multiple instances, but each instance functions only within the AWS region in which you create it\. Settings, users, metrics, and reporting are not shared between Amazon Connect instances\.

### Identity Management<a name="directories"></a>

When you create an Amazon Connect instance, you must choose how you want to manage your Amazon Connect users\. Permissions to access Amazon Connect features and resources, such as opening the contact control panel \(CCP\), placing calls, or creating reports, are assigned to user accounts within Amazon Connect\. You can choose from the following three options for identity management:
+ Store users in Amazon Connect\.
+ Link to an existing directory using AWS Directory Service\.
+ Use SAML 2\.0\-based authentication to federate with your Amazon Connect instance and enable single sign\-on\.

To learn more about identity management in Amazon Connect, see [Plan for User and Identity Management](gettingstarted.md#identity-management)\.

### Amazon Connect Administrator<a name="administrators"></a>

Amazon Connect administrators set permissions, manage and generate metrics, add users, and configure all aspects of your contact center\. You can grant or deny different types of permissions by assigning security profiles in Amazon Connect\.

### Secure Storage and Data Integrity<a name="storagedata"></a>

Secure storage and data integrity are an important part of managing recorded calls\. Customer calls are recorded in real time and can contain sensitive information\. 

By default, AWS creates a new Amazon S3 bucket during the configuration process, with built\-in encryption\. You can also use existing S3 buckets\. There are separate buckets for call recordings and exported reports, and they are configured independently\. There is full access through Amazon Connect and control over recordings, allowing for custom retention policies\. The customizable metrics reports published into Amazon S3 can be processed using the Amazon S3 API or AWS Lambda\. Integrate the reports with external systems such as workforce management and business intelligence tools\.

**Note**  
We recommend that you keep the default settings for encryption\.

The following security measures are supported:
+ AWS Key Management Service—AWS KMS is a powerful, managed service that gives you complete control over your encryption keys\. A default AWS KMS key is provided\.
+ ARN/ID—You can use an ARN/ID instead of an AWS KMS master key\. This is an advanced option and should be attempted only if you are confident of the changes that you're going to make\.

## Supported Browsers<a name="browsers"></a>

Before you start working with Amazon Connect, use the following table to verify that your browser is supported\.


| Browser | Version | Check your version | 
| --- | --- | --- | 
|  Google Chrome  |  Latest 3 versions  | Open Chrome and type chrome://version in your address bar\. The version is in the Google Chrome field at the top of the results\. | 
|  Mozilla Firefox ESR  |  Latest 3 versions  | Open Firefox\. On the menu, choose the Help icon and then choose About Firefox\. The version number is listed underneath the Firefox name\. | 
|  Mozilla Firefox  |  Latest 3 versions  | Open Firefox\. On the menu, choose the Help icon and then choose About Firefox\. The version number is listed underneath the Firefox name\. | 

## Service Limits<a name="amazon-connect-servicelimits"></a>

The following table provides the default limits for new Amazon Connect instances\. You can create two instances per AWS account to start, but if you need more instances it is easy to request an increase\. You can also request an increase for any of the limits using the [Amazon Connect service limits increase form](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-connect)\. You must be signed in to your AWS account to access the form\.


| Item | Default limit | 
| --- | --- | 
|  Amazon Connect instances per account  |  2  | 
|  Users per instance  |  500  | 
|  Phone numbers per instance  |  10  | 
|  Queues per instance  |  50  | 
|  Queues per routing profile  |  50  | 
|  Routing profiles per instance  |  100  | 
|  Hours of operation per instance  |  100  | 
|  Quick connects per instance  |  100  | 
|  Prompts per instance  |  500  | 
|  Agent status per instance  |  50  | 
|  Security profiles per instance  |  100  | 
|  Contact flows per instance  |  100  | 
|  Groups per level  |  50  | 
|  Reports per instance  |  500  | 
|  Scheduled reports per instance  |  50  | 
|  Concurrent active calls per instance  |  100  | 

## Related Services<a name="related-services-amazon-connect"></a>

The following services are used with Amazon Connect:
+ **AWS Directory Service**—AWS Directory Service for Microsoft Active Directory \(Enterprise Edition\), also known as Microsoft AD, enables your directory\-aware workloads and AWS resources to use managed Active Directory in the AWS Cloud\. Amazon Connect user and identity management is based on this service\.
+ **Amazon S3**—Amazon Simple Storage Service \(Amazon S3\) is object storage with a simple web service interface to store and retrieve any amount of data from anywhere on the web\. Amazon Connect uses Amazon S3 as a primary data storage service/platform for call recordings and metrics reports delivered into your AWS account\.
+ **AWS Lambda**—Lambda allows you to build and run code quickly without provisioning or managing servers\. Amazon Connect contact flows \(IVR flows\) are integrated with Lambda so you can build a highly personalized and dynamic IVR experience\. You can build Lambda functions that communicate with CRM systems or custom services for data dips that influence customer IVR experience \(such as customer segmentation and dynamic IVR menus, or account and last contact look ups\)\. Lambda functions can also be used as notification mechanisms to external systems during specific points in the contact flow\.
+ **Amazon Lex**—Amazon Connect integrates with Amazon Lex to build conversational interfaces using voice and text\. Amazon Lex provides the advanced deep learning functionalities of automatic speech recognition \(ASR\) for converting speech to text, and natural language understanding \(NLU\) to recognize the intent of the text, to enable you to build applications with highly engaging user experiences and lifelike conversational interactions\. For more information, see the [Amazon Lex Developer Guide](http://docs.aws.amazon.com/lex/latest/dg/)\.
+ **Kinesis**—Amazon Connect integrates with Kinesis as the platform for streaming contact trace records \(CTR\) and agent event streams data\. The data is published to Kinesis in JSON format, and include details about contacts and agent activities in your contact center\. You can use this data stream to optionally process and publish them into Amazon Redshift \(an AWS data warehouse service\) or your custom data warehouse systems, enabling detailed analytics and reporting on your contact center data\. You can leverage Amazon QuickSight \(a cloud\-powered business analytics service\) or your own BI tools to build powerful visualizations on top of synthesized data\. Additionally, this data can be streamed to Elasticsearch to query on this data using a convenient visual interface\. For more information, see the [Amazon Kinesis Data Streams Developer Guide](http://docs.aws.amazon.com/streams/latest/dev/)\.
**Note**  
Amazon Connect does not support publishing data to streams for which server\-side encryption is enabled\.
+ **Amazon CloudWatch**—Amazon Connect integrates with CloudWatch to provide you with real\-time operational metrics for your contact center, such as total calls per second, calls rejected and throttled, percentage of concurrent calls, failed / missed calls count \(errors, bad number/address, busy/line engaged\), and contact flow errors\. You can set up monitors on these metrics in order to stay on top of the health of your contact center\. For more information, see [Monitoring Amazon Connect in Amazon CloudWatch Metrics](monitoring-cloudwatch.md)\.
+ **AWS Identity and Access Management**—The AWS Management Console requires your user name and password so that any service you use can determine whether you have permission to access its resources\. We recommend that you avoid using AWS account root user credentials to access AWS because root user credentials cannot be revoked or limited in any way\. Instead, we recommend that you create an IAM user and add the user to an IAM group with administrative permissions\. You can then access the console using the IAM user credentials\. For more information, see the [IAM User Guide](http://docs.aws.amazon.com/IAM/latest/UserGuide/)\.

  If you signed up for AWS but have not created an IAM user for yourself, you can create one using the IAM console\. For more information, see [Create Individual IAM Users](http://docs.aws.amazon.com/IAM/latest/UserGuide/IAMBestPractices.html#create-iam-users) in the *IAM User Guide*\.
+ **AWS Key Management Service**—Amazon Connect is integrated with AWS KMS to protect your customer data\. Key management can be performed from the AWS KMS console\. For more information, see [What is the AWS Key Management Service](http://docs.aws.amazon.com/kms/latest/developerguide/overview.html) in the *AWS Key Management Service Developer Guide*\.