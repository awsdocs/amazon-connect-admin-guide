# Embed the CCP into Salesforce<a name="salesforce-integration"></a>

The core functionality of the Amazon Connect CTI Adapter provides a WebRTC browser\-based Contact Control Panel \(CCP\) within Salesforce\. The Amazon Connect CTI integration consists of two components: 
+ [A managed Salesforce package](https://appexchange.salesforce.com/appxListingDetail?listingId=a0N3A00000EJH4yUAH)
+ [An AWS Serverless application deployed to your AWS environment](https://serverlessrepo.aws.amazon.com/applications/arn:aws:serverlessrepo:us-west-2:821825267871:applications~AmazonConnectSalesforceLambda) 

 For a detailed walk\-through and setup of the full CTI Adapter capabilities for Salesforce Lightning, see the  [Amazon Connect CTI Adapter for Salesforce Lightning installation guide](https://amazon-connect.github.io/amazon-connect-salesforce-cti/docs/lightning/notices/)\. 

 For the CTI Adapter for Salesforce Classic, see the [Amazon Connect CTI Adapter for Salesforce Classic installation guide](https://amazon-connect.github.io/amazon-connect-salesforce-cti/docs/classic/notices/)\. 

We recommend that you initially install the package into your Salesforce sandbox\. After the package is installed, you can configure your Salesforce Call Center configuration within Salesforce\.