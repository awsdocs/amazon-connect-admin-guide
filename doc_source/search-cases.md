# Search and view cases<a name="search-cases"></a>

You can search cases using a keyword match\. Amazon Connect searches data across all system and custom fields\. The results are sorted from most\-recently to least\-recently updated case\.

If you are on a contact, and the contact has been associated to a customer profile, then search automatically filters to cases of current customer\.

![\[The Cases tab, the filter box.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-agent-application-search.png)

Regardless of whether you are on a contact, you have the option to do a general search\. If you are on a contact and want to search beyond the current customer, clear the selection for **Cases of current customer only**\.

## View a case<a name="view-cases"></a>

When you select any of the cases in the search results to view the case, a new tab opens\. This enables you to have multiple cases open at the same time\. 

If you add a [Cases](cases-block.md) block to a flow, and configure it with **Link contact to case** enabled, then cases will open automatically when the agent accepts the contact\. 

![\[The Cases tab opened for contact.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-agent-application-view-multiple-tabs.png)

### Activity feed<a name="cm-activityfeed"></a>

The activity feed shows calls, chats, tasks, and comments from the most recent to least recent Started data\.

Contacts will have an indicator of Ongoing or Completed\. If the contact was completed, there will a Completed/Terminated date/time and a link to **Contact details** that takes user directly to the **Contact details** page\.

Only users who have access to this page will be able to see contact details for a given contact\. Even within this page, there are more granular permissions so different users may see different information\. Information might include: basic contact details/contact attachments, transcripts and recordings with Contact Lens categories, sentiment, and summaries, recordings, etc\.

![\[The activity feed.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-agent-application-activity-feed.png)

### More information<a name="cm-moreinfo"></a>

There may be additional information for agents to view and populate on the **More information** tab, depending on the case template is designed\.

![\[The More information tab.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cases-agent-application-moreinfo.png)