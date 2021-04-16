# Assign permissions to review recordings of past conversations<a name="assign-permssions-to-review-recordings"></a>

Assign the **CallCenterManager** security profile so a user can listen to call recordings or review chat transcripts\. This security profile also includes a setting that makes the icon to download recordings appear in the results of the **Contact search** page\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/recording-permissions-listen-download-delete.png)

Or, assign the following individual permissions\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/recordings-assign-permissions.png)

1. **Contact search**: This permission is required so you can access the **Contact search** page, which is where you can search contacts so you can listen to recordings and review transcripts\. 

1. **Restrict contact access**: Manage access to results on the **Contact search** page based on their agent hierarchy group\. 

   For example, agents who are assigned to AgentGroup\-1 can only view contact trace records \(CTRs\) for contacts handled by agents in that hierarchy group, and any groups below them\. \(If they have permissions for **Recorded conversations**, they can also listen to call recordings and view transcripts\.\) Agents assigned to AgentGroup\-2 can only access CTRs for contacts handled by their group, and any groups below them\. 

   Managers and others who are in higher level groups can view CTRs for contacts handled by all the groups below them, such as AgentGroup\-1 and 2\.

   For this permission, **All** = **View** since **View** is the only action granted\.

   For more information about hierarchy groups, see [Set up agent hierarchies](agent-hierarchy.md)\.
**Note**  
When you change a the hierarchy group of a user, it may take a couple of minutes for their contact search results to reflect their new permissions\.

1. **Recorded conversations \(redacted\)**: If your organization uses Contact Lens for Amazon Connect, you can assign this permission so agents access only those call recordings and transcripts in which sensitive data has been removed\.

   The redaction feature is provided as part of Contact Lens for Amazon Connect\. For more information, see [Use sensitive data redaction](sensitive-data-redaction.md)\.

1. **Manager monitor**: This permission allows you to monitor live conversations and listen to recordings\.

1. **Recorded conversations \(unredacted\)**: If your organization isn't using Contact Lens for Amazon Connect, you need this permission so you can access the recordings\.

**Tip**  
If you also want the manager to monitor live conversations, assign the manager to the **Agent** security profile so they can access the Contact Control Panel \(CCP\)\. This is so they can monitor the conversation through the CCP\.