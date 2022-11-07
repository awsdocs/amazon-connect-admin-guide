# Set up prompts to play from an S3 bucket<a name="setup-prompts-s3"></a>

When you configure prompts on the [Get customer input](get-customer-input.md), [Loop prompts](loop-prompts.md), [Play prompt](play.md), or [Store customer input](store-customer-input.md) blocks, you can choose an S3 bucket as the source location\. You can store as many voice prompts as needed in an S3 bucket and access them in real time by using contact attributes\. For examples, see the [Play prompt](play.md) block\. 

## Requirements<a name="format-prompts-s3"></a>
+ **Supported formats**: Amazon Connect supports \.wav files to use for your prompt\. You must use \.wav files that are 8KHz, and mono channel audio with U\-Law encoding\. Otherwise, the prompt won't play correctly\. You can use publicly available third\-party tools to convert your \.wav files to U\-Law encoding\. After converting the files, upload them to Amazon Connect\.
+ **Size**: Amazon Connect supports prompts that are less than 50MB and less than five minutes long\.
+ **For Regions that are disabled by default** \(also called [opt\-in](https://docs.aws.amazon.com/general/latest/gr/rande-manage.html) Regions\) such as Africa \(Cape Town\), your bucket must be in the same Region\.

## Update the S3 bucket policy<a name="bucket-policy-prompts-s3"></a>

To allow Amazon Connect to play prompts from an S3 bucket, when you set up your S3 bucket, you must update the bucket policy to grant `connect.amazonaws.com` \(the Amazon Connect service principal\) permission to call `s3:ListBucket` and `s3:GetObject`\. 

**To update the S3 bucket policy:**

1. Go to the Amazon S3 admin console\. 

1. Choose the bucket that has your prompts\.

1. Choose the **Permissions** tab\.

1. In the **Bucket policy** box, choose **Edit**, and paste the following policy as your template\. Replace the bucket name, Region, AWS account ID, and [instance ID](find-instance-arn.md) with your own information, and then choose **Save changes**\. 

   ```
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "statement1",
               "Effect": "Allow",
               "Principal": {
                   "Service": "connect.amazonaws.com"
               },
               "Action": [
                   "s3:ListBucket",
                   "s3:GetObject"
               ],
               "Resource": [
                   "arn:aws:s3:::customer-prompt-example-bucket",
                   "arn:aws:s3:::customer-prompt-example-bucket/*"
               ],
               "Condition": {
                   "StringEquals": {
                       "aws:SourceAccount": "account-id",
                       "aws:SourceArn": "arn:aws:connect:region:account-id:instance/instance-id"
                   }
               }
           }
       ]
   }
   ```

1. Encryption: Amazon Connect cannot download and play prompts from an S3 bucket if an AWS managed key is enabled on that S3 bucket\. However, you can use a customer managed key to allow the Amazon Connect service principal \("connect\.amazonaws\.com"\) that enables your Amazon Connect instance to access the S3 bucket\. See the following code snippet:

   ```
   {
               "Sid": "Enable Amazon Connect",
               "Effect": "Allow",
               "Principal": {
                   "Service": "connect.amazonaws.com"
               },
               "Action": "kms:decrypt",
               "Resource": [
               	"arn:aws:kms:region:account-ID:key/key-ID"
               ]
   }
   ```

   For information on how to find the key ID, see [Finding the key ID and key ARN](https://docs.aws.amazon.com/Ikms/latest/developerguide/find-cmk-id-arn.html) in the *AWS Key Management Service Developer Guide*\. 

After you set up your S3 bucket with the required bucket policy, configure [Get customer input](get-customer-input.md), [Loop prompts](loop-prompts.md), [Play prompt](play.md), or [Store customer input](store-customer-input.md) to play a prompt from the bucket\.

**Tip**  
For more information about S3 buckets, including examples and limitations, see the [Play prompt](play.md) block\.