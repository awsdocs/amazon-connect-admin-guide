# Migrate contact flows to a different instance<a name="migrate-contact-flows"></a>

Amazon Connect lets you efficiently migrate contact flows to another instance\. For example, you might want to expand into new Regions, or move contact flows from your development environment to your production environment\. 

To migrate a few contact flows, use the [import/export feature](contact-flow-import-export.md) in the contact flow designer\. 

To migrate hundreds of contact flows, use the following procedure:

1. Source instance
   + [ListContactFlow](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListContactFlows.html): Retrieve the Amazon Resource Number \(ARN\) for the contact flows that you want to migrate\.
   + [DescribeContactFlow](https://docs.aws.amazon.com/connect/latest/APIReference/API_DescribeContactFlow.html): Get information about each contact flow that you want to migrate\.

1. Destination instance
   + [CreateContactFlow](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateContactFlow.html): Create the contact flows\.
   + [UpdateContactFlowContent](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateContactFlowContent.html): Update the contact flow content\.

You can update the information in the contact flows that you migrate\. For more information, see [Amazon Connect Flow Language](flow-language.md)\. 