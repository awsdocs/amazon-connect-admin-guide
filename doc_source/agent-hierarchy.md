# Set up agent hierarchies<a name="agent-hierarchy"></a>

 Agent hierarchies are a way for you to organize agents into teams and groups for reporting purposes\. It's useful to organize them based on their location and their skill sets\. For example, you might want to create large groups, such as all agents who work on a specific continent, or smaller groups such as all agents working in a specific department\. 

You can also configure hierarchies with up to five levels, and segment agents or teams\. Here are a couple of things to note about using hierarchies:
+ Removing agents from a level affects historical reporting\.
+ When you use the **Restrict contact access** permission, you can restrict contact search results based on the agent's hierarchy\. For more information, see [Manage who can search for contacts and access detailed information](contact-search.md#required-permissions-search-contacts)\.

## Required permissions<a name="permissions-agent-hierarchy"></a>

To create agent hierarchies, you need the **View \- Agent hierarchy** permission in your security profile\. 

**Note**  
Since agent hierarchies may include location and skill set data, you also need this permission to view the agent hierarchy information in a real\-time metrics report\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/permission-agent-hierarchy.png)

## Create a new agent hierarchy<a name="new-agent-hierarchy"></a>

1. Log in to the Amazon Connect console with an **Admin** account, or an account assigned to a security profile that has permissions to create agent hierarchies\.

1. Choose **Users**, **Agent hierarchy**\.

1. Enter a name and choose **\+** to create the first level of your hierarchy\.

1. Choose **\+** to add more levels to your hierarchy\.

1. Choose **Save** to apply the changes, or **Cancel** to undo them\.
**Tip**  
If the Save button isn't active, you don't have permissions to create or edit the agent hierarchy\.

## Add groups, teams, and agents to a hierarchy<a name="add-groups-teams-agents-hierarchy"></a>

After you create a hierarchy, you can add groups, teams, and agents from the top down\.

1. Select the top level of the hierarchy\.

1. Choose **x** to add groupings to each level\.

1. Choose the check icon to save the name, choose the pencil icon to edit the name\.

1. Choose **Save**\.

Choose **View historical changes** to view the change history\. You can filter changes by date \(between two dates\) or by user name\. If you cannot see the link, ensure that you have the proper permissions to view these changes\.