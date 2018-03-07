# What Is Amazon Connect?<a name="what-is-amazon-connect"></a>

Amazon Connect is a cloud\-based contact center solution\. Amazon Connect makes it easy to set up and manage a customer contact center and provide reliable customer engagement at any scale\. You can deploy a contact center in just a few steps, on\-board agents from anywhere, and begin to engage with your customers\. 

Amazon Connect provides rich metrics and real\-time reporting that allow you to manage contact routing to decrease wait times and resolve issues by putting customers in touch with the right agents\. Amazon Connect integrates with your existing systems and business applications to provide visibility and insight into all of your customer interactions\. Amazon Connect requires no long\-term contracts, and you pay only for what you use\.

## How Amazon Connect Works<a name="amazon-connect-fundamentals"></a>

An Amazon Connect contact center resides in an instance, which contains all the resources and settings you need to launch, run, and scale your contact center\. These instances provide both the ability to configure settings such as data storage options, and a user interface to manage and use your contact center\.

To get started with Amazon Connect, ensure that you have either a user directory or a list of users\. These users can range from administrators to agents\.

It's important to understand the underlying functions of your Amazon Connect configuration\. These need to be set up correctly to ensure that your contact center doesn't encounter any issues\.

**Note**  
You can have multiple instances, but information such as user directories cannot be shared across instances\.

### Directories for Identity Management<a name="directories"></a>

Amazon Connect requires a directory to store user information and permissions for the instance\. As a first step to setting up an Amazon Connect instance, you select the directory you want to use for identity management\. You can choose to manage users in Amazon Connect, or to use an existing directory that is set up in AWS Directory Service\. An existing directory must be associated with your AWS account, and active in the AWS region in which you create your instance\. You can choose to use a [Microsoft Active Directory](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/directory_microsoft_ad.html), [Active Directory Connector](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/directory_ad_connector.html), or [Simple Active Directory](http://docs.aws.amazon.com/directoryservice/latest/admin-guide/directory_simple_ad.html)\. You can associate an AWS Directory Service directory with only one Amazon Connect instance at a time\.

You cannot change the directory you select for identity management after you create the instance\. If you decide to change the directory you selected, you can delete the instance and create a new one\. When you delete an instance, you lose all configuration settings and metrics data for it\.

There is no additional charge for using an existing or a proprietary directory\. For information about the costs associated with using AWS Directory Service, see [AWS Service Pricing Overview](http://aws.amazon.com/pricing)\.

The following limitations apply to all new directories created using AWS Directory Service:

+ Directories can only have alphanumeric names\. Only the **\.** character can be used\.

+ Directories cannot be unbound from an Amazon Connect instance after they have been associated\.

+ Only one directory can be added to an Amazon Connect instance\.

+ Directories cannot be shared across multiple Amazon Connect instances\.

### Administrators<a name="administrators"></a>

Administrators set permissions, manage and generate metrics, add users, and configure all aspects of contact management\. Administrators can be granted different types of permissions—this is done in Amazon Connect\.

### Secure Storage and Data Integrity<a name="storagedata"></a>

Secure storage and data integrity are an important part of managing recorded calls\. Customer calls are recorded in real time and can contain sensitive information\. 

By default, AWS creates a new Amazon S3 bucket during the configuration process, with built\-in encryption\. You can also use existing S3 buckets\. There are separate buckets for call recordings and exported reports, and they are configured independently\. There is full access through Amazon Connect and control over recordings, allowing for custom retention policies\. Customizable metrics reports published into Amazon S3 can be processed using the Amazon S3 API or AWS Lambda to integrate with external systems such as workforce management and business intelligence tools\.

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

The following table provides the default limits for new Amazon Connect instances\. You can create two instances per AWS account to start, but if you need more instances it is easy to request an increase\. You can also request an increase for any of the limits using the [Amazon Connect service limits increase form](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-connect)\. You need to be signed in to your AWS account to access the form\.


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
|  Concurrent active calls per instance  |  10  | 

## Related Services<a name="related-services-amazon-connect"></a>

The following services are used with Amazon Connect:

+ **AWS Directory Service**—AWS Directory Service for Microsoft Active Directory \(Enterprise Edition\), also known as Microsoft AD, enables your directory\-aware workloads and AWS resources to use managed Active Directory in the AWS Cloud\. Amazon Connect user and identity management is based on this service\.

+ **Amazon S3**—Amazon Simple Storage Service \(Amazon S3\) is object storage with a simple web service interface to store and retrieve any amount of data from anywhere on the web\. Amazon Connect uses Amazon S3 as a primary data storage service/platform for call recordings and metrics reports delivered into your AWS account\.

+ **AWS Lambda**—Lambda allows you to build and run code quickly without provisioning or managing servers\. Amazon Connect contact flows \(IVR flows\) are integrated with Lambda so you can build a highly personalized and dynamic IVR experience\. You can build Lambda functions that communicate with CRM systems or custom services for data dips that influence customer IVR experience \(such as customer segmentation and dynamic IVR menus, or account and last contact look ups\)\. Lambda functions can also be used as notification mechanisms to external systems during specific points in the contact flow\.

+ **Amazon Lex**—Amazon Connect integrates with Amazon Lex to build conversational interfaces using voice and text\. Amazon Lex provides the advanced deep learning functionalities of automatic speech recognition \(ASR\) for converting speech to text, and natural language understanding \(NLU\) to recognize the intent of the text, to enable you to build applications with highly engaging user experiences and lifelike conversational interactions\. For more information, see the [Amazon Lex Developer Guide](http://docs.aws.amazon.com/lex/latest/dg/)\.

+ **Kinesis**—Amazon Connect integrates with Kinesis as the platform for streaming contact trace records \(CTR\) and agent event streams data\. The data is published to Kinesis in JSON format, and include details about contacts and agent activities in your contact center\. You can use this data stream to optionally process and publish them into Amazon Redshift \(an AWS data warehouse service\) or your custom data warehouse systems, enabling detailed analytics and reporting on your contact center data\. You can leverage Amazon QuickSight \(a cloud\-powered business analytics service\) or your own BI tools to build powerful visualizations on top of synthesized data\. Additionally, this data can be streamed to Elasticsearch to query on this data using a convenient visual interface\. For more information, see the [Amazon Kinesis Data Streams Developer Guide](http://docs.aws.amazon.com/streams/latest/dev/)\.
**Note**  
Amazon Connect does not support publishing data to streams for which server\-side encryption is enabled\.

+ **Amazon CloudWatch**—Amazon Connect integrates with CloudWatch to provide you with real\-time operational metrics for your contact center, such as total calls per second, calls rejected and throttled, percentage of concurrent calls, failed / missed calls count \(errors, bad number/address, busy/line engaged\), and contact flow errors\. You can set up monitors on these metrics in order to stay on top of the health of your contact center\. For more information, see [Monitoring Amazon Connect Using Amazon CloudWatch Metrics](monitoring-cloudwatch.md)\.

+ **AWS Identity and Access Management**—The AWS Management Console requires your username and password so that any service you use can determine whether you have permission to access its resources\. We recommend that you avoid using AWS account root user credentials to access AWS because root user credentials cannot be revoked or limited in any way\. Instead, we recommend that you create an IAM user and add the user to an IAM group with administrative permissions\. You can then access the console using the IAM user credentials\. For more information, see the [IAM User Guide](http://docs.aws.amazon.com/IAM/latest/UserGuide/)\.

  If you signed up for AWS but have not created an IAM user for yourself, you can create one using the IAM console\. For more information, see [Create Individual IAM Users](http://docs.aws.amazon.com/IAM/latest/UserGuide/IAMBestPractices.html#create-iam-users) in the *IAM User Guide*\.

+ **AWS Key Management Service**—Amazon Connect is integrated with AWS KMS to protect your customer data\. Key management can be performed from the AWS KMS console\. For more information, see [What is the AWS Key Management Service](http://docs.aws.amazon.com/kms/latest/developerguide/overview.html) in the *AWS Key Management Service Developer Guide*\.