# Enable real\-time chat message streaming<a name="chat-message-streaming"></a>

Amazon Connect Chat provides [APIs](https://docs.aws.amazon.com/connect/latest/APIReference/Welcome.html) that enable you to subscribe to a real\-time stream of chat messages\. Using these APIs, you can: 
+ Stream chat messages in real time when a new chat contact is created\.
+ Extend the current Amazon Connect Chat functionality to support use cases like building integrations with [SMS solutions](http://aws.amazon.com/blogs/contact-center/building-personalized-customer-experiences-over-sms-through-amazon-connect/) and third\-party messaging applications \(for example, [Facebook Messenger](http://aws.amazon.com/blogs/contact-center/adding-digital-messaging-channels-to-your-amazon-connect-contact-center/) \), enabling mobile push notifications, and creating analytics dashboards to monitor and track chat message activity\. 

## How the message streaming APIs work<a name="how-chat-message-streaming-apis-work"></a>

The [Amazon Connect message streaming APIs](https://docs.aws.amazon.com/connect/latest/APIReference/Welcome.html) are triggered when certain events occur within an Amazon Connect Chat contact\. For example, when a customer sends a new chat message, the event sends a [payload](sns-payload.md) to a specified endpoint containing data about the message that was just sent\. Messages are published using [Amazon Simple Notification Service](https://docs.aws.amazon.com/sns/latest/dg/welcome.html) \(Amazon SNS\) to a specific endpoint\. 

This topic describes how to set up real\-time message streaming using Amazon Connect and Amazon SNS\. The steps are: 

1. Use the Amazon SNS console to create a new standard SNS topic and set up the messages\.

1. Call the [StartChatContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html) API to initiate the chat contact\.

1. Call the [StartContactStreaming](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartContactStreaming.html) API to initiate message streaming\. 

1. Call the [CreateParticipantConnection](https://docs.aws.amazon.com/connect-participant/latest/APIReference/API_CreateParticipantConnection.html) API to create the participant's connection\.

## Step 1: Create a standard SNS topic<a name="step1-chat-streaming"></a>

1. Go to the Amazon SNS console\. 

1. [Create a SNS topic](https://docs.aws.amazon.com/sns/latest/dg/sns-create-topic.html) in your AWS account\. In the **Details** section, for **Type**, choose **Standard**, enter a name for the topic, and then choose **Create topic**\.
**Note**  
Currently, the message streaming APIs only support standard SNS for real\-time streaming of messages\. They don't support [Amazon SNS FIFO \(first in, first out\) topics](https://docs.aws.amazon.com/sns/latest/dg/sns-fifo-topics.html)\. 

1. After you create the topic, its Amazon Resource Name \(ARN\) is displayed in the **Details** section\. Copy the topic ARN to the clipboard\. You'll use the topic ARN in the next step, and in [Step 3: Enable message streaming on the contact](#step3-chat-streaming)\. 

   The topic ARN looks similar to the following example: 

   ```
   arn:aws:sns:us-east-2:123456789012:MyTopic                                
   ```

1. Choose the **Access policy** tab, choose **Edit**, and then add a resource\-based policy on the SNS topic so that Amazon Connect has permission to publish to it\. Following is a sample SNS policy that you can copy and paste into the JSON editor, and then customize with your values: 

   ```
   {
      "Version":"2012-10-17",
      "Statement":[
         {
            "Effect":"Allow",
            "Principal":{
               "Service":"connect.amazonaws.com"
            },
            "Action":"sns:Publish",
            "Resource":"YOUR_SNS_TOPIC_ARN",
            "Condition":{
               "StringEquals":{
                  "aws:SourceAccount":"YOUR_AWS_ACCOUNT_ID"
               },
               "ArnEquals":{
                  "aws:SourceArn":"YOUR_CONNECT_INSTANCE_ARN"
               }
            }
         }
      ]
   }
   ```
**Note**  
The default **Access policy** comes with conditions applied to `sourceOwner` such as:   

   ```
   "Condition": {
           "StringEquals": {
             "AWS:SourceOwner": "921772911154"
           }
         }
   ```
Make sure you remove it and replace with `SourceAccount`, for example:  

   ```
   "Condition":{
               "StringEquals":{
                  "aws:SourceAccount":"YOUR_AWS_ACCOUNT_ID"
               },
               "ArnEquals":{
                  "aws:SourceArn":"YOUR_CONNECT_INSTANCE_ARN"
               }
            }
   ```
This prevents a [cross\-service confused deputy](cross-service-confused-deputy-prevention.md) issue\. 

1. If you're using server\-side encryption on SNS, verify you have `connect.amazonaws.com` permission enabled on the KMS key\. Following is a sample policy:

   ```
   {
           "Version": "2012-10-17",
           "Id": "key-consolepolicy-3",
           "Statement": [
               {
                   "Sid": "Enable IAM User Permissions",
                   "Effect": "Allow",
                   "Principal": {
                       "AWS": "arn:aws:iam::your_accountId:root",
                       "Service": "connect.amazonaws.com"
                   },
                   "Action": "kms:*",
                   "Resource": "*"
               },
               {
                   "Sid": "Allow access for Key Administrators",
                   "Effect": "Allow",
                   "Principal": {
                       "AWS": "arn:aws:iam::your_accountId:root",
                       "Service": "connect.amazonaws.com"
                   },
                   "Action": [
                       "kms:Create*",
                       "kms:Describe*",
                       "kms:Enable*",
                       "kms:List*",
                       "kms:Put*",
                       "kms:Update*",
                       "kms:Revoke*",
                       "kms:Disable*",
                       "kms:Get*",
                       "kms:Delete*",
                       "kms:TagResource",
                       "kms:UntagResource",
                       "kms:ScheduleKeyDeletion",
                       "kms:CancelKeyDeletion"
                   ],
                   "Resource": "*"
               }
           ]
       }
   ```

## Step 2: Initiate the chat contact<a name="step2-chat-streaming"></a>

1. Call the Amazon Connect [StartChatContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html) API to initiate the chat contact\. 

   For information about how to create the SDK client for calling Amazon Connect APIs, see the following topics:
   + [Class AmazonConnectClientBuilder](https://docs.aws.amazon.com/AWSJavaSDK/latest/javadoc/com/amazonaws/services/connect/AmazonConnectClientBuilder.html) 
   + [Creating Service Clients](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/creating-clients.html) 

1. Keep track of `ContactId` and `ParticipantToken` from the [StartChatContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartChatContact.html) response since these response attributes are used for calling other chat APIs required to enable streaming\. This is described in the next steps\.

## Step 3: Enable message streaming on the contact<a name="step3-chat-streaming"></a>
+ Call [StartContactStreaming](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartContactStreaming.html) to enable real\-time message streaming to your SNS topic\.
  + **Limits**: You can subscribe to up to two SNS topics per contact\.
  + When you call [StartContactStreaming](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartContactStreaming.html), you'll need to provide the Amazon Resource Name \(ARN\) of the SNS topic \(see [Step 1: Create a standard SNS topic](#step1-chat-streaming)\)\.

    A single SNS topic ARN may be used across multiple AWS accounts, but it must be in the same Region as your Amazon Connect instance\. For example, if your topic ARN is in **us\-east\-2**, your Amazon Connect instance must be in **us\-east\-2**\.

## Step 4: Create the participant connection<a name="step4-chat-streaming"></a>
+ Call [CreateParticipantConnection](https://docs.aws.amazon.com/connect-participant/latest/APIReference/API_CreateParticipantConnection.html) with the `ConnectParticipant` attribute passed as true\. 
  + You must call [CreateParticipantConnection](https://docs.aws.amazon.com/connect-participant/latest/APIReference/API_CreateParticipantConnection.html) within five minutes of creating the chat\.
  + Calling [CreateParticipantConnection](https://docs.aws.amazon.com/connect-participant/latest/APIReference/API_CreateParticipantConnection.html) with `ConnectParticipant` set to true only works if you enabled streaming in [Step 2: Initiate the chat contact](#step2-chat-streaming) and caller participant is `Customer`\.
  + This step \(creating the participant connection\) is optional if you have already successfully connected to the chat contact using `WEBSOCKET`\.

## Next steps<a name="nextsteps-chat-streaming"></a>

You are all set for working with the message streaming APIs\.

1. To verify it is working, check that messages are published to the SNS topic you created\. You can do this using Amazon CloudWatch metrics\. For instructions, see [Monitoring Amazon SNS topics using CloudWatch](https://docs.aws.amazon.com/sns/latest/dg/sns-monitoring-using-cloudwatch.html)\. 

1. Because SNS has [limited retention](http://aws.amazon.com/blogs/aws/sns-ttl-control/), we recommend that you set up [Amazon Simple Queue Service \(Amazon SQS\)](http://aws.amazon.com/sqs/) [Amazon Kinesis](http://aws.amazon.com/kinesis/), or another service to retain messages\. 

1. Using [StopContactStreaming](https://docs.aws.amazon.com/connect/latest/APIReference/API_StopContactStreaming.html) is optional and not required if the chats are being [disconnected](disconnect-hang-up.md) through a contact flow, or if the customer disconnects the chat\. However, `StopContactStreaming` provides the option to stop the message streaming on the SNS topic, even if the chat is active and ongoing\.