# Enable attachments to share files using chat<a name="enable-attachments"></a>

You can allow customers and agents to share files using chat\. After you complete the steps in this topic, an attachment icon automatically appears in your agent's Contact Control Panel so they can share attachments on chats\. 

You will need to update your customer\-facing user interface to support attachment sharing\.

**Using a custom agent application?** Check out the APIs we've added to support attachment sharing: [StartAttachmentUpload](https://docs.aws.amazon.com/connect-participant/latest/APIReference/API_StartAttachmentUpload.html), [CompleteAttachmentUpload](https://docs.aws.amazon.com/connect-participant/latest/APIReference/API_CompleteAttachmentUpload.html), and [GetAttachment](https://docs.aws.amazon.com/connect-participant/latest/APIReference/API_GetAttachment.html)\.

## Step 1: Enable attachments<a name="step1-enable-attachments"></a>

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. On the **Instances** page, choose the instance alias\. The instance alias is also your instance name, which appears in your Amazon Connect URL\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/instance.png)

1. On the **Data storage** page, under the **Attachments**, choose **Edit**, select **Enable Attachments sharing**, and then choose **Save**\.

   Storage options appear, similar to the following image\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/attachments-enable.png)

1. You can change the Amazon S3 bucket location where attachments are stored\. By default, your existing Amazon Connect bucket is used, with a new prefix for attachments\. 
**Note**  
Currently, Amazon Connect doesn’t support S3 buckets with [Object Lock](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lock.html) enabled\. 

   The attachments feature leverages two Amazon S3 locations: a staging location and a final location\. 

   Note the following about the staging location:
   + The staging location is used as part of a business validation flow\. Amazon Connect uses it to validate the file size and type before it is shared with the chat participant\. 
   + The staging prefix is created by Amazon Connect based on the bucket path you have selected\. Specifically, it includes the S3 prefix for where you are saving files, with **staging** appended to it\.
   + We recommend that you change the data retention policy for the staging prefix to one day\. This way you won't be charged for storing the staging files\. For instructions, see [How do I create a lifecycle rule for an S3 bucket?](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/create-lifecycle.html) in the *Amazon S3 User Guide*\.
**Warning**  
Only change the lifecycle for the **file staging location**\. If you accidentally change the lifecycle for the entire Amazon S3 bucket, all transcripts and attachments will be deleted\.

## Step 2: Configure a CORS policy on your attachments bucket<a name="step2-update-cors-policy"></a>

To allow customers and agents to upload and download files, update your cross\-origin resource sharing \(CORS\) policy to allow `PUT` and `GET` requests for the Amazon S3 bucket you are using for attachments\. This is more secure than enabling public read/write on your Amazon S3 bucket, which we don't recommend\.

**To configure CORS on the attachments bucket**

1. Find the name of the Amazon S3 bucket for storing attachments: 

   1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

   1. In the Amazon Connect console, choose **Data storage**, and locate the Amazon S3 bucket name\. 

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In the Amazon S3 console, select your Amazon S3 bucket\. 

1. Choose the **Permissions** tab, and then scroll down to the **Cross\-origin resource sharing \(CORS\)** section\.

1. Add a CORS policy that has one of the following rules on your attachments bucket\. For example CORS policies, see [Cross\-origin resource sharing: Use\-case scenarios](https://docs.aws.amazon.com/AmazonS3/latest/dev/cors.html#example-scenarios-cors) in the *Amazon S3 Developer Guide*\.
   + Option 1: List the endpoints from where attachments will be sent and received, such as the name of your business web site\. This rule allows cross\-origin PUT and GET requests from your website \(for example, http://www\.example1\.com\)\.

     Your CORS policy might look like the following example:

     ```
     [
         {                               
             "AllowedMethods": [
                 "PUT",
                 "GET"            
             ],
             "AllowedOrigins": [
                 "http://www.example1.com",   //List the endpoints from where attachments will be sent and received, 
                 "http://www.example2.com"    //such as the name of your business web site. 
            ],
            "AllowedHeaders": [
                 "*"
            ]
         }    
     ]
     ```
   + Option 2: Add the `*` wildcard to `AllowedOrigin`\. This rule allows cross\-origin PUT and GET requests from all origins, so you don't have to list your endpoints\.

     Your CORS policy might look like the following example:

     ```
     [    
         {                               
             "AllowedMethods": [
                 "PUT",
                 "GET"            
             ],       
             "AllowedOrigins": [
                 "*"
             ],
             "AllowedHeaders": [
                 "*"
             ]
         }
     ]
     ```

## Step 3: Update your chat UI<a name="step3-update-chat-ui"></a>

To help you update the chat user interface that your customers use, we've posted an updated version of chat interface JS\. It exposes an attachment icon on the UI and supports the backend calls for attachment sharing\. See [Amazon Connect Chat UI Examples](https://github.com/amazon-connect/amazon-connect-chat-ui-examples) on GitHub\.