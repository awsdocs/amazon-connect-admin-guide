# Import/export contact flows<a name="contact-flow-import-export"></a>

Use the procedures described in this topic to import/export a few contact flows from one instance to another, or from one Region to another as you expand your customer service organization\.

To migrate tens or hundreds of contact flows, use the APIs described in [Migrate contact flows to a different instance](migrate-contact-flows.md)\. 

**Note**  
The Contact Flow Import/Export feature is currently in Beta status\. Updates and improvements that we make could result in issues in future releases importing contact flows that are exported during the beta phase\.

## Export limitations<a name="contact-flow-export-limitations"></a>

You can export contact flows that meet the following requirements:
+ The flow has fewer than 100 blocks\.
+ The total size of the flow is less than 1MB\.

We recommend dividing large flows in to smaller ones to meet these requirements\.

## Contact flows are exported to JSON files<a name="contact-flow-export-json"></a>

A contact flow is exported to a JSON file\. It has the following characteristics:
+ The JSON includes a section for each block in the flow\.
+ The name used for a specific block, parameter, or other element of the contact flow may be different than the label used for it in the user interface \(UI\)\.

By default, contact flow export files are created without a file name extension, and saved to the default location set for your browser\. We suggest saving your exported contact flows to folder that contains only exported contact flows\.

## How to import/export contact flows<a name="how-to-import-export-contact-flows"></a>

**To export a contact flow**

1. Log in to your Amazon Connect instance using an account that is assigned a security profile that includes view permissions for contact flows\.

1. Choose **Routing**, **Contact flows**\.

1. Open the contact flow to export\.

1. Choose **Save**, **Export flow**\.

1. Provide a name for the exported file, and choose **Export**\.

**To import a contact flow**

1. Log in to your Amazon Connect instance\. The account must be assigned a security profile that includes edit permissions for contact flows\.

1. On the navigation menu, choose **Routing**, **Contact flows**\.

1. Do one of the following:
   + To replace an existing contact flow with the one you are importing, open the contact flow to replace\.
   + Create a new contact flow of the same type as the one you are importing\.

1. Choose **Save**, **Import flow**\.

1. Select the file to import, and choose **Import**\. When the contact flow is imported into an existing contact flow, the name of the existing contact flow is updated, too\.

1. Review and update any resolved or unresolved references as necessary\.

1. To save the imported flow, choose **Save**\. To publish, choose **Save and Publish**\.

## Resolve resources in imported contact flows<a name="contact-flow-export-resources"></a>

When you create a contact flow, the resources you include in the contact flow, such as queues and voice prompts, are referenced within the contact flow using the name of the resource and the Amazon Resource Name \(ARN\)\. The ARN is a unique identifier for a resource that is specific to the service and Region in which the resource is created\. When you export a contact flow, the name and ARN for each resource referenced in the contact flow is included in the exported contact flow\.

When you import a contact flow, Amazon Connect attempts to resolve the references to the Amazon Connect resources used in the contact flow, such as queues, by using the ARN for the resource\. When you import a contact flow into the same Amazon Connect instance that you exported it from, the resources used in the contact flow will resolve to the existing resources in that instance\. If you delete a resource, or change the permissions for a resource, Amazon Connect may not be able to resolve the resource when you import the contact flow\. When a resource cannot be found using the ARN, Amazon Connect attempts to resolve the resource by finding a resource with the same name as the one used in the contact flow\. If no resource with the same name is found, a warning is displayed on the block that contains a reference to the unresolved resource\.

If you import a contact flow into a different Amazon Connect instance than the one it was exported from, the ARNs for the resources used are different\. If you create resources in the instance with the same name as the resource in the instance where the contact flow was exported from, the resources can be resolved by name\. You can also open the blocks that contain unresolved resources, or resources that were resolved by name, and change the resource to another one in the Amazon Connect instance\. You can save a contact flow with unresolved or missing resources, but you cannot publish it until the resources are resolved or removed\.