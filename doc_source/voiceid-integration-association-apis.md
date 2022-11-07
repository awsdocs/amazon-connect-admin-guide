# Voice ID and Amazon Connect Integration Association APIs<a name="voiceid-integration-association-apis"></a>

You can use the following APIs to manage associations with Amazon Connect instances\. You can perform these operations on the AWS Console as well\. 

1. [CreateIntegrationAssociation](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateIntegrationAssociation.html): To enable Voice ID on an Amazon Connect instance, you will need to associate a Voice ID domain with a Amazon Connect instance using a `CreateIntegrationAssociation` request\. You can only associate one Voice ID domain to an Amazon Connect instance\. If the instance is already associated with a domain, the API returns the following error: 

   `DuplicateResourceException` \(409\) \- Request is trying to created a duplicate resource\.
**Note**  
When you enable Voice ID for an Amazon Connect instance \(by using either the Amazon Connect console or the [CreateIntegrationAssociation](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateIntegrationAssociation.html) API\), Amazon Connect creates a managed Amazon EventBridge rule in your account\. This rule is used to ingest Voice ID events for creating contact records related to Voice ID\. Additionally, Amazon Connect adds [Voice ID permissions](connect-slr.md) to the service\-linked role for Amazon Connect\.

1.  [DeleteIntegrationAssociation](https://docs.aws.amazon.com/connect/latest/APIReference/API_DeleteIntegrationAssociation.html): To delete an existing association between an Amazon Connect instance and a Voice ID domain, you will need to call the `DeleteIntegrationAssociation` APIs along with the Amazon Connect InstanceID and the `IntegrationAssociationID` returned by `CreateIntegrationAssociation`\. This is a required step if you want to associate a different Voice ID domain to this Amazon Connect instance\. We do not recommend deleting associations in a production setup as it can cause unpredictable behavior for Voice ID in your Amazon Connect instance\.

1.  [ListIntegrationAssociations](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListIntegrationAssociations.html): To list all the associations between Amazon Connect instance and Voice ID domains for your account in this Region, you can invoke `ListIntegrationAssociations` API\.