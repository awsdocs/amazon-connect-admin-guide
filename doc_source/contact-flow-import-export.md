# Import/export flows<a name="contact-flow-import-export"></a>

Use the procedures described in this topic to import/export a flows from the previous flow designer to the new one, from one instance to another, or from one Region to another as you expand your customer service organization\.

**Note**  
To copy and paste flows and blocks in the updated flow designer, the flow must be in the new flow language\. To convert a legacy flow into the new format, you have two options:  
Option 1: In the flow designer user interface, opt in to the updated flow designer\. Your legacy flows are automatically converted\.
Option 2: Manually import the legacy flow using the updated flow designer\.  
This option is most useful for scenarios where you have stored your flows in JSON offline\. For example, for configuration control, you may have flow configurations in an offline data store\. To copy a part of that flow and paste it into the updated flow designer, you need to import it into the updated flow designer\. The importing process converts it to the new flow language\. After that, you can copy and paste within the updated flow designer\. If you want to keep using your offline data store as a source of truth, update the flow with the new format\.

To migrate tens or hundreds of flows, use the APIs described in [Migrate flows to a different instance](migrate-contact-flows.md)\. 

The Flow Import/Export feature is currently in Beta status\. Updates and improvements that we make could result in issues in future releases importing contact flows that are exported during the beta phase\.

## Export limitations<a name="contact-flow-export-limitations"></a>

You can export flows that meet the following requirements:
+ The flow has fewer than 100 blocks\.
+ The total size of the flow is less than 1MB\.

We recommend dividing large flows in to smaller ones to meet these requirements\.

## Flows are exported to JSON files<a name="contact-flow-export-json"></a>

A flow is exported to a JSON file\. It has the following characteristics:
+ The JSON includes a section for each block in the flow\.
+ The name used for a specific block, parameter, or other element of the flow may be different than the label used for it in the user interface \(UI\)\.

By default, flow export files are created without a file name extension, and saved to the default location set for your browser\. We suggest saving your exported flows to folder that contains only exported flows\.

## How to import/export flows<a name="how-to-import-export-contact-flows"></a>

**To export a flow**

1. Log in to your Amazon Connect instance using an account that is assigned a security profile that includes view permissions for flows\.

1. Choose **Routing**, **Contact flows**\.

1. Open the flow to export\.

1. Choose **Save**, **Export flow**\.

1. Provide a name for the exported file, and choose **Export**\.

**To import a flow**

1. Log in to your Amazon Connect instance\. The account must be assigned a security profile that includes edit permissions for flows\.

1. On the navigation menu, choose **Routing**, **Contact flows**\.

1. Do one of the following:
   + To replace an existing flow with the one you are importing, open the flow to replace\.
   + Create a new flow of the same type as the one you are importing\.

1. Choose **Save**, **Import flow**\.

1. Select the file to import, and choose **Import**\. When the flow is imported into an existing flow, the name of the existing flow is updated, too\.

1. Review and update any resolved or unresolved references as necessary\.

1. To save the imported flow, choose **Save**\. To publish, choose **Save and Publish**\.

## Resolve resources in imported contact flows<a name="contact-flow-export-resources"></a>

When you create a flow, the resources you include in the flow, such as queues and voice prompts, are referenced within the flow using the name of the resource and the Amazon Resource Name \(ARN\)\. The ARN is a unique identifier for a resource that is specific to the service and Region in which the resource is created\. When you export a flow, the name and ARN for each resource referenced in the flow is included in the exported flow\.

When you import a flow, Amazon Connect attempts to resolve the references to the Amazon Connect resources used in the flow, such as queues, by using the ARN for the resource\. When you import a flow into the same Amazon Connect instance that you exported it from, the resources used in the flow will resolve to the existing resources in that instance\. If you delete a resource, or change the permissions for a resource, Amazon Connect may not be able to resolve the resource when you import the flow\. When a resource cannot be found using the ARN, Amazon Connect attempts to resolve the resource by finding a resource with the same name as the one used in the flow\. If no resource with the same name is found, a warning is displayed on the block that contains a reference to the unresolved resource\.

If you import a flow into a different Amazon Connect instance than the one it was exported from, the ARNs for the resources used are different\. If you create resources in the instance with the same name as the resource in the instance where the flow was exported from, the resources can be resolved by name\. You can also open the blocks that contain unresolved resources, or resources that were resolved by name, and change the resource to another one in the Amazon Connect instance\. You can save a flow with unresolved or missing resources, but you cannot publish it until the resources are resolved or removed\.