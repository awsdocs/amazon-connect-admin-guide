# Search for contacts<a name="contact-search"></a>

You can search for contacts as far back as two years ago\.

The search results for a given query are limited to the first 10K results returned\.

When you filter by Contact ID, only results for that specific contact will be returned and other criteria are ignored\. For example, say you search for Contact ID 12345 and agent login Jane Doe\. Results for Contact ID 12345 will be returned regardless of whether Jane Doe was the agent\.

## What's new in contact search<a name="new-contact-search-experience"></a>

Thanks to your feedback, we've made the following changes to contact search\.
+ Search up to 8 weeks\.
+ Multi\-select for filters such as agent names, contact queues, contact flows, and more\. Previously only single\-select was supported\. 

  This new feature is available only for searches with a date range that starts November 2, 2020, or later, when the feature was released\. If you search for contacts that occurred before November 2, 2020, you will be prompted to ensure only one value is selected for each filter mentioned above\. 
+ New filters for [Contact Lens for Amazon Connect](analyze-conversations.md)\. You can now [search for Contact categories](search-conversations.md#contact-category-search) by specifying the full category name\.

  In the **Add filter** drop\-down box, the Contact Lens filters have **CL** next to them\. You can apply these filters only if your organization has enabled Contact Lens\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-search-contact-category-1.png)

  If you want to remove the Contact Lens filters from a user's drop\-down list, remove the following permissions from their security profile: 
  + **Search contacts by conversation**: This controls access to the sentiment scores, non\-talk time, and category searches\.
  +  **Search contacts by keywords**: This controls access to the keywords search\.
  +  **Contact Lens \- speech analytics**: On the Contact Trace Record page, this displays graphs that summarize speech analytics\.

## Manage who can search for contacts and access detailed information<a name="required-permissions-search-contacts"></a>

Before users can search for contacts in Amazon Connect, or access detailed contact information, they need to be assigned to the **CallCenterManager** security profile, or have the following permissions:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-search-required-permissions.png)
+ **Access metrics \- Access** \(Required\): Grants access to metrics data\.
+ **Contact search \- View** \(Required\): Grants access to the **Contact search** page, and the ability to search for contacts\.
+ **Restrict contact access** \(Optional\): Manage a user's access to results on the **Contact search** page based on their agent hierarchy group\.

  For example, agents who are assigned to AgentGroup\-1 can only view contact trace records \(CTRs\) for contacts handled by agents in that hierarchy group, and any groups below them\. \(If they have permissions for **Recorded conversations**, they can also listen to call recordings and view transcripts\.\) Agents assigned to AgentGroup\-2 can only access CTRs for contacts handled by their group, and any groups below them\. 

  Managers and others who are in higher level groups can view CTRs for contacts handled by all the groups below them, such as AgentGroup\-1 and 2\.

  For this permission, **All** = **View** since **View** is the only action granted\.

  For more information about hierarchy groups, see [Set up agent hierarchies](agent-hierarchy.md)\.
**Note**  
When you change a user's hierarchy group, it may take a couple of minutes for their contact search results to reflect their new permissions\.
+ **Contact Lens \- speech analytics**: On the Contact Trace Record page for a contact, you can view graphs that summarize speech analytics: customer sentiment trend, sentiment, and non\-talk time\. 
+ **Recorded conversations \(redacted\)**: If your organization uses Contact Lens for Amazon Connect, you can assign this permission so agents access only those call recordings and transcripts in which sensitive data has been removed\.
+ **Recorded conversations \(unredacted\)**: If your organization isn't using Contact Lens, agents need **Recorded conversations \(unredacted\)** to listen to call recordings or view transcripts\. If desired, you can use **Restrict contact access** to ensure they only have access to detailed information for those contacts handled by their hierarchy group\. 

By default, the Amazon Connect **Admin** and **CallCenterManager** security profiles have these permissions\.

For information about how add more permissions to an existing security profile, see [Update security profiles](update-security-profiles.md)\.

## How to search for a contact<a name="how-to-search-contacts"></a>

1. Log in to Amazon Connect with a user account that has [permissions to access contact records](#required-permissions-search-contacts)\.

1. In Amazon Connect choose **Metrics and quality**, **Contact search**\.

1. Use the filters on the page to narrow your search\. For date, you can search up to 8 weeks at a time\.

**Tip**  
To see if a conversation was recorded, you need to be assigned to a profile that has **Manager monitor** permissions\. If a conversation was recorded, by default the search result will indicate so with an icon in the **Recording** column\. You won't see this icon if you don't have permission to review the recordings\.

## Additional fields: Add columns to your search results<a name="additional-fields"></a>

Use the options under **Additional fields** to add columns in your search results\. These options are not used to filter your search\.

For example, if you want to include columns for **Agent Name** and **Routing profile** in your search output, choose those columns here\.

**Tip**  
The **Is transferred out** option provides the date and time \(in UTC time\) when the transfer was connected\. It maps to `TransferCompletedTimestamp` in the [ContactTraceRecord](ctr-data-model.md#ctr-ContactTraceRecord)\. 

## Download search results<a name="download-search-results"></a>

You can download up to 3,000 search results at a time\. 