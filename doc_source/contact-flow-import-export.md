# Import/Export Contact Flows<a name="contact-flow-import-export"></a>

You can export contact flows from and import contact flows into your Amazon Connect instance\. This lets you can easily copy contact flows from one Amazon Connect instance to another, for example from a test environment to a production environment, or from one Region to another as you expand your customer service organization\.

**Note**  
The Contact Flow Import/Export feature is currently in Beta status\. Updates and improvements that we make could result in issues in future releases importing contact flows that are exported during the beta phase\.

Because Amazon Connect contact flows are not tied to a specific instance or account, exported flows could also be imported into instances created by other customers, allowing Amazon Connect partners to create custom contact flow solutions that can be used by Amazon Connect customers\.

When you export a contact flow, the most recently saved version of the flow you currently have open in the contact flow designer is exported as a UTF\-8 encoded JSON document\. Each block of your contact flow is included in the JSON document as a separate section\. To import a contact flow, either one that you previous exported, or that was exported from a different Amazon Connect instance, you just select the JSON file and import it\. The imported flow replaces the contact flow currently open in the editor\. The imported contact flow is not added to your Amazon Connect instance until you save it after importing\.

## Resolve Resources in Imported Contact Flows<a name="contact-flow-export-resources"></a>

When you create a contact flow, the resources you include in the contact flow, such as queues and voice prompts, are referenced within the contact flow using the name of the resource and the Amazon Resource Name \(ARN\)\. The ARN is a unique identifier for a resource that is specific to the service and Region in which the resource is created\. When you export a contact flow, the name and ARN for each resource referenced in the contact flow is included in the exported contact flow\.

When you import a contact flow, Amazon Connect attempts to resolve the references to the Amazon Connect resources used in the contact flow, such as queues, by using the ARN for the resource\. When you import a contact flow into the same Amazon Connect instance that you exported it from, the resources used in the contact flow will resolve to the existing resources in that instance\. If you delete a resource, or change the permissions for a resource, Amazon Connect may not be able to resolve the resource when you import the contact flow\. When a resource cannot be found using the ARN, Amazon Connect attempts to resolve the resource by finding a resource with the same name as the one used in the contact flow\. If no resource with the same name is found, a warning is displayed on the block that contains a reference to the unresolved resource\.

If you import a contact flow into a different Amazon Connect instance than the one it was exported from, the ARNs for the resources used are different\. If you create resources in the instance with the same name as the resource in the instance where the contact flow was exported from, the resources can be resolved by name\. You can also open the blocks that contain unresolved resources, or resources that were resolved by name, and change the resource to another one in the Amazon Connect instance\. You can save a contact flow with unresolved or missing resources, but you cannot publish it until the resources are resolved or removed\.

## Export and Import a Contact Flow<a name="contact-flow-labels"></a>

When you export a contact flow, the JSON document created for the flow includes a section for each block in the flow\. The name used for a specific block, parameter, or other element of the contact flow may be different than the label used for it in the user interface \(UI\)\.

By default, contact flow export files are created without a file name extension, and saved to the default location set for your browser\. We suggest saving your exported contact flows to folder that contains only exported contact flows\.

**Important**  
When you attempt to import or export a large or complex contact flow, the export may fail if the contact flow contains a large amount of blocks and resources\. It may also fail if the file size for the exported contact flow exceeds 1 MB in size\. An notification message is displayed when this occurs\.

**To export a contact flow**

1. Log in to your Amazon Connect instance using an account that is assigned a security profile that includes view permissions for contact flows\.

1. Choose **Routing**, **Contact flows**\.

1. Open the contact flow to export\.

1. Choose **Save**, **Export flow**\.

1. Provide a name for the exported file, and choose **Export**\.

**To import a contact flow**

1. Log in to your Amazon Connect instance\. The account must be assigned a security profile that includes edit permissions for contact flows\.

1. Choose **Routing**, **Contact flows**\.

1. Do one of the following:
   + To replace an existing contact flow with the one you are importing, open the contact flow to replace\.
   + Create a new contact flow of the same type as the one you are importing\.

1. Choose **Save**, **Import flow**\.

1. Select the file to import, and choose **Import**\.

1. Review and update any resolved or unresolved references as necessary\.

1. To save the imported flow, choose **Save**\. To publish, choose **Save and Publish**\.