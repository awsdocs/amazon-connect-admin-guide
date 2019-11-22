# What Is Amazon Connect?<a name="what-is-amazon-connect"></a>

Amazon Connect is a cloud\-based contact center solution\. Amazon Connect makes it more efficient to set up and manage a customer contact center\. It lets you provide reliable customer engagement at any scale\. You can set up a contact center in just a few steps, add agents from anywhere, and start engaging with your customers\.

You can create personalized experiences for your customers using omni\-channel communications\. For example, you can dynamically offer chat and voice contact based on such factors as customer preference and estimated wait times\. Agents, meanwhile, conveniently handle all customers from just one interface\. 

Amazon Connect provides metrics and real\-time reporting so you can optimize contact routing\. You can also resolve customer issues more efficiently by connecting customers with the agents that can best assist them\. Amazon Connect integrates with your existing systems and business applications to provide visibility and insight into all of your customer interactions\. 

Amazon Connect requires no long\-term contracts\. You pay only for what you use\.

## Features of Amazon Connect<a name="amazon-connect-features"></a>
+ **Amazon Connect instance**—A virtual contact center based in the AWS cloud\. Instances can scale to support any size of business\.
+ **User administration**—The ability to add users, such as agents or managers, and configure them with permissions that are appropriate to their roles\. You can authenticate users through Amazon Connect, an existing AWS Directory Service directory service, or a SAML\-based identity provider \(IdP\)\.
+ **Contact Control Panel \(CCP\)**—A customizable interface that agents use to engage with contacts across multiple channels, such as voice and chat\. 
+ **Contact flows**—Features that let you define the customer experience with the contact center from start to end\. For example, you can play prompts, get input from the customer, branch based on customer impact, invoke a Lambda function, or integrate an Amazon Lex bot\.
+ **Skills\-based routing**—The routing of contacts based on the skills of the agents\.
+ **Metrics and reporting**—Real\-time and historical information about the activity in your contact center\.

## Supported Browsers<a name="browsers"></a>

Before you work with Amazon Connect, use the following table to verify that your browser is supported\.


| Browser | Version | How to check your version | 
| --- | --- | --- | 
|  Google Chrome  |  Latest 3 versions  | Open Chrome and type chrome://version in your address bar\. The version is in the Google Chrome field at the top of the results\. | 
|  Mozilla Firefox ESR  |  Latest 3 versions  | Open Firefox\. On the menu, choose the Help icon and then choose About Firefox\. The version number is listed underneath the Firefox name\. | 
|  Mozilla Firefox  |  Latest 3 versions  | Open Firefox\. On the menu, choose the Help icon and then choose About Firefox\. The version number is listed underneath the Firefox name\. | 

## Related Services<a name="related-services-amazon-connect"></a>

To help provide a useful customer connection experience, you can use Amazon Connect with the following services:
+ **AWS Directory Service**—AWS Directory Service for Microsoft Active Directory \(Enterprise Edition\) enables your directory\-aware workloads and AWS resources to use managed Active Directory in the AWS Cloud\. The user and identity management that is available in Amazon Connect is based on this service\.
+ **Amazon S3**—Amazon Simple Storage Service \(Amazon S3\) stores data from Amazon Connect, such as recordings of conversations and metrics reports\.
+ **AWS Lambda**—Lambda lets you build and run code quickly without provisioning or managing servers\. In Amazon Connect, you can invoke functions in a contact flow\. You can build Lambda functions that communicate with your internal systems, such as retrieving the status of an order\. You can then use the values returned from the function in your contact flows to personalize the customer experience\.
+ **Amazon Lex**—Amazon Connect integrates with Amazon Lex to provide voice and text capabilities\. Amazon Lex provides automatic speech recognition \(ASR\) for converting speech to text, and natural language understanding \(NLU\) to recognize the customer intent\. For more information, see the [Amazon Lex Developer Guide](https://docs.aws.amazon.com/lex/latest/dg/)\.
+ **Kinesis**—Amazon Connect integrates with Kinesis as the platform for streaming contact trace records \(CTR\) and agent event streams data\. The data is published to Kinesis in JSON format, and include details about contacts and agent activities in your contact center\. You can use the data stream to publish CTRs to Amazon Redshift, an AWS data warehouse service, or your custom data warehouse systems\. You can then enable detailed analysis and reporting on your contact center data\. You can use Amazon QuickSight, a cloud\-powered business analytics service, or your own BI tools to build powerful visualizations on top of synthesized data\. Additionally, this data can be streamed to Elasticsearch to query on this data using a convenient visual interface\. For more information, see the [Amazon Kinesis Data Streams Developer Guide](https://docs.aws.amazon.com/streams/latest/dev/)\.
**Note**  
Amazon Connect does not support publishing data to streams for which server\-side encryption is enabled\.
+ **Amazon CloudWatch**—Amazon Connect integrates with CloudWatch to provide you with real\-time operational metrics for your contact center\. Metrics include total calls per second, calls rejected and throttled, percentage of concurrent calls, the number of failed and missed calls, and contact flow errors\. You can set up monitors on these metrics to stay on top of the health of your contact center\. For more information, see [CloudWatch Metrics for Your Amazon Connect Instance](monitoring-cloudwatch.md)\.
+ **AWS Identity and Access Management**—The AWS Management Console requires your user name and password to determine whether you have permission to access its resources\. You should not use root credentials to access AWS because root user credentials cannot be revoked or limited in any way\. Instead, we recommend that you create an IAM user and add the user to an IAM group with administrative permissions\. You can then access the console using the IAM user credentials\. For more information, see the [IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/)\.

  If you signed up for AWS but have not created an IAM user for yourself, you can create one using the IAM console\. For more information, see [Create Individual IAM Users](https://docs.aws.amazon.com/IAM/latest/UserGuide/IAMBestPractices.html#create-iam-users) in the *IAM User Guide*\.
+ **AWS Key Management Service**—Amazon Connect is integrated with AWS KMS to protect your customer data\. You can perform crucial management tasks from the AWS KMS console\. For more information, see [What is the AWS Key Management Service](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html) in the *AWS Key Management Service Developer Guide*\.