# Migrate flows to a different instance<a name="migrate-contact-flows"></a>

Amazon Connect lets you efficiently migrate flows to another instance\. For example, you might want to expand into new Regions, or move flows from your development environment to your production environment\. 

To migrate a few flows, use the [import/export feature](contact-flow-import-export.md) in the flow designer\. 

To migrate hundreds of flows, you need developer skills\. You use the following procedure:

1. Source instance
   + [ListContactFlow](https://docs.aws.amazon.com/connect/latest/APIReference/API_ListContactFlows.html): Retrieve the Amazon Resource Number \(ARN\) for the flows that you want to migrate\.
   + [DescribeContactFlow](https://docs.aws.amazon.com/connect/latest/APIReference/API_DescribeContactFlow.html): Get information about each flow that you want to migrate\.

1. Destination instance
   + [CreateContactFlow](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateContactFlow.html): Create the flows\.
   + [UpdateContactFlowContent](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateContactFlowContent.html): Update the flow content\.

You must also build an ARN\-to\-ARN mapping for queues, flows, and prompts between the source and target Amazon Connect instances, and replace every ARN in the source flow with the corresponding ARN from the target instance\. Otherwise UpdateContactFlowContent fails with `InvalidContactFlow` error\. 

You can update the information in the flows that you migrate\. For more information, see [Amazon Connect Flow Language](flow-language.md)\. 