# Create an Amazon Connect Instance<a name="amazon-connect-instances"></a>

The first step in setting up your Amazon Connect contact center is to create a virtual contact center instance\. Each instance contains all the resources and settings related to your contact center\. 

## Prerequisites<a name="get-started-prerequisites"></a>
+ When you sign up for Amazon Web Services \(AWS\), your AWS account is automatically signed up for all services in AWS, including Amazon Connect\. You are charged only for the services that you use\. To create an AWS account, see [How do I create and activate an AWS account?](http://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)
+ To allow an IAM user to create an instance, ensure that they have the permissions granted by the **AmazonConnectFullAccess** policy\.

## Step 1: Identity Management<a name="get-started-identity-management"></a>

Permissions to access Amazon Connect features and resource are assigned to user accounts within Amazon Connect\. When you create an instance, you must decide how you want to manage users\. You can't change the identity management option after you create the instance\. For more information, see [Plan Your Identity Management in Amazon Connect](connect-identity-management.md)\.

**To configure identity management for your instance**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. Choose **Get started**\. If you have previously created an instance, choose **Add an instance** instead\.

1. Choose one of the following options:
   + **Store users within Amazon Connect** \- Use Amazon Connect to create and manage user accounts\.
   + **Link to an existing directory** \- Use an AWS Directory Service directory to manage your users\. You can use each directory with one Amazon Connect instance at a time\.
   + **SAML 2\.0\-based authentication** \- Use an existing identity provider \(IdP\) to federate users with Amazon Connect\.

1. If you chose **Store users within Amazon Connect** or **SAML 2\.0\-based authentication**, provide the left\-most label for **Access URL**\. This label must be unique across all Amazon Connect instances in all Regions\. You can't change the access URL after you create your instance\.

1. If you chose **Link to an existing directory**, select the AWS Directory Service directory for **Directory**\. The directory name is used as the left\-most label for **Access URL**\.

1. Choose **Next step**\.

## Step 2: Administrator<a name="get-started-administrator"></a>

After you specify the user name of the administrator for the Amazon Connect instance, a user account is created in Amazon Connect and the user is assigned the **Admin** security profile\.

**To specify the administrator for your instance**

1. Do one of the following, based on the option that you chose in the previous step:
   + If you chose **Store users within Amazon Connect**, select **Add a new admin**, and provide a name, password, and email address for the user account in Amazon Connect\.
   + If you chose **Link to an existing directory**, for **Username**, type the name of an existing user in the AWS Directory Service directory\. The password for this user is managed through the directory\.
   + If you chose **SAML 2\.0\-based authentication**, select **Add a new admin** and provide a name for the user account in Amazon Connect\. The password for this user is managed through the IdP\.

1. Choose **Next step**\.

## Step 3: Telephony Options<a name="get-started-telephony"></a>

Customers can call into your contact center and speak to an agent\. Agents can use the web\-based softphone provided by Amazon Connect for incoming and outgoing telephony, or agents can use a desk phone through the public switched telephone network \(PSTN\)\.

**To configure telephony options for your instance**

1. \(Optional\) To enable customers to call into your contact center, choose **I want to handle incoming calls with Amazon Connect**\.

1. \(Optional\) To enable outbound calling from your contact center, choose **I want to make outbound calls with Amazon Connect**\.

1. Choose **Next step**\.

## Step 4: Data Storage<a name="get-started-data-storage"></a>

When you create an instance, by default we create an Amazon S3 bucket\. Data, such as reports and recordings of conversations, is encrypted using AWS Key Management Service, and then stored in the Amazon S3 bucket\.

This bucket and key are used for both recordings of conversations and exported reports\. Alternatively, you can specify separate buckets and keys for recordings of conversations and exported reports\.

By default, we enable call recording, chat transcripts, exported reports, and contact flow logs\. Live media streaming is not enabled by default\.

You can choose **Next step** to keep the default data storage settings, or you can customize them as follows\.

**To customize the data storage settings for your instance or enable/disable certain functionality:**

1. Choose **Customize settings**\.

1. \(Optional\) To specify the bucket and KMS key for recordings of voice conversations, choose **Call recordings**, **Edit**, specify the bucket name and prefix, select the KMS key by name, and then choose **Save**\.

1. \(Optional\) To specify the bucket and KMS key for recordings \(transcripts\) of chat conversations, choose **Chat transcripts**, **Edit**, specify the bucket name and prefix, select the KMS key by name, and then choose **Save**\.

1. \(Optional\) To specify the bucket and KMS key for exported reports, choose **Exported reports**, **Edit**, specify the bucket name and prefix, select the KMS key by name, and then choose **Save**\.

1. \(Optional\) To disable contact flow logs, clear **Enable Contact flow logs**\.

1. Choose **Next step**\.

## Step 5: Review and Create<a name="get-started-review"></a>

When you are finished configuring your instance, you can create it\.

**To create your instance**

1. Review the configuration choices\. Remember that you cannot change the identity management options after you create the instance\.

1. \(Optional\) To change any of the configuration options, choose **Change**\.

1. Choose **Create instance**\.

1. \(Optional\) To continue configuring your instance, choose **Get started** and then choose **Let's go**\. If you prefer, you can access your instance and configure it later on\. For more information, see [Next Steps](#get-started-next-steps)\.

   If you chose to manage your users directly within Amazon Connect or through an AWS Directory Service directory, you can access the instance using its access URL\. If you chose to manage your users through SAML\-based authentication, you can access the instance using the IdP\.

## Next Steps<a name="get-started-next-steps"></a>

After you create an instance, you can assign your contact center a phone number or import your own phone number\. For more information, see [Set Up Phone Numbers for Your Contact Center](contact-center-phone-number.md)\.