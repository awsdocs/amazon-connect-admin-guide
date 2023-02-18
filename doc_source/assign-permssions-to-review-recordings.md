# Assign permissions to review recordings of past conversations<a name="assign-permssions-to-review-recordings"></a>

Assign the **CallCenterManager** security profile so a user can listen to call recordings or review chat transcripts\. This security profile also includes a setting that makes the icon to download recordings appear in the results of the **Contact search** page\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/recording-permissions-listen-download-delete.png)

Or, assign the following individual permissions\.

1. **Contact search**: This permission is required so users can access the **Contact search** page, which is where they can search contacts so they can listen to recordings and review transcripts\. 

1. **Restrict contact access**: Manage access to results on the **Contact search** page based on their agent hierarchy group\. 

   For example, agents who are assigned to AgentGroup\-1 can only view contact trace records \(CTRs\) for contacts handled by agents in that hierarchy group, and any groups below them\. \(If they have permissions for **Recorded conversations**, they can also listen to call recordings and view transcripts\.\) Agents assigned to AgentGroup\-2 can only access CTRs for contacts handled by their group, and any groups below them\. 

   Managers and others who are in higher level groups can view CTRs for contacts handled by all the groups below them, such as AgentGroup\-1 and 2\.

   For this permission, **All** = **View** since **View** is the only action granted\.

   For more information about hierarchy groups, see [Set up agent hierarchies](agent-hierarchy.md)\.
**Note**  
When you change a the hierarchy group of a user, it may take a couple of minutes for their contact search results to reflect their new permissions\.

1. **Recorded conversations \(redacted\)**: If your organization uses Contact Lens for Amazon Connect, you can assign this permission so agents access only those call recordings and transcripts in which sensitive data has been removed\.

   The redaction feature is provided as part of Contact Lens for Amazon Connect\. For more information, see [Use sensitive data redaction](sensitive-data-redaction.md)\.

1. **Manager monitor**: This permission allows users to monitor live conversations and listen to recordings\.
**Tip**  
Be sure to assign managers to the **Agent** security profile so they can access the Contact Control Panel \(CCP\)\. This enables them can monitor the conversation through the CCP\.

1. **Recorded conversations \(unredacted\)**: If your organization isn't using Contact Lens for Amazon Connect, use this permission to manage who can access recordings on the **Details** page, through corresponding URLs that are generated in S3\. From there, these users can delete recordings\. 

   Note the following:
   + To restrict access to recordings, ensure users do not have **Analytics and Optimization** \- **Recorded conversations \(unredacted\) \- Access** permissions, as shown in the following image\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/recording-permissions-access.png)
   + If users do not have **Recorded conversations** permission—or they're not logged in to Amazon Connect—they cannot listen to the call recording or view the chat transcript, or access the URL in S3, even if they know how the URL is formed\.
   + The **Enable download button** permission controls only whether the download button appears in the user interface\. It does not control access to the recording\. 
   + To enable a user to delete recordings, choose the **Delete** permission\. By default, the **Enable download button** permission is granted too so the user can delete recordings through the user interface\. 