# Sort agents by activity in a real\-time metrics report<a name="rtm-sort-by-agent-activity"></a>

On the real\-time metrics **Agents** report, you can sort agents by **Activity** when agents are enabled to use the same channel\.

For example, the following image shows that you can sort agents by the **Activity** column because all the agents are enabled to use the same channel: voice\.

![\[The Agents report, the sort icon for the Activity column.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/agent-activity-sortable.png)

However, if one or more agents are enabled to handle voice, chat, and tasks—or any two of the channels—you can't sort them by the **Activity** column because of the multiple channels\. In this case, there's no option to sort by the **Activity** column, as shown in the following image:

![\[The Agents report, no sort icon appears in the Activity column.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/agent-activity-not-sortable.png)

**Note**  
The real\-time metrics Agents report doesn't support secondary sorting\. For example, you can't sort by **Activity**, and then sort by **Duration**\.