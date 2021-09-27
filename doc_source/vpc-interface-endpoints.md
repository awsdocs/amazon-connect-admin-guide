# Amazon Connect Voice ID and interface VPC endpoints \(AWS PrivateLink\)<a name="vpc-interface-endpoints"></a>

You can establish a private connection between your VPC and Amazon Connect Voice ID by creating an interface VPC endpoint\. Interface endpoints are powered by [AWS PrivateLink](http://aws.amazon.com/privatelink), a technology that enables you to privately access Amazon Connect Voice ID APIs without an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection\. Instances in your VPC don't need public IP addresses to communicate with Amazon Connect Voice ID APIs\. Traffic between your VPC and Amazon Connect Voice ID does not leave the Amazon network\. 

Each interface endpoint is represented by one or more [Elastic network interfaces](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html) in your subnets\.

For more information, see [AWS PrivateLink and VPC endpoints](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html) in the *AWS PrivateLink Guide*\.

## Considerations for Amazon Connect Voice ID VPC endpoints<a name="vpc-endpoint-considerations"></a>

Before you set up an interface VPC endpoint for Amazon Connect Voice ID, ensure that you review [Interface endpoint properties and limitations](https://docs.aws.amazon.com/vpc/latest/privatelink/vpce-interface.html#vpce-interface-limitations) in the *AWS PrivateLink Guide*\. 

Amazon Connect Voice ID supports making calls to all of its API actions from your VPC\. 

## Creating an interface VPC endpoint for Amazon Connect Voice ID<a name="vpc-endpoint-create"></a>

You can create a VPC endpoint for the Amazon Connect Voice ID service using either the Amazon VPC console or the AWS Command Line Interface \(AWS CLI\)\. For more information, see [Create an interface endpoint](https://docs.aws.amazon.com/vpc/latest/privatelink/vpce-interface.html#create-interface-endpoint) in the *AWS PrivateLink Guide*\. 

Create a VPC endpoint for Amazon Connect Voice ID using the following service name: 
+ com\.amazonaws\.\[*region*\]\.voiceid

If you enable private DNS for the endpoint, you can make API requests to Amazon Connect Voice ID using its default DNS name for the Region, for example, voiceid\.us\-east\-1\.amazonaws\.com\.

For more information, see [Access a service through an interface endpoint](https://docs.aws.amazon.com/vpc/latest/privatelink/vpce-interface.html#access-service-though-endpoint) in the *AWS PrivateLink Guide*\.

## Creating a VPC endpoint policy for Amazon Connect Voice ID<a name="vpc-endpoint-policy"></a>

You can attach an endpoint policy to your VPC endpoint that controls access to Amazon Connect Voice ID\. The policy specifies the following information: 
+ The principal that can perform actions\.
+ The actions that can be performed\.
+ The resources on which actions can be performed\.

For more information, see [Control access to services with VPC endpoints](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints-access.html) in the *IAM User Guide*\. 

### Example: VPC endpoint policy for Amazon Connect Voice ID actions<a name="vpc-interface-endpoints"></a>

The following VPC endpoint policy grants access to the listed Amazon Connect Voice ID actions for all principals on all resources\. 

```
{
    "Statement":[
        {
            "Effect":"Allow",
            "Action":[
                "voiceid:CreateDomain",
                "voiceid:EvaluateSession",
                "voiceid:ListSpeakers"
            ],
            "Resource":"*",
            "Principal":"*"
        }
    ]
}
```