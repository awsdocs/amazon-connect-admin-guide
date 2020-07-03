# Contact search<a name="contact-search"></a>

You can search for contacts as far back as two years ago, 14 days at a time\.

The search results for a given query are limited to the first 10K results returned\.

When you filter by Contact ID, only results for that specific contact will be returned and other criteria are ignored\. For example, say you search for Contact ID 12345 and agent login Jane Doe\. Results for Contact ID 12345 will be returned regardless of whether Jane Doe was the agent\.

**To search contacts**

1. Log in to Amazon Connect with a user account that is assigned the **CallCenterManager** security profile, or one that is enabled for the **Contact search** permission\.

1. In Amazon Connect choose **Metrics and quality**, **Contact search**\.

1. Use the filters on the page to narrow your search\. For date, you can search up to 14 days at a time\.

1. To see additional columns in your search results, expand **Additional fields** to choose what other data you want to view\. Choose **Apply** to view the columns\. 

**Tip**  
To see if a conversation was recorded, you need to be assigned to a profile that has **Manager monitor** permissions\. If a conversation was recorded, by default the search result will indicate so with an icon in the **Recording** column\. You won't see this icon if you don't have permission to review the recordings\.