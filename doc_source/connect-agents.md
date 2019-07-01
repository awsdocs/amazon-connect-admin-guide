# Amazon Connect Agents<a name="connect-agents"></a>

You can manage and load\-balance customer contacts using agent hierarchy organization and agent status management\. These tools provide filtering and agent availability management per queue, skill set, and routing profiles\.

## Agent Hierarchies<a name="agent-hierarchy"></a>

You can organize agents and teams into groups based on their location and their skill sets\. For example, you might want to create large groups, such as all agents who work on a specific continent, or smaller groups such as all agents working in a specific department\. 

You can also configure hierarchies with up to five levels, and segment agents or teams\. The hierarchies are reflected in reports and historical metrics to allow for granulated reporting\. Here are a couple of things to note about using hierarchies:
+ Removing agents from a level affects historical reporting\.
+ Hierarchies do not determine agent permissions or security settings\. They define the organizational structure of agent groups for effective reporting\.

To manage who can create hierarchies and see the location and skill set data, create a security profile and then grant the appropriate permissions to users assigned to that profile\. For more information, see [Amazon Connect Security Profiles](connect-security-profiles.md)\.

**To configure a new agent hierarchy**

1. Choose **Contact management**, **Agent hierarchy**\.

1. Enter a name and choose **\+** to create the first level of your hierarchy\.

1. Choose **\+** to add more levels to your hierarchy\.

1. Choose **Save** to apply the changes, or **Cancel** to undo them\.

When a hierarchy has been created, you can add groups, teams, and agents from the top down\.

**To add groupings to a hierarchy**

1. Select the top level of the hierarchy\.

1. Choose **x** to add groupings to each level\.

1. Choose the check icon to save the name, choose the pencil icon to edit the name\.

1. Choose **Save**\.

Choose **View historical changes** to view the change history\. You can filter changes by date \(between two dates\) or by user name\. If you cannot see the link, ensure that you have the proper permissions to view these changes\.

## Agent Status<a name="agent-status"></a>

Agent status is used for reporting and metrics, as well as resource management\. Amazon Connect provides default editable states, but custom status values can be added\. Customized agent status values are auxiliary by default\.

**To add a new agent status**

1. Choose **Contact management**, **Agent status**, **Add new agent status**\.

1. Enter a status name, description, and type, and select whether the status should be enabled in the CCP\.

1. Choose **Save**\.

**To edit a status**

1. Choose **Contact management**, **Agent status**\.

1. Hover over the status name and choose the pencil icon\.

1. Enter the new information, and choose **Save** to apply the changes\.

Choose **View Historical Changes** to view the change history\. You can filter changes by date \(between two dates\) or by user name\. If you cannot see the **View historical changes** link, ensure that you have the proper permissions to view these changes\.